# REST API

* API 란? Application Programming Interface, 프로그램간 서로 정보를 교환 가능하도록 함.
* REST란? Representational State Transfer, 자원\(Resource\) 의 표현\(Representation\) 에 의한 상태 전달
  * 자원, 행위, 표현
    * URI를 통해 자원\(Resource\)를 명시하고 Method\(POST, GET, PUT, DELETE\)를 통해 자원에 대한 행위를 적용
    * 자원은 JSON, XML, TEXT, RSS 등의 형태로 표현\(Representation\)
  * 특징
    * Stateless: context를 갖고있지 않는다. 각각의 요청을 개별적으로 인식하고 처리함
    * Cacheable: Last-Modified, E-Tag\)
    * 자체 표현
    * Client-Server 구조
  * Resource
    * Document: 문서, 하나의 객체, 레코드의 개념. 단수 명사. 소문자.
    * Collection: 문서들의 집합. 디렉토리의 라고도 함. 복수 명사
  * 규칙
    * 행위는 Method로 표현. URI에 Method 가 포함되면 안된다 .
    * 마지막 슬래시 포함하지 않음. 슬래시는 계층관계를 나타내는 데 사용되는 것이다.
    * 하이픈\(-\) 사용. 언더바\(\_\)는 사용하지 않는다.
    * 파일 확장자는 포함하지 않는다. Accept-Header를 사용한다.



* REST란? REST API란? RESTful이란? [https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
* REST API 제대로 알고 사용하기 [https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92)

## 그런 REST API로 괜찮은가 [https://slides.com/eungjun/rest](https://slides.com/eungjun/rest#/)

* 로이 필딩. MSresearch에서 발표하고 박사논문 씀
* REST API's must be hypertext-driven
* REST는 분산 하이퍼 미디어 시스템\(예: 웹\)을 위한 아키텍쳐 스타일\(제약 조건들의 집합\)
  * client-server, stateless, cache, _uniform interface_,\* layered system, code-on-demand \(optional\)
* uniform interface 의 제약 조건
  * identification of resources
  * manipulation of resources through representations
  * **self-descriptive messages ← 메세지가 스스로 설명해야 한다.**
    * Host, Content-Type: application/json-patch+json
    * HTTP 명세에 media type은 IANA에 등록되어있다고 하므로, IANA에서 application/json-patch+json의 설명을 찾는다.
    * 확장 가능한 커뮤니 케이션: 클라/ 서버가 변경되도 메세지 자체는 self descriptive 함으로 언제나 해석 가능함.
  * **hypermedia as the engine of application state \(HATEOAS\) ← 어플리케이션의 상태는 Hyperlink를 통해 전이 되어야 한다.**
    * Link
    * 애플리케이션 상태 전이의 late binding: 어디서 어디로 전이 가능한지는 미리 결정되지 않음. 어떤 상태로 전이가 완료되고 그다음 전이될 수 있는 상태가 결정. 즉 링크는 동적으로 변경될 수 있음.
* 독립적 진화를 위해서 uniform interface는 반드시 만족되어야한다.
  * 서버 기능이 변경되어도 클라이언트를 업데이트 할 필요가 없다.
  * Improve HTTP without breaking the Web
* REST가 웹에 준 영향
  * Host 헤더 추가
  * 길이제한 다루는 방법 명시\(414 URI Too Long\)
  * HTTP/1.1
* 그렇다면 우리가 말하는 REST API 는? REST API가 아니라 Resourceful API에 가까움
  * 웹페이지는 HTML, API는 JSON
  * JSON 은 Hyperlink 가 정의되어있지 않음. Self-descriptive도 불완전함. 별도 API 문서가 필요. key: value 에 대한 설명이 안됨

