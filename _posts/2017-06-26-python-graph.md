---
layout: post
title:  "Pandas 이용해서 XRD 그래프 그리기"
date:   2017-06-24 19:46:00
---

# Pandas 이용해서 XRD 그래프 그리기

## 파이썬을 이용해서 XRD 원본 Data(csv)를 읽어 오는 법

csv파일 읽어 오기 (현재의 폴더내에 '파일이름.csv'가 있을때)


    import pandas as pd
    rawData = pd.read_csv('파일이름.csv')

    
파일이름.csv가 다른 폴더에 있으면 경로를 같이 기록해 주어야 한다.


파일이름.csv의 구성은 아래와 같다.

| Angle |   Intensity |
| :---: | :----------:|
| 10.0  | 234         |
| 10.1  | 343         |
| 10.2  | 443         |
| 10.3  | 543         |
| 10.4  | 453         |
| 10.5  | 345         |
| 10.6  | 373         |
| 10.7  | 348         |

DataFrame의 columns를 확인하면 아래와 같이 나온다.

    rawData.columns
    Index(['Angle', 'Intensity'], dtype='object')


그림 그리기는 아래의 코드를 사용한다.

    import matplotlib.pyplot as plt
    plt.plot(rawData.Angle, rawData.Intensity)

그림은 아래와 같다.

![graph image](/images/xrd_example.png)
