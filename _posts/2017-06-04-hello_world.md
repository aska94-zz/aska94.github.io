---
title: Hello world!
layout: single
tags: [test, jekyll]
---

Test article. 

Log.

1. 한글확인
새글이 등록되지 않는 문제있음  
-> Timezone 이슈로 보임. 하루 전날 시간으로 마킹하면 올라감.  
jekyll 설명을 찾아보니 CC값이 아니라 TZ 값을 써야 함.   
난 한국이니까 Asia/Seoul 이면 될까?   
테스트필요함.  
    1-1. Asia/Seould 설정후에도 업데이트 시간은 변화없음.   
        파일 이름만 보고 있는것 같음.  
    1-2. post의 date를 override 해서 시간을 바꿀 수 있다고 함.   
    1-3. 편의를 위해 Visual Studio Code 에서 Insert Time String 을 설치함.   
        단축키는 Ctrl + Shift + I 
    1-4. Visual Studio Code 에서 미리보기사용하면 편함. 개행은 라인끝에 space 2개

2. 타이틀 문제  
FrontMatter에 넣은 타이틀이 이상하게 보임  
    2-1 첫줄에 --- 를 넣어야 하는듯  
    2-2 뭘 바꿨는지 모르겠는데, 파일이 삭제돼서 deploy됨  
    2-3 title 동작함
    2-4 tags 동작함. layout 을 single 로 해야 함. -> minimal mistake 테마 연구필요.  


{% highlight html %}  
Test2
 less than 1 minute read
layout: post title: Test 2nd writing. tags: jekyll blog test —

Hello_world
 less than 1 minute read  
{% endhighlight %}




3. 댓글 문제
댓글이 안보임.  