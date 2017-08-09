# **爬虫**

## 需求
> 总体的框架为兴趣脸谱，总体的流程为输入**微博用户UID**，通过爬虫获取该用户的个人资料以及微博内容，从中归纳总结出其潜在的兴趣，对这些兴趣进行分类，最后对该用户根据兴趣分类进行**产品推荐**。
> 
> 本部分主要介绍爬虫爬取过程中遇到的问题以及解决方案，并且针对目前版本的爬虫程序，汇报测试结果以及预计成果。

## 问题
> 编写爬虫之前需要先明确以下三个问题：
1. 爬什么？
2. 怎么爬？
3.  怎么反爬？

<br></br>
**Q:** 爬什么？
**A:** 爬取的内容完全依赖后期数据处理的需求，当前可以爬取的内容包括微博资料页的所有内容以及关注人、粉丝列表

**Q:** 怎么爬？
**A:** 从爬取方法上主要可以通过Request GET的方式来获取静态网页内容，然后通过不同的爬取策略对网页内容进行解析，由此扩展出[Scrapy](https://scrapy.org/)，Python开发的一个快速,高层次的屏幕抓取和Web抓取框架，用于抓取Web站点并从页面中提取结构化的数据。Scrapy用途广泛，可以用于数据挖掘、监测和自动化测试。Scrapy吸引人的地方在于它是一个框架，任何人都可以根据需求方便的修改。

**Q:** 怎么反爬？
**A:** 爬虫可以说是道高一尺，魔高一丈，爬虫从诞生的一刻，就是一场互相博弈的战争，永远处于爬虫-反爬虫的技术斗争中。面对各大网站的反爬机制，需要见招拆招，目前接触到的反爬机制有验证码登录，手势码登录，IP检测，异常操作处理等手段，针对不同的反爬机制，我们整理了一些当前比较成熟的反反爬手段针锋相对，具体细节和处理结果见下一章。

## 方案
1. 基于需求的爬取
2. 页面解析工具
	* Regular Expression
	* Xpath
	* BeautifulSoup
3. 反反爬对策
	* User Agent
	* 动态IP池
	* Cookie池 

###细节整理

针对特定网页（如微博、百度热点、搜狗微信公众号、百度指数）通过Request + Urllib2获取网页信息，返回得到html表单，以[百度热点](http://top.baidu.com/buzz.php?p=top10)为例: 

    baiduUrl = 'http://top.baidu.com/buzz.php?p=top10'
    html = requests.get(url = baiduUrl).content

通过BeautifulSoup或Xpath对html表单进行解析：

    # BeautifulSoup解析html内容判断该新闻是否存在简介
    soup = BeautifulSoup(html,"lxml")
    hasDetail = soup.find('div', class_ ="c-span-last")

    # Xpath提取微博用户名
    selector = etree.HTML(html）
    userName = selector.xpath("//title/text()")[0]

同时，利用正则表达式对个别元素进行进一步的特征提取，如提取微博用户关注人数：

    pattern = r"\d+\.?\d*"
    str_gz = selector.xpath("//div[@class='tip2']/a/text()")[0]
    guid = re.findall(pattern, str_gz, re.M)
<br></br>
应对反爬机制的处理方法介绍：

在Scrapy框架下定义了[Downloader Middleware](https://doc.scrapy.org/en/latest/topics/downloader-middleware.html),即下载器中间件，它介于Scrapy的request/response处理的钩子框架，是用于全局修改Scrapy request和response的一个轻量、底层的系统。

在这里，我们可以在修改爬虫在request/response处理页面之前的参数配置问题。简单来说，将事先得到的User Agents, IP以及Cookies信息存在路径下的`list`中，通过中间件的处理，随机选择不同的User Agent, IP以及Cookie组合，来避免网页跳转的问题。具体实现如下（以User Agent为例）：

    from user_agents import agents
	class UserAgentMiddleware(object):
	    def process_request(self, request, spider):
	        agent = random.choice(agents)
	        request.headers["User-Agent"] = agent

## 结果
目前对于微博的爬虫已经基本完成，所需求的数据内容都已经实现了爬取，以下为部分成果展示（红色框内为当前可以爬取的内容）：

![Img1](https://github.com/AgentCyrusJr/markdown/raw/master/weekly/img1.PNG)

![Img2](https://github.com/AgentCyrusJr/markdown/raw/master/weekly/img2.PNG)

![Img3](https://github.com/AgentCyrusJr/markdown/raw/master/weekly/img3.PNG)

目前微博爬取内容清单（以下内容均可以通过数据库或者.txt文本形式输出）：
+ 用户UID、昵称、性别、生日、地区、简介、标签
+ 用户粉丝数、关注数
+ 用户粉丝列表、关注人列表
+ 微博内容以及对应的点赞数、转发数、评论数



## 展望







