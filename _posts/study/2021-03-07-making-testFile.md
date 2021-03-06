---
layout: post
title: '[GithubPages] 04.테스트하기'
subtitle: 커스텀하기
categories: study
tags: githubpage
comments: true
published: true
---
# 2020 0707.


1. 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 
	* [Chapter03 스프링 부트에서 JPA로 데이터베이스 다뤄보자](#chpater03)
2. Baekjoon
	* [배열](#array)

---

1.스프링 부트와 AWS로 혼자 구현하는 웹 서비스
----

### chpater03

### 스프링 부트에서 JPA로 데이터베이스 다뤄보자

1. _JPA_
	* __인터페이스로서 자바 표준명세서 입니다.__
	* 객체와 Table 사이의 mismatch를 없애 줌.
	* 하지만 Spring에서 JPA 사용시 이 구현체들을 직접 다루지는 않는다.
		*__ JPA <- Hibernate <- Spring Data JPA__

2. _Spring Data JPA_
	* Hibernate와 큰 차이는 없다
	* __그럼에도 한 단계 더 감싸놓은 이유는 2가지이다.__
		+ 구현체 교체의 용이성
		+ 저장소 교체의 용이성

3. _프로젝트에 Spring Data JPA 적용하기_
	* Spring-boot-starter-data-jpa
		+ 스프링 부트용 Spring Data Jpa 추상화 라이브러리
		+ 스프링 부트 버전에 맞춰 자동으로 JPA 관련 버전 관리
	* h2
		+ 인메모리 관계형데이터베이스
		+ __메모리에서 실행되기 때문에 app를 재시작할 때마다 초기화된다는 점을 이용하여 테스트 용도로 많이 쓰임__

* build.grable

```
compile('org.springframework.boot:spring-boot-starter-web')
compile('org.springframework.boot:spring-boot-starter-data-jpa')
compile('com.h2database:h2')
testCompile('org.springframework.boot:spring-boot-starter-test')
```

4. _TestCode 작성하기_

# PostsRepositoryTest.java

```
package com.jojoldu.Book.springboot.domain;

import com.jojoldu.Book.springboot.domain.posts.Posts;
import com.jojoldu.Book.springboot.domain.posts.PostsRepository;
import org.junit.After;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import java.util.List;

import static org.assertj.core.api.Assertions.assertThat;

@RunWith(SpringRunner.class)
@SpringBootTest
public class PostsRepositoryTest {

    @Autowired
    PostsRepository postsRepository;

    @After
    public void cleanup(){
        postsRepository.deleteAll();
    }
    // 단위 테스트가 끝날 때 마다 실행되는 메소드를 지정
    // 테스트간 데이터 침범을 막기 위한 용도 

    @Test
    public void 게시글저장_불러오기(){
        //given
        String title = "테스트 게시글";
        String content = "테스트 본문";
	
        postsRepository.save(Posts.builder()
                .title(title)
                .content(content)
                .author("chosunz4@naver.com")
                .build());
        //when
        List<Posts> postsList = postsRepository.findAll();

        //then
        Posts posts = postsList.get(0);
        assertThat(posts.getTitle()).isEqualTo(title);
        assertThat(posts.getContent()).isEqualTo(content);
    }
}

```

5. _Annonation_
	* `@After`
		+ Junit 단위 테스트가 끝날 때마다 수행되는 메소드
		+ 테스트간의 데이터 침범을 막기 위해 시전

6. _JPARepository_
	* __interface 이다.__
	* 미리 검색 메소드를 정의 해 두는 것으로
	* __이를 상속받은 class는 메소드를 호출하는 것만으로 데이터 검색을 할 수 있게 되는 것이다.__

---

1.Baekjoon
----

### array

### 1차원 배열

# 특별히 어려운 문제는 없었다.

1. 주의할 점
	* doulbe 과 int의 나누기 연산 주의하기
	* double형태를 반올림으로 출력 할 때 : String.format("%3.f", result);
	* 문자열 함수 subString( start, end) : start부터 end까지의 문자열을 뽑아준다.
	* __출력 모양을 잘 보고 제출해야 한번에 통과한다.__

![1차원배열](https://user-images.githubusercontent.com/52272332/86914826-e9633880-c15b-11ea-9453-303dcbd2c5d1.JPG)
