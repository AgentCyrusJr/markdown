# **Simple WEB crawler**

### It is currently available on:
+ Weibo
+ Baidu real-time headlines
+ Sougou real-time keywords and headlines

###And the following target will be coming soon:
+ Baidu Index
+ ...

## Instructions
Under the directory `Headlines\`, execute the following in command lines:

`$ scrapy crawl Headlines -a target=[option]`

>  [option] can be replaced: 
	> 1. "baidu"   ( for Baidu real-time headlines ) 
	> 2. "sougou"   ( for Sougou real-time keywords and headlines )

For example, you want to crawl 'sougou':

`$ scrapy crawl Headlines -a target="sougou"` 

## Introductions
In this **scrapy**-based web crawler, we have currently defined three types of items:

1. BaiduItem()  
2. SougouHotWordItem()
3. SougouHotNewsItem()
4. ... *(more are coming)*

Among these three items, we have also provided several attributes:

+ rank
+ time
+ title
+ source
+ summary
+ upOrDown
+ ImageUrl
+ detailsUrl
+ relatedNews
+ searchIndex
+ ... *(more are coming)*





