---
title: Python生成双色球号码
author: MZ-ZONE
top: false
cover: true
toc: true
mathjax: false
date: 2020-08-23 15:19:02
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/039.jpg
coverImg:
password:
summary:
tags: 双色球
categories: 
   - python
---

``` python
import random,time
def process_int(x):
    '''这个函数用来把int类型转成字符串'''
    x = str(x)
    if len(x)==1:
        #如果是个位数前面加0
        x='0'+x
    return x
def tickets(num):
#:num 产生几条这个函数是用来随机产生双色球号码的，每次把产生的号码保存在当天日期的文件中
 
    red_nums = list(map(process_int,range(1,34)))
    #红球，范围在1-33，使用map把每个元素传给process_int转成字符串
    blue_nums = list(map(process_int,range(1,17)))
    #蓝球，范围在1-16
    res_list = []#保存所有的结果，用来写到文件里面
    for i in range(1,num+1):
        red_num = random.sample(red_nums, 6)
        blue_num = random.sample(blue_nums, 1)
        res = red_num+blue_num
        format_str = '第%s个：红球：%s 蓝球  %s'%(i,' , '.join(res[:7]),res[-1])
        res_list.append(format_str+'\n')
        print(format_str)
    cur_time = time.strftime('%Y.%m.%d %H_%M_%S')
    with open('%s.txt'%cur_time,'w',encoding='utf-8') as fw:
        fw.writelines(res_list)
if __name__ =='__main__':
    nums = input('请输入你要产生多少条双色球号码：').strip()
    tickets(int(nums))
```
