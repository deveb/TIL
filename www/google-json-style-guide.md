# Google JSON Style Guide

[https://google.github.io/styleguide/jsoncstyleguide.xml](https://google.github.io/styleguide/jsoncstyleguide.xml)

JSON API는 [JSON.org](https://www.json.org/json-ko.html) 따라야 함. 이 가이드라인은 RPC-based, REST-based API에 적용가능함.

* 정의: name, value 모두 property 이다. number는 JS number\(float 포함\)를 의미하고 integer는 integer이다.

  ```text
    {
      // The name/value pair together is a "property".
      "propertyName": "propertyValue"
    }
  ```

* 일반적인 가이드 라인
  * 주석은 없어야함.
  * 쌍 따옴표를 사용한다. bool, number 제외
  * 편의를 위해 임의로 그룹지으면 안된다. Flattened data여야 함. Structured Hierarchy 사용해야 하면 잘 고려해서 sementic sense 가 맞을 떄만 사용해라.
  * 들여쓰기는 의미가 없다.
* Property name 가이드 라인
  * property name 포맷
    * 의미 있는 이름 지어라.
    * camelCase이고 ascii 문자열이어야 한다.
    * 첫 문자는 letter, underscore, $ 이어야 함. 그 이후의 문자들은 letter, digit, \_, $
    * JS 예약어는 피해라
  * JSON Maps 에서 Key 이름
    * JSON object 가 map으로 사용되면 property name 포맷 규칙은 적용되지 않는다.
    * 아무 unicode 가능
  * 예약어 property name
    * 아래 내용에 목록이 있다.
  * 단수 vs 복수
    * 배열은 복수여야함. 그외는 다 단수. `itemCount` , `totalItems` 는 `total` 이 일반적.
  * Naming 충돌 피해라
    * 새 이름으로 하던지 버저닝 해라
* Property value 가이드 라인
  * property value 포맷
    * [JSON.org](https://www.json.org/json-ko.html) 따르면 Unicode, booleans, numbers, strings, objects, arrays, or `null` 허용
    * Empty/Null 은 없는게 좋다.
      * 강력한 이유가 없다면 optional은 아예 보내지 말자.
    * Enum은 문자열로 표현되어야 한다.
* Property Value Data Types
  * Property Value 가이드라인에 따르면 Unicode, booleans, numbers, strings, objects, arrays, or `null` 여야 하지만 특정 값들을 다룰 때standard data types를 정의하면 편리하다. data types는 항상 문자열이어야 라지만 특정 포맷으로 쉽게 파싱 할수 있을 것이다.
  * 날짜 속성: [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) `2018-06-08T23:46:11-05:00`
  * 시간 간격: [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Durations) `P3Y6M4DT12H30M5S`
  * 위도 및 경도값: [ISO6709](https://en.wikipedia.org/wiki/ISO_6709) `40.748747-73.985547` 위도 먼저, 북위가 양수, 동경이 양수, 음수 기호이므로 문자열로 나타냄
  * JSON object는 아래 가이드를 따른다. request/response 모두 동일하다.
  * 이 구조에서는 특정용도의 예약어가 있다. 이는 권장일 뿐 필수가 아니다.
* Property 순서
  * `kind` 는 첫번째
  * `items` 는 data object의 마지막

    { "data": { "kind": "album", "title": "My Photo Album", "description": "An album in the user's account", "items": \[ { "kind": "photo", "title": "My First Photo" } \] } }
* 예시
  * YouTubeJSON API

    { "apiVersion": "2.0", "data": { "updated": "2010-02-04T19:29:54.001Z", "totalItems": 6741, "startIndex": 1, "itemsPerPage": 1, "items": \[ { "id": "BGODurRfVv4", "uploaded": "2009-11-17T20:10:06.000Z", "updated": "2010-02-04T06:25:57.000Z", "uploader": "docchat", "category": "Animals", "title": "From service dog to SURFice dog", "description": "Surf dog Ricochets inspirational video ...", "tags": \[ "Surf dog", "dog surfing", "dog", "golden retriever", \], "thumbnail": { "default": "[https://i.ytimg.com/vi/BGODurRfVv4/default.jpg](https://i.ytimg.com/vi/BGODurRfVv4/default.jpg)", "hqDefault": "[https://i.ytimg.com/vi/BGODurRfVv4/hqdefault.jpg](https://i.ytimg.com/vi/BGODurRfVv4/hqdefault.jpg)" }, "player": { "default": "[https://www.youtube.com/watch?v=BGODurRfVv4&feature=youtube\_gdata](https://www.youtube.com/watch?v=BGODurRfVv4&feature=youtube_gdata)", "mobile": "[https://m.youtube.com/details?v=BGODurRfVv4](https://m.youtube.com/details?v=BGODurRfVv4)" }, "content": { "1": "rtsp://v5.cache6.c.youtube.com/CiILENy73wIaGQn-Vl-0uoNjBBMYDSANFEgGUgZ2aWRlb3MM/0/0/0/video.3gp", "5": "[https://www.youtube.com/v/BGODurRfVv4?f=videos&app=youtube\_gdata](https://www.youtube.com/v/BGODurRfVv4?f=videos&app=youtube_gdata)", "6": "rtsp://v7.cache7.c.youtube.com/CiILENy73wIaGQn-Vl-0uoNjBBMYESARFEgGUgZ2aWRlb3MM/0/0/0/video.3gp" }, "duration": 315, "rating": 4.96, "ratingCount": 2043, "viewCount": 1781691, "favoriteCount": 3363, "commentCount": 1007, "commentsAllowed": true } \] } }

  * Paging

    \`{ "apiVersion": "2.1", "id": "1", "data": { "query": "chicago style pizza", "time": "0.1", "currentItemCount": 10, "itemsPerPage": 10, "startIndex": 11, "totalItems": 2700000, "nextLink": "[https://www.google.com/search?hl=en&q=chicago+style+pizza&start=20&sa=N](https://www.google.com/search?hl=en&q=chicago+style+pizza&start=20&sa=N)" "previousLink": "[https://www.google.com/search?hl=en&q=chicago+style+pizza&start=0&sa=N](https://www.google.com/search?hl=en&q=chicago+style+pizza&start=0&sa=N)", "pagingLinkTemplate": "[https://www.google.com/search/hl=en&q=chicago+style+pizza&start={index}&sa=N](https://www.google.com/search/hl=en&q=chicago+style+pizza&start=%7Bindex%7D&sa=N)", "items": \[ { "title": "Pizz'a Chicago Home Page" // More fields for the search results } // More search results \] } }
* JSON 구조와 예약된 Property Names

  ```text
    object {
      string apiVersion?;
      string context?;
      string id?;
      string method?;
      object {
        string id?
      }* params?;
      object {
        string kind?;
        string fields?;
        string etag?;
        string id?;
        string lang?;
        string updated?; # date formatted RFC 3339
        boolean deleted?;
        integer currentItemCount?;
        integer itemsPerPage?;
        integer startIndex?;
        integer totalItems?;
        integer pageIndex?;
        integer totalPages?;
        string pageLinkTemplate /^https?:/ ?;
        object {}* next?;
        string nextLink?;
        object {}* previous?;
        string previousLink?;
        object {}* self?;
        string selfLink?;
        object {}* edit?;
        string editLink?;
        array [
          object {}*;
        ] items?;
      }* data?;
      object {
        integer code?;
        string message?;
        array [
          object {
            string domain?;
            string reason?;
            string message?;
            string location?;
            string locationType?;
            string extendedHelp?;
            string sendReport?;
          }*;
        ] errors?;
      }* error?;
    }*;
  ```

* 최상위 예약어 Property Names
  * apiVersion
  * context
  * id
  * method
  * params
  * data
  * error
* data object에서 예약된 Property Names
  * data.kind
  * data.fields
  * data.etag
  * [data.id](http://data.id)
  * data.lang
  * data.updated
  * data.deleted
  * data.items
* 페이징을 위해 예약된 Property Names
  * data.currentItemCount
  * data.itemsPerPage
  * data.startIndex
  * data.totalItems
  * data.pagingLinkTemplate
  * data.pageIndex
  * data.totalPages
* Link를 위해 예약된 Property Names
  * data.self / data.selfLink
  * data.edit / data.editLink
  * data.next / data.nextLink
  * data.previous / data.previousLink
* error object에 쓰이는 예약된 Property Names
  * error.code
  * error.message
  * error.errors
  * error.errors\[\].domain
  * error.errors\[\].reason
  * error.errors\[\].message
  * error.errors\[\].location
  * error.errors\[\].locationType
  * error.errors\[\].extendedHelp
  * error.errors\[\].sendReport
* JS 예약어

  From the [ECMAScript Language Specification 5th Edition](http://www.ecma-international.org/publications/standards/Ecma-262.htm)

  ```text
    abstract
    boolean break byte
    case catch char class const continue
    debugger default delete do double
    else enum export extends
    false final finally float for function
    goto
    if implements import in instanceof int interface
    let long
    native new null
    package private protected public
    return
    short static super switch synchronized
    this throw throws transient true try typeof
    var volatile void
    while with
    yield
  ```



