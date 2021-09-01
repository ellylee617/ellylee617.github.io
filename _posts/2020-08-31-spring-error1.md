---
layout: single

title: "[Spring] 오류 - exception is java.lang.IllegalArgumentException: Pointcut is not well-formed"

date: 2021-08-31
lastmod: 2021-08-31

author_profile: true

categories: 
  - test post

tags: 
    - Spring
    - error
---


<br>

### AOP 설정 관련 오류

<br>


```java
Error creating bean with name 'org.springframework.transaction.annotation.AnnotationTransactionAttributeSource#0': Initialization of bean failed; nested exception is java.lang.IllegalArgumentException: Pointcut is not well-formed: expecting 'name pattern' at character position 38
execution(*com.project.first..*Impl.*(..)))
                                      ^
```


<br><br>
root-context.xml 파일에서 transaction을 위한 aop pointcut 설정을 하였는데
<br>

```java
<aop:config proxy-target-class="true">
		<aop:pointcut id="txPointcut" expression="execution(*com.project.first..*Impl.*(..)))" />
		<aop:advisor id="transactionAdvisor" pointcut-ref="txPointcut" advice-ref="txAdvice" />
</aop:config>
```

expression을 잘못 작성하여 오류가 발생한 경우다.


<br><br>
"execution(\*com.project.first.\*Impl.*(..))"

⇒ **"execution(* com.project.first.\*Impl.\*(..))"**

<br>

- 모든 리턴 타입(*****) 

- com.project.first 패키지 및 하위 패키지에 속한(com.project.first) Impl로 끝나는(\*Impl) 클래스의 파라미터가 0개 이상(..)인 메서드(*(..)) 

<br>

>"execution([리턴타입] [타겟메소드지정(argument타입)])"의 형태이므로
>
>
>[리턴타입] [메소드] 사이에 **띄어쓰기** 꼭!

<br><br><br><br><br>
