---
layout: single
title: jvm heap allocation error with android studio
tags: [java, android, studio]
time: 2017-06-12 14:42:39
---

개발중인 Android project 에 모 라이브러리를 추가하게 되면서, multidex 모드를 사용하게 되었다.  
없애고 싶지만. 일단은 하던걸 먼저 해야 하니깐.  

그런데 multidex 모드가 되면서 빌스시 메모리에러가 발생하는 경우가 자주 발생한다. 

물론 메모리는 충분하다. 

![Task Manager screenshot]({{ site.url }}/assets/2017-06-12-task-manager.PNG)

Available 9117 MB !!

에러 메세지

{% highlight gradle %}

Error occurred during initialization of VM
Could not reserve enough space for 3170304KB object heap
Java HotSpot(TM) Client VM warning: ignoring option MaxPermSize=512m; support was removed in 8.0

{% endhighlight %}

현재 jvm 옵션

org.gradle.jvmargs=-Xmx3096m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8

gradle jvmarg 를 넣을 수 있는 곳

- Project dir: {projectdir}/gradle.properties  
add org.gradle.jvmargs=-Xmx3096m 

- Global config:
{userdir}/.gradle/gradle.properties  
add org.gradle.jvmargs=-Xmx3096m 

- JAVA_OPTIONS:  
add JAVA_OPTIONS="-Xmx3096m"


-> 아무 효과가 없다. 어라? 

같은 증상의 글들을 검색해본 결과
32bit mode 에서는 오히려 값을 작게 가져가야 한다고 한다. 
64bit mode 에서는 정상동작해야 하는것이 정상임.

현재의 JVM 이 어떤 모드인지를 확인하기 위해선 커맨드창에 다음과 같이 입력한다.  
아래는 64bit JVM의 경우

{% highlight dos %}
> java -d64 -version
java version "1.8.0_131"
Java(TM) SE Runtime Environment (build 1.8.0_131-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)

{% endhighlight %}


확인시 어쩐일인지 32bit mode JVM 이 설치되어 있었다!  

64bit mode 로 바꾸고 모든 문제 해결됨.  :-(  

심지어 넣었던 jvm 값들을 다시 빼도 동작함 WTH... 


