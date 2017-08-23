# **基于百度指数的舆情分析**

## 第一部分：爬取搜索词的舆情
> 输入搜索词（eg.**平安银行**），通过百度指数中的‘舆情分析’中的最新新闻，分析搜索词在当前环境下的舆情指数

### 涉及内容：
1. Selenium半自动登录，模拟操作
2. API调用获取新闻信息

### Demo演示一
测试前准备：
打开`~/roujiamo/`下的`baiduAccount.txt`，修改百度账号密码


在`~/roujiamo/`文件夹下，运行`python roujiamo.py`

在命令行输入你感兴趣的搜索词（eg.**平安银行**），

> input keyword for search:平安银行

脚本会自动打开Chrome浏览器进入百度账号登录界面，观察验证码，

> input verification code:[验证码]

不出意外，百度要求登录账号时输入手机验证码，

> please input six-digit code received from your phone:[六位验证码]

一切顺利的话，登录成功会跳转到百度首页，通过执行js来新开一个窗口，

>`js = 'window.open("http://index.baidu.com");'`
>`browser.execute_script(js)`

利用Selenium模拟操作找到‘舆情洞察’按钮，

>`sentiment = browser.find_elements_by_xpath("//i[@class = 'icons sentimentIcon']")[0]`

模拟鼠标点击按钮，跳转到‘舆情洞察’界面，获取搜索词新闻源，

![](https://github.com/AgentCyrusJr/markdown/raw/master/20170821153943.png)

打开新闻源网页，调用易源接口API获取新闻正文，存入`~/roujiamo/roujiamo.csv`，很稳！

## 第二部分：舆情内容的情感分析
> 分析正文中的情感极性，给出极性打分

### 涉及内容：
1. [情感极性分析库](https://github.com/chaoming0625/SentimentPolarityAnalysis)
	>现在找到的这个库我看了一下，主要是用于分析电商产品的点评，分词的倾向性比较严重，该模型中的字典`~\SentimentPolarityAnalysis\spa\f_dict\`不是很适合做舆情的情感分析

### Demo演示二
测试前准备：
1. Python 3.6 以及部分库
2. 把舆情正文内容存入一个`test.txt`文件中，路径问题不大

在`~\SentimentPolarityAnalysis\spa\`下，
> `from classifiers import DictClassifier`
> `d = DictClassifier()`
`result = d.analysis_file([inputfile], [outputfile], encoding="utf-8", print_show=True, start=0, end=-1)`

对每一句话单独进行评分，
![](https://github.com/AgentCyrusJr/markdown/raw/master/ss0823_2.PNG)

对正文所有内容的情感进行总体打分，
![](https://github.com/AgentCyrusJr/markdown/raw/master/ss0823.PNG)

## 第三部分：缺陷分析
1. 登录过程要观察输入验证码，必须在有可视化界面的服务器上才能跑
2. 并没有实现全自动化，第一部分需要手动输入两次验证码，第二部分是python3.6版本，并且需要对收集到的舆情新闻做简单的处理（删除换行等）
3. 现版本的模型训练（打分的词典）不是很适合舆情分析，NLP没有做过深入研究，需要花点时间。

















