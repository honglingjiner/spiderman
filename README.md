# spiderman
spider_practice

#! /usr/bin/env python3
import requests
import json
import re


headers = {
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.81 Safari/537.36'
}
ls=[]
url = ' https://u.y.qq.com/cgi-bin/musicu.fcg'
for i in list(range(297)):
    i=i+1
    print(i)
    cur_page = i
    per_page = 80
    sin = (cur_page - 1) * per_page
    data = {"comm": {"ct": 24, "cv": 0}, "singerList": {"module": "Music.SingerListServer", "method": "get_singer_list",
                                                    "param": {"area": -100, "sex": -100, "genre": -100, "index": -100,
                                                              "sin": sin, "cur_page": cur_page}}}
    data = json.dumps(data)
    data = data.replace(' ', "")
    req = requests.get(url, headers=headers, params={"data": data})
    html = req.content.decode()
    pattern=re.compile('{"country":"(.*?)","singer_id":(.*?),"singer_mid":"(.*?)","singer_name":"(.*?)"(.*?)',re.S)
    data_final=pattern.findall(html)
    for item in data_final:
        ls.append(item[3])
    print(ls)
'''  res  = req.json()
    for singer in res['singerList']['data']['singerlist']:
        singer_name = singer['singer_name']
        print(singer_name)
        ls.append(singer_name)'''
with open('test.csv','w',encoding='utf-8') as f:
    f.write(str(ls))
   
推荐业务标签拓展----爬取QQ音乐歌手列表
    
    
    
    
