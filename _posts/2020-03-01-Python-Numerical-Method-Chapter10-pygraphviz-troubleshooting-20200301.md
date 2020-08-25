---
layout: post
title:  파이썬 pygraphviz 라이브러1 구글 Colab에서 사용하기
date:   2020-03-01 01:10:00
---


"파이썬 수치해석"이라는 책의 희소 행렬과 그래프에서 도쿄의 지하철을 Networkx 라이브러리를 이용해서 시각화하는 코드가 있다.

구글 Colab에서 실행하려고 하니 pygraphviz가 임포트되지 않아 에러가 발생했다.
!pip install pygraphviz로 설치하려고 하니 설치가 되지 않는 문제가 있다.

구들 검색을 해서 보니 아래의 코드로 가능하보았다

~~~
# pygraphviz
!wget https://anaconda.org/anaconda/pygraphviz/1.3/download/linux-64/pygraphviz-1.3-py36h14c3975_1.tar.bz2
!tar xvjf pygraphviz-1.3-py36h14c3975_1.tar.bz2
!cp -r lib/python3.6/site-packages/* /usr/local/lib/python3.6/dist-packages/

import pygraphviz
~~~

검색 출처 : https://gist.github.com/korakot/d0a49d7280bd3fb856ae6517bfe8da7a
