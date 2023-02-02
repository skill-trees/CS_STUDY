## REST API

> REST : 웹 (HTTP) 의 장점을 활용한 아키텍쳐

### REST

> 즉 REST란
HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해
해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.
>

- REST의 특징
  - Server-Client(서버-클라이언트 구조)
  - Stateless(무상태)
  - Cacheable(캐시 처리 가능)
  - Layered System(계층화)
  - Uniform Interface(인터페이스 일관성)

### CRUD Operation

Create : 데이터 생성(POST)
Read : 데이터 조회(GET)
Update : 데이터 수정(PUT, PATCH)
Delete : 데이터 삭제(DELETE)


### Restful API


RESPT API란 REST의 원리를 따르는 API를 의미합니다.

하지만 REST API를 올바르게 설계하기 위해서는 지켜야 하는 몇가지 규칙이 있으며 해당 규칙을 알아 보겠습니다.

### REST API 설계 예시
1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.

```shell
Bad Example http://kkk98.com/Running/
Good Example  http://kkk98.com/run/
```


2. 마지막에 슬래시 (/)를 포함하지 않는다.
```shell
Bad Example http://kkk98.com/test/  
Good Example  http://kkk98.com/test
```

3. 언더바 대신 하이폰을 사용한다.
```shell
Bad Example http://kkk98.com/test_blog
Good Example  http://kkk98.com/test-blog
```

4. 파일확장자는 URI에 포함하지 않는다.
```shell
Bad Example http://kkk98.com/photo.jpg  
Good Example  http://kkk98.com/photo
```

5. 행위를 포함하지 않는다.
```shell
Bad Example http://kkk98.com/delete-post/1  
Good Example  http://kkk98.com/post/1  
```