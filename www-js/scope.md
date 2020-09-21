# Scope

* 자바스크립트\(ES6\)는 함수 레벨과 블록 레벨의 렉시컬 스코프규칙을 따른다.
* 스코프 레벨
  * 함수레벨 스코프 - var 혹은 함수 선언식으로 만들어진 함수
  * 블록레벨 스코프 - let, const
    * ES6 부터 블록레벨 스코프를 지원한다.
  * 렉시컬 스코프 - 소스코드가 작성된 문맥에서 결정됨. 현대 프로그래밍에서 대부분은 렉시컬 스코프
  * 동적 스코프 - 프로그램 런타임 도중의 실행컨텍스트나 호출 컨텍스트에 의해 결정됨.
    * JS는 호출 스택과 관계 없이 런타임에 변경시키지 않음. eval, with으로 가능하긴 하지만 비권장
  * 중첩 스코프\(스코프 체인 혹은 스코프 버블\)
    * ECMA 명세에서는 Lexical environment, Environment Record 라는 개념으로 정의됨

자바스크립트의 스코프와 클로저 [https://meetup.toast.com/posts/86](https://meetup.toast.com/posts/86)
