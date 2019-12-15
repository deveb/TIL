---
description: 'https://asfirstalways.tistory.com/362'
---

# Event Loop

* JS Engine은 인터프리터이다. 서버 사이드에선 V8
  * 엔진은 세가지 영역으로 나뉨. Call Stack, Task Queue\(Event queue\), Heap
  * 그리고 추가적으로 Event Loop
* Call Stack
  * JS는 단 하나의 호출 스택을 사용함. 이런 특징으로 함수가 실행되는 방식을 "Run to Completion" 이라고 함. 하나의 함수가 실행되면 끝날 때 까지 어떤 task도 수행될수 없다. 순차적으로 호출스택에 담아 처리.
* Heap
  * 동적으로 생성된 객체는 힙에 할당됨. 구조화 되지 않은 더미 메모리 영역
* Task Queue\(JS의 이벤트 루프\)
  * 처리해야하는 Task들을 임시 저장하는 대기 큐. Call Stack이 비었을 때 먼저 들어온 순서대로 수행. 비동기로 호출되는 함수들은 Call Stack에 쌓이지 않고 여기에 enqueue됨. 이벤트 핸들러, JS Engine이 아닌 Web API영역에 정의된 함수들 등
  * Event Loop 는 현재 실행중인 태스크가 없는지 태스크 큐에 태스크가 있는지 반복적으로 확인. Task Queue에서 대기하고있다가 Call Stack으로 호출되어 처리됨.
  * Web API: setTimeout, requestAnimationFrame, Promise 등등
    * Microtask Queue → Animation frames → Task Queue

