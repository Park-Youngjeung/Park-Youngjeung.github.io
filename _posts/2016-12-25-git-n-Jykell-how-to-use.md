---
layout: post
title:  "git으로 post 등록하기"
date:   2016-12-25 19:26:00
---

Jykell을 통해서 Git으로 post를 등록하는 절차

다른 사람들의 블로그를 통해서 확인했는데, 잊어 버릴 것 같아서 여기 적어 놓는다.


먼저 git에 추가 및 수정할 내용의 파일을 알려준다.

> git add "파일 이름" or git add . ("."은 모든 파일을 의미한다.)

그리고, 추가 및 수정된 내용을 확정해 준다.

> git commit -m "메시지"   메시지는 변경된 내용에 대한 코멘트이다.

최종적으로 확정된 내용을 git의 master로 내용을 전달한다. (난 현재 블로그를 master로 사용하고 있다.)

> git push origin master  origin을 설정하고 git 작업을 할 폴더를 알려주는 작업이 사전에 필요하다.
> (여기서는 생략한다.)

참고한 블로그들....
[Jekyll 공식 홈페이지(한글)][http://jekyllrb-ko.github.io/]
