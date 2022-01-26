---
date: 2022-01-27 06:41:00
layout: post
title: "Tranquility"
subtitle: 疯女人与好女人与坏女人与电锯人
description: 电锯人好看  
image: /assets/82598639_zuuutgsty.jpg
optimized_image: /assets/82598639_zuuutgsty.jpg
category: blog
tags:
- scrapy
- scapy
author: Ayerlans
paginate: false
music_id: 135410567
istopfeatured: false
---
```
DEFAULT_REQUEST_HEADERS = {
   'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
    'Accept-Language': 'en',
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.113 Safari/537.36'
}
```
```

def get_all_info_of_one_market():
    Cookie = ''

    headers = {
    }
    url = ""
    print(url)
    response = requests.get(url, headers=headers)
    soup = BeautifulSoup(data, 'lxml')
    # print(soup)
    all_staff = soup.find_all(class_="p-name")
    # print(all_staff)
    # print(type(all_staff))
    # soup = BeautifulSoup(all_staff, 'lxml')
    result_title = []
    i = 0
    for staff in all_staff:
        # result_title.extend()
        staff_a_tag = staff.find('a')
        # print(type(staff_a_tag))
        if staff_a_tag:
            aherf = staff_a_tag['href']
            # print(aherf)
            # urlparse已经被移动至urllib.parse.urlparse
            result = urllib.parse.urlparse(aherf)
            # print(result)
            only_skuId = urllib.parse.parse_qs(result.query)
            # print(only_skuId)
            # 数据类型 字典dic
            # print(type(only_skuId))
            skuId = only_skuId['skuId']
            # print(type(skuId))
            skuId_str = ''.join(skuId)
            print(skuId_str)
            a_name = staff_a_tag['title']
            print(a_name)

        # staff_a_tag.get['href']
        # print(result_title)
        # print(staff)
        # title=staff.find_all("title")
        # print(title)

```
##### 听了大家的话 第一次 感觉高考没考好是件好事
其实也不是这样 只是比较满足?  
有些人的亚银保了北大  
有些人的亚银给了他慢性病 再不能从事代码工作     
确实 考好了有用 应该是我想错了 山高路远  
scrapy和scapy只差了一个字 好奇怪的两个包  
可是没了nas 我存不了那么多 scapy就不能用了  
不过能去上交确实厉害 心态好好  
被成都,广州和上海的看过?  
是SEO起效果了吗 还是引来了怪人 用钉钉看博客也是好雅兴   
电锯人好看  一晚上看完了  
![](/assets/markdown-img-paste-20220127002413964.png)
