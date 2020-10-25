---
title: selenium+requests爬取百度图片（基础篇）
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 18:26:39
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/012.jpg
coverImg:
password:
summary:
tags: 
  - [python]
  - [Selenium]
categories:
  - [python]
  - [Selenium]
---

``` python
写着玩儿的
# coding=utf-8
from selenium import webdriver
import requests,time,os
d = webdriver.Chrome()
d.maximize_window()
d.get("https://www.baidu.com")
d.find_element_by_id("kw").send_keys("吴彦祖")
d.find_element_by_id("su").click()
time.sleep(1)
d.find_element_by_xpath("//div[@id='content_left']//a").click()
time.sleep(1)
handles = d.window_handles
d.switch_to.window(handles[1])
eles = d.find_elements_by_xpath("//div[@class='imgbox']//img")
print(eles)
urls=[]
for ele in eles:
    url = ele.get_attribute("src")
    urls.append(url)
print(urls)
path =r"C:\Users\shixi\Desktop\吴彦祖\\"
#如果路径不存在，则新建路径
if os.path.isdir(path)!=True:
    os.mkdir(path)
i = 0
for url in urls:
    fname = url.split(",")[1].split("&")[0]+".jpg"
    resp = requests.get(url,timeout=30)
    data = resp.content
    with open(path+fname,'wb') as f:
        f.write(data)
    i+=1
    if i==9:
        break
d.quit()
```
