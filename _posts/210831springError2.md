---

layout: single

title: "[Spring] 오류 - org.apache.ibatis.builder.BuilderException: Mapper's namespace cannot be empty"
excerpt: "Mybatis 연동 설정 오류"

date: 2021-08-31 
lastmod: 2021-08-31 

author_profile: true

categories: 
  - Spring

tags: 
   - Spring
   - error

---

<br>

### Mybatis 연동 설정 오류

<br><br>

```java
Error parsing SQL Mapper Configuration. 
Cause: org.apache.ibatis.builder.BuilderException: Error parsing Mapper XML. 
Cause: org.apache.ibatis.builder.BuilderException: Mapper's namespace cannot be empty
```

<br><br>

root-context.xml 파일에서 Mybatis 연동을 위한 설정을 하였는데

```java
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dataSource" />
	<property name="configLocation" value="classpath:mybatis-config.xml" />
	<property name="mapperLocations" value="classpath:mappers/**/*Maper.xml"/>
</bean>
```

ㅎㅎ.. 야무진 오타로 인한 오류가 발생한 경우다.

<br><br>

\<property name="mapperLocations" value="classpath:mappers/\*\*/*Maper.xml"/>

⇒ \<property name="mapperLocations" value="classpath:mappers/\*\*/***Mapper**.xml"/>

<br>

단순 오타고 에러메시지에서도 아주 친절하게 설명해주는 오류지만

그럼에도 검색이 필요할 나와 같은 초보 개발자를 위하여 기록해두기

<br>

<br>

<br>

<br>

<br>
