---

layout: single

title: "[Spring] 오류 - org.apache.ibatis.builder.BuilderException: Mapper's namespace cannot be empty"
excerpt: "mapper에 namespace를 작성하지 않은 오류"

date: 2021-08-31
lastmod: 2021-08-31

author_profile: ture

categories: 
  - Spring

tags: 
   - Spring
   - error

---

<br>

### Mapper에 namespace를 작성하지 않은 오류

<br><br>

```java
Caused by: org.apache.ibatis.builder.BuilderException: Error parsing SQL Mapper Configuration. 
Cause: org.apache.ibatis.builder.BuilderException: Error parsing Mapper XML. 
Cause: org.apache.ibatis.builder.BuilderException: Mapper's namespace cannot be empty
```

<br><br>

해당 오류는 해당 에러메시지 말그대로 mapper의 namespace가 없어서 나는 에러.

<br>

내 경우엔 프로젝트 초기 작업으로 필요한 파일들을 미리 만들었는데

그 중엔 당연히 mapper.xml도 여러개 있었다.

그리고 야무지게 mybatis-config.xml에 만든 모든 mapper.xml들을 다 등록했다.

당장 필요하지 않은 파일은 생성만 해두고 신경쓰지 않았다가 이런 오류를 만났다.

<br>

> 해결방법으로는 
>
> 1. <strong>mapper.xml을 미리 만든다면 mybatis-config.xml에 등록하지 말 것</strong>
> 2. <strong>mapper.xml을 미리 만들고 mybatis-config.xml에 등록한 mapper.xml은 꼭 namespace 작성해주기</strong>

<br>

톰캣 구동이 되지 않으니 당황할 스프링 초보들을 위하여.(포 미)

<br><br><br><br><br>
