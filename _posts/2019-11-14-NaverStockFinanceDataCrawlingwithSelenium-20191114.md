---
layout: post
title:  "셀레니움을 이용한 네이버 증권 상장사 재무정보 크롤링"
date:   2019-11-14 17:00:00
---


# 셀레니움을 이용한 네이버 증권 상장사 재무정보 클롤링



네이버 증권에서 재무제표를 수집하는 파이썬 스크립트이다.
전체 내용은 https://shinminyong.tistory.com/15의 코드를 사용했다.

내가 추가 한 부분은 모든 종목을 루프를 돌려가면서 재무제표를 저장하는 것과 재무제표가 없는 기업에 대해 예외 처리를 하는 것이다.

실제 돌려보면 에러나 발생하면서 루프가 중단이 된다.

그 이유까지는 확인을 못 했다.

종목 리스트는 [FinanceDatareader](https://github.com/FinanceData/FinanceDataReader) 패키지를 이용해서 다운 받은 자료를 사용했다.

아직 iframe내에 접근하는 방법에 대해서는 제대로 이해를 못 했다.

단지 아래의 코드를 사용해서 필요한 자료를 구할 수는 있었다.



```

import requests # 웹 페이지 소스를 얻기 위한 패키지(기본 내장 패키지이다.)
from bs4 import BeautifulSoup # 웹 페이지 소스를 얻기 위한 패키지, 더 간단히 얻을 수 있다는 장점이 있다고 한다.
from datetime import datetime                                # (!pip install beautifulsoup4 으로 다운받을 수 있다.)
import pandas as pd # 데이터를 처리하기 위한 가장 기본적인 패키지
import time # 사이트를 불러올 때, 작업 지연시간을 지정해주기 위한 패키지이다. (사이트가 늦게 켜지면 에러가 발생하기 때문)
import urllib.request #
from selenium.webdriver import Chrome
import json
import re
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
import datetime as dt



def stock_crawler(code):
    #code = 종목번호
    name = code
    base_url = 'https://finance.naver.com/item/coinfo.nhn?code='+ name + '&target=finsum_more'

    browser.get(base_url)
    #frmae구조 안에 필요한 데이터가 있기 때문에 해당 데이터를 수집하기 위해서는 frame구조에 들어가야한다.
    browser.switch_to_frame(browser.find_element_by_id('coinfo_cp'))

    #재무제표 "연간" 클릭하기
    browser.find_elements_by_xpath('//*[@class="schtab"][1]/tbody/tr/td[3]')[0].click()

    browser.implicitly_wait(1)

    html0 = browser.page_source
    html1 = BeautifulSoup(html0,'html.parser')

    #기업명 뽑기
    title0 = html1.find('head').find('title').text
    print(title0.split('-')[-1])

    html22 = html1.find('table',{'class':'gHead01 all-width','summary':'주요재무정보를 제공합니다.'})

    #date scrapy
    thead0 = html22.find('thead')
    tr0 = thead0.find_all('tr')[1]
    th0 = tr0.find_all('th')

    date = []
    for i in range(len(th0)):
        date.append(''.join(re.findall('[0-9/]',th0[i].text)))

    #columns scrapy
    tbody0 = html22.find('tbody')
    tr0 = tbody0.find_all('tr')

    col = []
    for i in range(len(tr0)):

        if '\xa0' in tr0[i].find('th').text:
            tx = re.sub('\xa0','',tr0[i].find('th').text)
        else:
            tx = tr0[i].find('th').text

        col.append(tx)

    #main text scrapy
    td = []
    for i in range(len(tr0)):
        td0 = tr0[i].find_all('td')
        td1 = []
        for j in range(len(td0)):
            if td0[j].text == '':
                td1.append('0')
            else:
                td1.append(td0[j].text)

        td.append(td1)

    td2 = list(map(list,zip(*td)))

    return pd.DataFrame(td2,columns = col,index = date)


krx_code_list = pd.read_csv('KRX_stock_list.csv')
# KRX_stock_list.csv는 finance-datareader 를 통해서 다운 받았다.
#

for i in krx_code_list['Symbol']:
    code = str(i).zfill(6)
    browser  = Chrome(executable_path="/home/park/Downloads/chromedriver")
    browser.maximize_window()

    try:
        fin_data = stock_crawler(code)
        fin_data.to_csv(code + '_fin_data_fr_naver.csv')
    except:
        print("페이지를 찾을 수 없습니다.")
    finally:
        browser.quit()

```
