---
layout: single
title: logs while setup blog on github.io with Minimal mistake theme
tags: [blog, jekyll, minimal mistake]
time: 2017-06-06 13:42:39
---

Setup logs


들어가며
1. 유행은 좀 지났지만 어쨌든 개발자 나부랭이로써 github.io 에 개발블로그를 하나 만들어보고 싶었다. 
2. 회사 정책상 그간 github은 못썼지만, 이제 
쓰게 해준다니 열심히 써보자. 

준비
1. github.com 의 문서를 읽어보았다. 
2. github.io 블로그 만들기 따위로 검색

실행
1. github.com 에 블로그를 만들기 위해선 [username].github.io 라는 이름의 public repository 가 필요하다.  
- GitHub Pages 설명 https://pages.github.com/  
이 repository 의 Master branch 에 내용물을 올려놓으면 웹페이지로 동작한다

2. index.html 만 올려놓기엔 좀 그러니 제공되는 테마를 써보자.  
repository setting > GitHub Pages 항목을 보면 Theme chooser 라고 Jekyll theme 를 고를수 있다. 
그런데 들어가보면 theme 가 12 개 달랑 있다. 

    2-1 jekyll theme 라는 걸 지원한다. 
      그럼 jeykyll 이 뭔지 알아본다
      - Jekyll site : https://jekyllrb.com/    
      - Jekyll themes : http://jekyllthemes.org/

    2-2 minimal mistake theme 를 선택해보았다.
    - minimal mistake : https://mmistakes.github.io/minimal-mistakes/

    2-3 하라는 대로 따라한다. 참쉽죠? ~_~  
     ... 쉽긴 개뿔이.  
     10년만에 홈페이지를 건드리려니 모르는 용어투성이라 이해하기 어렵다.

    2-4 추가 compoenent 설정
    - 사이트 통계 : google universal 을 붙여보았다.
    - SEO :  short for search engine optimization 인듯. 필요없어보여 안했음.
    - comment : 여러가지 시스템이 있지만. 많이 쓰는거 같은 Disqus 를 적용했다. 
    - disqus : https://disqus.com/ 사이트 가입하고 short id 를 얻어서 적용하면 된다

3. jekylll 문서를 읽다보면, 각종 plugin 인이 github.io 에서는 안된다는 걸 알수 있다. 방법은 local 에서 빌드해서 넣든지, 아니면 다른 site 에서 만들어 넣든지. 보통 많이 쓰는 travis-ci.org 를 써서 연결해 보았다. 

    3-1 travis-ci 사이트에 가입하고, github.com 과 연결한다. github.io repository 에서 travis-ci 를 사용하도록 한다

    3-2 github.com 의 profile setting 페이지에서 Key 값을 가져다 travis 의 secure 값을 만들어낸다. 이유는 그렇게 안하면 key 값이 노출돼서 암호화가 필요하다.

    3-3 travis secure 를 만들려면 Local 에 실행파일을 설치해야 한다. repository 별로 secure 값이 다르므로, repository 를 재생성한다든지 하면 다시 만들어야 된다

    3-4 travis 세팅을 하고 나면 repository 에 파일을 올려야 하는데, source branch 를 만들어 업로드하고, repository setting의 Branch 항목에서 source 를 default 로 설정한다.  
    이렇게 하면 source 에 파일을 업로드하면, travis 가 이를 감지하고 build후 완성된 파일을 master 에 업로드한다

    3-5 _config.yml 의 travis 설정 항목

    {% highlight ruby %}  
        # Settings for deploy rake task  
        # Username and repo of Github repo, e.g.  
        # https://github.com/USERNAME/REPO.git  
        # username defaults to ENV['GIT_NAME'] used by Travis  
        # repo defaults to USERNAME.github.io  
        # Branch defaults to "source" for USERNAME.github.io  
        # or "master" otherwise  
        username: aska94  
        repo: aska94.github.io  
        source_branch: source  
        destination_brach: master  
        destination: ../gh-pages/         
    {% endhighlight %} 

    3-6 Rakefile 의 내용도 확인해본다

    {% highlight ruby %}  
        CONFIG = YAML.load(File.read('_config.yml'))  
        USERNAME = CONFIG["username"]  
        REPO = CONFIG["repo"]  
        SOURCE_BRANCH = CONFIG["source_branch"]  
        DESTINATION_BRANCH = CONFIG["destination_brach"]      
    {% endhighlight %}
