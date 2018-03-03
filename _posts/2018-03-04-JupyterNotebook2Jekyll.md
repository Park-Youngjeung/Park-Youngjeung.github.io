---
layout: post
title:  "Jupyter Notebook을 Jekyll로  "
date:   2018-03-04 01:00:00
---


Juputer Notebook을 Jekyll로 변경하는 방법
======================================

파이썬으로 데이터 주무르기라는 책을 공부 중인데, 여기서 Jupyter Notebook으로 실행한 내용을 Jekyll로 옮기는 방법을 기술함


참조한 사이트


[Display Jupyter Notebook with Jekyll](https://linode.com/docs/applications/project-management/jupyter-nobook-on-jekyll "title")


상기 링크에서 설명하는 바에 따르면 Notebook의 File > Download As > Markdown (.md)에서 다운을 받을 수 있다. 다른 방법으로는 ipynb파일을 command line에서 직접적으로 생성할 수 있다.


'''jupyter nbconvert --to markdown /path/to/example_notebook.ipynb'''


다음 3, 4항은 마크다운 파일 만드는 것에 대해 이야기하는데, 알고 있으므로 생략한다.


5번항은 jupyter에서 내보낸 마크다운 파일 내용을 새로운 포스트 파일에 붇여 넣는 내용이다.


'''cat example_notebook.md | tee -a exampleblog/_post/YYYY-MM-DD-example-post.md'''


Modify Markdown Files 부분은 잘 몰라서 생략한다.


##Add an Image in Jekyll 부분

1. Jupyter에서 내보낸 모든 이미지 파일을 /assets/images 폴더로 옮긴다.

2. 적절한 결로에 마크다운으로 이미지 참조를 수정한다. 결로는 중괄호(}) 두개와 쌍따옴표('"')로 감싼다.

'''![png]({{"/assets/images/example_notebook_5_0.png"}})'''

/assets/images/ 경로로 되어 있는데, 내 경로는 그냥 /images이다.

3. 더 긴 차원에서 범례를 갖는 그래프가 표시된다.


```python
import os
import sys
os.chdir('/home/park/DataScience/data/')
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

from matplotlib import font_manager, rc
plt.rcParams['axes.unicode_minus'] = False
path = '/usr/share/fonts/truetype/nanum/NanumGothic.ttf'
font_name = font_manager.FontProperties(fname=path).get_name()
rc('font', family=font_name)
```


```python
CCTV_Seoul = pd.read_csv('../data/01. CCTV_in_Seoul.csv', encoding='utf-8')
CCTV_Seoul.head()
CCTV_Seoul.rename(columns={CCTV_Seoul.columns[0] : '구별'}, inplace=True)
pop_Seoul = pd.read_excel('01. population_in_Seoul.xls',
                          header=2,
                          usecols = 'B, D, G, J, N',
                          encoding='utf-8')

pop_Seoul.rename(columns={pop_Seoul.columns[0] : '구별',
                          pop_Seoul.columns[1] : '인구수',
                          pop_Seoul.columns[2] : '한국인',
                          pop_Seoul.columns[3] : '외국인',
                          pop_Seoul.columns[4] : '고령자'}, inplace=True)
pop_Seoul.drop([0], inplace=True)
pop_Seoul['구별'].unique()
pop_Seoul.drop([26], inplace=True)
pop_Seoul.head()

CCTV_Seoul['최근증가율'] = (CCTV_Seoul['2016년'] +  CCTV_Seoul['2015년'] + \
                            CCTV_Seoul['2014년']) / CCTV_Seoul['2013년도 이전'] * 100
CCTV_Seoul.sort_values(by='최근증가율', ascending=False).head(5)


pop_Seoul['외국인비율'] = pop_Seoul['외국인'] / pop_Seoul['인구수'] * 100
pop_Seoul['고령자비율'] = pop_Seoul['고령자'] / pop_Seoul['인구수'] * 100
pop_Seoul.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>구별</th>
      <th>인구수</th>
      <th>한국인</th>
      <th>외국인</th>
      <th>고령자</th>
      <th>외국인비율</th>
      <th>고령자비율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>종로구</td>
      <td>162820.0</td>
      <td>153589.0</td>
      <td>9231.0</td>
      <td>25425.0</td>
      <td>5.669451</td>
      <td>15.615404</td>
    </tr>
    <tr>
      <th>2</th>
      <td>중구</td>
      <td>133240.0</td>
      <td>124312.0</td>
      <td>8928.0</td>
      <td>20764.0</td>
      <td>6.700690</td>
      <td>15.583909</td>
    </tr>
    <tr>
      <th>3</th>
      <td>용산구</td>
      <td>244203.0</td>
      <td>229456.0</td>
      <td>14747.0</td>
      <td>36231.0</td>
      <td>6.038828</td>
      <td>14.836427</td>
    </tr>
    <tr>
      <th>4</th>
      <td>성동구</td>
      <td>311244.0</td>
      <td>303380.0</td>
      <td>7864.0</td>
      <td>39997.0</td>
      <td>2.526635</td>
      <td>12.850689</td>
    </tr>
    <tr>
      <th>5</th>
      <td>광진구</td>
      <td>372164.0</td>
      <td>357211.0</td>
      <td>14953.0</td>
      <td>42214.0</td>
      <td>4.017852</td>
      <td>11.342849</td>
    </tr>
  </tbody>
</table>
</div>




```python
import platform

from matplotlib import font_manager, rc
plt.rcParams['axes.unicode_minus'] = False

if platform.system() == 'Darwin':
    rc('font', family ='AppleGothic')
elif platform.system() == 'Windows':
    path = "c:/Windows/Fonts/malgun.ttf"
    font_name = font_manager.FontProperties(fname=path).get_name()
    rc('font', family=font_name)
else:
    print("Unknown system...  sorry~~~")

```

    Unknown system...  sorry~~~



```python
data_result = pd.merge(CCTV_Seoul, pop_Seoul, on = '구별')
data_result.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>구별</th>
      <th>소계</th>
      <th>2013년도 이전</th>
      <th>2014년</th>
      <th>2015년</th>
      <th>2016년</th>
      <th>최근증가율</th>
      <th>인구수</th>
      <th>한국인</th>
      <th>외국인</th>
      <th>고령자</th>
      <th>외국인비율</th>
      <th>고령자비율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구</td>
      <td>2780</td>
      <td>1292</td>
      <td>430</td>
      <td>584</td>
      <td>932</td>
      <td>150.619195</td>
      <td>570500.0</td>
      <td>565550.0</td>
      <td>4950.0</td>
      <td>63167.0</td>
      <td>0.867660</td>
      <td>11.072217</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강동구</td>
      <td>773</td>
      <td>379</td>
      <td>99</td>
      <td>155</td>
      <td>377</td>
      <td>166.490765</td>
      <td>453233.0</td>
      <td>449019.0</td>
      <td>4214.0</td>
      <td>54622.0</td>
      <td>0.929765</td>
      <td>12.051638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강북구</td>
      <td>748</td>
      <td>369</td>
      <td>120</td>
      <td>138</td>
      <td>204</td>
      <td>125.203252</td>
      <td>330192.0</td>
      <td>326686.0</td>
      <td>3506.0</td>
      <td>54813.0</td>
      <td>1.061806</td>
      <td>16.600342</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강서구</td>
      <td>884</td>
      <td>388</td>
      <td>258</td>
      <td>184</td>
      <td>81</td>
      <td>134.793814</td>
      <td>603772.0</td>
      <td>597248.0</td>
      <td>6524.0</td>
      <td>72548.0</td>
      <td>1.080540</td>
      <td>12.015794</td>
    </tr>
    <tr>
      <th>4</th>
      <td>관악구</td>
      <td>1496</td>
      <td>846</td>
      <td>260</td>
      <td>390</td>
      <td>613</td>
      <td>149.290780</td>
      <td>525515.0</td>
      <td>507203.0</td>
      <td>18312.0</td>
      <td>68082.0</td>
      <td>3.484582</td>
      <td>12.955291</td>
    </tr>
  </tbody>
</table>
</div>




```python
del data_result['2013년도 이전']
del data_result['2014년']
del data_result['2015년']
del data_result['2016년']
data_result.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>구별</th>
      <th>소계</th>
      <th>최근증가율</th>
      <th>인구수</th>
      <th>한국인</th>
      <th>외국인</th>
      <th>고령자</th>
      <th>외국인비율</th>
      <th>고령자비율</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구</td>
      <td>2780</td>
      <td>150.619195</td>
      <td>570500.0</td>
      <td>565550.0</td>
      <td>4950.0</td>
      <td>63167.0</td>
      <td>0.867660</td>
      <td>11.072217</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강동구</td>
      <td>773</td>
      <td>166.490765</td>
      <td>453233.0</td>
      <td>449019.0</td>
      <td>4214.0</td>
      <td>54622.0</td>
      <td>0.929765</td>
      <td>12.051638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강북구</td>
      <td>748</td>
      <td>125.203252</td>
      <td>330192.0</td>
      <td>326686.0</td>
      <td>3506.0</td>
      <td>54813.0</td>
      <td>1.061806</td>
      <td>16.600342</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강서구</td>
      <td>884</td>
      <td>134.793814</td>
      <td>603772.0</td>
      <td>597248.0</td>
      <td>6524.0</td>
      <td>72548.0</td>
      <td>1.080540</td>
      <td>12.015794</td>
    </tr>
    <tr>
      <th>4</th>
      <td>관악구</td>
      <td>1496</td>
      <td>149.290780</td>
      <td>525515.0</td>
      <td>507203.0</td>
      <td>18312.0</td>
      <td>68082.0</td>
      <td>3.484582</td>
      <td>12.955291</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_result.set_index('구별', inplace=True)
data_result.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>소계</th>
      <th>최근증가율</th>
      <th>인구수</th>
      <th>한국인</th>
      <th>외국인</th>
      <th>고령자</th>
      <th>외국인비율</th>
      <th>고령자비율</th>
    </tr>
    <tr>
      <th>구별</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>강남구</th>
      <td>2780</td>
      <td>150.619195</td>
      <td>570500.0</td>
      <td>565550.0</td>
      <td>4950.0</td>
      <td>63167.0</td>
      <td>0.867660</td>
      <td>11.072217</td>
    </tr>
    <tr>
      <th>강동구</th>
      <td>773</td>
      <td>166.490765</td>
      <td>453233.0</td>
      <td>449019.0</td>
      <td>4214.0</td>
      <td>54622.0</td>
      <td>0.929765</td>
      <td>12.051638</td>
    </tr>
    <tr>
      <th>강북구</th>
      <td>748</td>
      <td>125.203252</td>
      <td>330192.0</td>
      <td>326686.0</td>
      <td>3506.0</td>
      <td>54813.0</td>
      <td>1.061806</td>
      <td>16.600342</td>
    </tr>
    <tr>
      <th>강서구</th>
      <td>884</td>
      <td>134.793814</td>
      <td>603772.0</td>
      <td>597248.0</td>
      <td>6524.0</td>
      <td>72548.0</td>
      <td>1.080540</td>
      <td>12.015794</td>
    </tr>
    <tr>
      <th>관악구</th>
      <td>1496</td>
      <td>149.290780</td>
      <td>525515.0</td>
      <td>507203.0</td>
      <td>18312.0</td>
      <td>68082.0</td>
      <td>3.484582</td>
      <td>12.955291</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_result['소계'].sort_values().plot(kind='barh', grid=True, figsize=(10,10))
plt.show()
```


![png]({{"/images/output_6_0.png"}})



```python
data_result['CCTV비율'] = data_result['소계'] / data_result['인구수'] * 100
data_result['CCTV비율'].sort_values().plot(kind='barh', grid=True, figsize=(10,10))
plt.show()
```


![png]({{"/images/output_7_0.png"}})



```python
plt.figure(figsize=(6,6))
plt.scatter(data_result['인구수'], data_result['소계'], s=50)
plt.xlabel('인구수')
plt.ylabel('CCTV')
plt.grid()
plt.show()
```


![png]({{"/images/output_8_0.png"}})



```python
fp1 = np.polyfit(data_result['인구수'], data_result['소계'], 1)
fp1
```




    array([1.30916415e-03, 6.45066497e+02])




```python
f1 = np.poly1d(fp1)
fx = np.linspace(100000, 700000, 100)
```


```python
plt.figure(figsize=(6,6))
plt.scatter(data_result['인구수'], data_result['소계'], s=50)
plt.plot(fx, f1(fx), ls='dashed', lw=3, color='g')
plt.xlabel('인구수')
plt.ylabel('CCTV')
plt.grid()
plt.show()
```


![png]({{"output_11_0.png"}})



```python
fp1 = np.polyfit(data_result['인구수'], data_result['소계'], 1)

f1 = np.poly1d(fp1)
fx = np.linspace(100000, 700000, 100)

data_result['오차'] = np.abs(data_result['소계'] - f1(data_result['인구수']))

df_sort = data_result.sort_values(by='오차', ascending=False)
df_sort.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>소계</th>
      <th>최근증가율</th>
      <th>인구수</th>
      <th>한국인</th>
      <th>외국인</th>
      <th>고령자</th>
      <th>외국인비율</th>
      <th>고령자비율</th>
      <th>CCTV비율</th>
      <th>오차</th>
    </tr>
    <tr>
      <th>구별</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>강남구</th>
      <td>2780</td>
      <td>150.619195</td>
      <td>570500.0</td>
      <td>565550.0</td>
      <td>4950.0</td>
      <td>63167.0</td>
      <td>0.867660</td>
      <td>11.072217</td>
      <td>0.487292</td>
      <td>1388.055355</td>
    </tr>
    <tr>
      <th>송파구</th>
      <td>618</td>
      <td>104.347826</td>
      <td>667483.0</td>
      <td>660584.0</td>
      <td>6899.0</td>
      <td>72506.0</td>
      <td>1.033584</td>
      <td>10.862599</td>
      <td>0.092587</td>
      <td>900.911312</td>
    </tr>
    <tr>
      <th>양천구</th>
      <td>2034</td>
      <td>34.671731</td>
      <td>479978.0</td>
      <td>475949.0</td>
      <td>4029.0</td>
      <td>52975.0</td>
      <td>0.839413</td>
      <td>11.036964</td>
      <td>0.423769</td>
      <td>760.563512</td>
    </tr>
    <tr>
      <th>서초구</th>
      <td>1930</td>
      <td>63.371266</td>
      <td>450310.0</td>
      <td>445994.0</td>
      <td>4316.0</td>
      <td>51733.0</td>
      <td>0.958451</td>
      <td>11.488308</td>
      <td>0.428594</td>
      <td>695.403794</td>
    </tr>
    <tr>
      <th>용산구</th>
      <td>1624</td>
      <td>53.216374</td>
      <td>244203.0</td>
      <td>229456.0</td>
      <td>14747.0</td>
      <td>36231.0</td>
      <td>6.038828</td>
      <td>14.836427</td>
      <td>0.665020</td>
      <td>659.231690</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sort['인구수'][0]*1.02
df_sort['소계'][0]*0.98

```




    2724.4




```python
plt.figure(figsize=(14,10))

plt.scatter(data_result['인구수'], data_result['소계'],
            c=data_result['오차'], s=50)
plt.plot(fx, f1(fx), ls='dashed', lw=3, color='g')

for n in range(10):
    plt.text(df_sort['인구수'][n]*1.000001, df_sort['소계'][n]*1.0000001, df_sort.index[n], fontsize=15)

plt.xlabel('인구수')
plt.ylabel('인구당비율')

plt.colorbar()
plt.grid()
plt.show()
```


![png]({{"/images/output_14_0.png"}})
