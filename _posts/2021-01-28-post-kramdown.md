---
title: "Post:: kramdown 문법"
categories:
  - post
---

kramdown 문법 테스트

** 강조 **

이것은 헤더
===============
이것은 서브헤더
--------------
본문....


# H1 header
## H2 header
### H3 header
#### H4 header
##### H5 header
###### H6 header

이것은 *이텔릭*, **진하게**  
이것도 _이텔릭_, __진하게__

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

```
package me.kajundrama.demostreamingservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoStreamingServiceApplication {

  public static void main(String[] args) {
    SpringApplication.run(DemoStreamingServiceApplication.class, args);
  }

}
```
~~~ xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
~~~
~~~ java
package me.kajundrama.demostreamingservice;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoStreamingServiceApplication {

  public static void main(String[] args) {
    SpringApplication.run(DemoStreamingServiceApplication.class, args);
  }

}
~~~

순서 리스트2
1.  리스트 Item 1
    > blockquote와 함께
    # 헤더와 함께
{:.no_toc}    
2.  리스트 Item 2


순서없는 리스트2
* Item 1
+ Item 2
- Item 3

| 헤더1 | 헤더2 | 헤더3 |
|:--------|:-------:|--------:|
| 컬럼1   | 컬럼2   | 컬럼3   |
| 컬럼4   | 컬럼5   | 컬럼6   |
|----
| 컬럼1   | 컬럼2   | 컬럼3   |
| 컬럼4   | 컬럼5   | 컬럼6   |
|=====
| Foot1   | Foot2   | Foot3
{: rules="groups"}