# **基于百度指数的舆情分析**

## 第一部分：爬取搜索词的舆情
> 输入搜索词（eg.**平安银行**），通过百度指数中的‘舆情分析’中的最新新闻，分析搜索词在当前环境下的舆情指数

### 涉及内容：
1. Selenium半自动登录，模拟操作
2. API调用获取新闻信息

### Demo演示
测试前准备：
打开`~/roujiamo/`下的`baiduAccount.txt`，修改百度账号密码

在`~/roujiamo/`文件夹下，运行`python roujiamo.py`

在命令行输入你感兴趣的搜索词（eg.**平安银行**），

> input keyword for search:平安银行

脚本会自动打开Chrome浏览器进入百度账号登录界面，观察验证码，

> input verification code:[验证码]

不出意外，百度要求登录账号时输入手机验证码，

> please input six-digit code received from your phone:[6位验证码]

一切顺利的话，登录成功会跳转到百度首页，通过执行js来新开一个窗口，

>`js = 'window.open("http://index.baidu.com");'`
>`browser.execute_script(js)`

利用Selenium模拟操作找到‘舆情洞察’按钮，

>`sentiment = browser.find_elements_by_xpath("//i[@class = 'icons sentimentIcon']")[0]`

模拟鼠标点击按钮，跳转到‘舆情洞察’界面，获取搜索词新闻源，

![](https://github.com/AgentCyrusJr/markdown/raw/master/20170821153943.png)

打开新闻源网页，调用易源接口API获取新闻正文，存入`~/roujiamo/roujiamo.csv`，很稳！










