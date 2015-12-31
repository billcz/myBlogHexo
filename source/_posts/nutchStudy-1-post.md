title: 爬虫工具nutch学习系列１  - 入门
date: 2015-12-30 19:19:37
tags: crawler
clearReading: true
thumbnailImage: ""
thumbnailImagePosition: bottom
autoThumbnailImage: yes
metaAlignment: center
coverImage: cover.jpg
coverCaption: "Life is beautiful"
coverMeta: in
comments: false
---

## Nutch简介
Nutch是Apache开源项目里的网络爬虫(Web crawler)，包括２大功能：网络爬虫和索引建立。Nutch目的是能够建立强大的搜索引擎。Nutch 1.x支持Hadoop分布式爬取，建立反向索引至solr，直接能在solr进行搜索。Nutch 2.x使用Gora(Apache开源项目，大数据序列化工具)开始支持多种数据源的导出，支持HBase、MySQL(2.3后不支持)、Solr、ElasticSearch等。

## 安装
- 下载安装包apache-nutch-1.X-bin.zip
- 解压
- cd apache-nutch-1.X/
- 配置环境变量NUTCH_RUNTIME_HOME，指向nutch所在路径

验证是否安装成功，敲入命令bin/nutch，显示如下类似信息：
``` bash
    Usage: nutch COMMAND where command is one of:
    readdb            read / dump crawl db
    mergedb           merge crawldb-s, with optional filtering
    readlinkdb        read / dump link db
    inject            inject new urls into the database
    generate          generate new segments to fetch from crawl db
    freegen           generate new segments to fetch from text files
    fetch             fetch a segment's pages
    ...

```

<!-- more -->

## 爬取你的第一个网站
Nutch只需２步配置，就能开始爬虫任务
1. 自定义nutch爬虫配置，主要是文件conf/nutch-site.xml. 在文件中加入如下内容：
``` bash
<property>
         <name>http.agent.name</name>
         <value>My Nutch Spider</value>
</property>
```

2. 创建一个url种子列表文件
url种子文件定义了初始要爬取的网站，一行一个，nutch会逐个爬取。
    - 在nutch目录创建一个urls目录。
 ``` bash
mkdir -p urls
cd urls
```
    - 新建一个seed.txt，在该文件中写入要爬取网站。例如：
``` bash
http://nutch.apache.org/
```
3. 创建过滤规则(可选)
 - 配置文件conf/regex-urlfilter.txt定义了爬取的规则，包括了一些正则表达式。如若只爬取nutch.apache.org的网站，将
``` bash
# accept anything else
+.
```
 - 修改为：
``` bash
+^http://([a-z0-9]*\.)*nutch.apache.org/
```
## 总结
本节简单介绍了nutch和一个简单的例子。主要对nutch有个初步的认识。下节介绍如何自定义爬取并建立索引，并在Solr里进行搜索。
