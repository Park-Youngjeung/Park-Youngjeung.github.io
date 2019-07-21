---
layout: post
title:  "파이썬 데이터 다루기"
date:   2019-07-21 16:00:00
---



# 파이썬 데이터 다루기 - 판다스로 엑셀 파일 다루기

"파이썬 데이터 분석 입문"이라는 책으로 파이썬을 공부하고 있는데, 몇 가지 예제를 다루는 중에 기록하고 싶은 것이 있다.

예제는 CSV파일과 엑셀 파일이 여러가지 있을 때 중복되는 되는 내용을 찾아 CSV 파일에 저장하는 내용이다.

책에서는 엑셀 파일을 열어서 데이터를 입력하고, 이를 파이썬 스크립트에서 읽어와서 처리하는 방식인데, 엑셀 파일 자체를 pandas를 이용해서 만드는 과정부터 시작했다.

관련된 csv 파일과 excel 파일은 깃허브에 있으며 아래의 링크를 참조한다.

관련된 csv 파일과 excel 파일은 깃허브에 있으며 아래의 링크를 참조한다.

코드 및 파일 주소 :  [깃허브 주소](https://github.com/cbrownley/foundations-for-analytics-with-python)

우선 csv 파일은 입력을 해서 만들고, 이 csv 파일의 연도를 변경한 엑셀 파일로 만들었다. 아래가 코드 내용이다.

```python
import pandas as pd

data = pd.read_csv('supplies_2012.csv')
data[' Date'] = data[' Date'].str.replace('2012', '2013')
data.to_excel('supplies_2013.xls', index=None, sheet_name='supplies_2013')

```

csv 파일의 `Date`열에 `2012`를 `2013`으로 변경하고 이를 `supplies.xls`파일에 저장하고 sheet이름은 `supplies_2013`으로 지정했다.



문제는 다음인데, `2013`을 `2014`로 변경한 sheet를 새로 만들어서 같은 파일에 저장해야 하는데, 이를 잘 몰라서 한 참 헤멨다. 이글을 적고 있는 상태에서도 헤메고 있는 중이라 이렇게 기록을 남긴다.



```python

import pandas as pd

writer = pd.ExcelWriter('supplies.xls')
data_sheet2 = pd.read_excel('supplies_2013.xls')
data_sheet2[' Date'] = data_sheet1[' Date'].str.reaplce('2013', '2014')
data_sheet1 = pd.read_excel('supplies_2013.xls')
data_sheet1.to_excel(writer, 'supplies_2013')
data_sheet2.to_excel(writer, 'supplies_2014')
writer.save()
```

두 개의 sheet를 저장하기 위해서 `supplies_2013`파일을 두 번 읽어 들였다. 좀 더 좋은 방법이 있을 것 같은데, 아직까지는 더 생각하지 못 했다.

**중요한 것** 은 엑셀 파일을 쓰기 위해서는 **pandas의 ExcelWriter** 를 사용할 수 있다.
저장하는 방법은 **to_excel(writer, 'sheetname')** 으로 하면 된다.
마지막으로 **writer.save()** 를 해 준다.

이렇게 해결은 했지만, 파일을 읽어들이면서 인덱스가 열에 추가되었다.

파일 읽을 때 인덱스를 제거하는 옵션은 `index=False`이다.
