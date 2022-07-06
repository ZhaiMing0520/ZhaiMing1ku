import requests
from lxml import html
etree=html.etree

def huya_girl():

    url="https://www.huya.com/g/4079"
    headers={
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36 Core/1.77.106.400 QQBrowser/10.9.4626.400"
    }
    response=requests.get(url=url,headers=headers)
    data=etree.HTML(response.text)
    girls=data.xpath('//img[@class="pic"]')

    for girl in girls:
        img_url=girl.xpath('./@data-original')[0]
        # print(img_url)
        name=girl.xpath('./@alt')[0]
        img_url= img_url.split("?")[0]
        image=requests.get(url=img_url,headers=headers)
        with open('./Girl/%s.jpg' % name,'wb')as jpg:
            jpg.write(image.content)
        print('《%s》 下载完毕' % name)
huya_girl()