---
title: "JS 이벤트루프란 무엇인가?"
date: 2019-06-08 20:21:28
categories: EventLoop JavaScript
---

{% include video id="8aGhZQkoFbQ" provider="youtube" %}

세줄요약
1. 이벤트루프EventLoop(와 Web API, AJAX, DOM, 콜백큐 등)는 JS Runtime의 일부가 아니다. 이들은 Browser(nodejs에서는 libuv)가 제공해주는 것이다.
2. 일반 함수는 호출되면 콜스택Call Stack에 쌓였다가 실행이 끝나면 pop된다.
3. Web APIs(AJAX, Timer 등)를 사용하는 결과값이 바로 나오지 않는 것들은 실행이 끝나면, 작업큐(Task Queue)에 콜백 함수를 올려 놓고, **콜스택이 비었을 때** 이벤트루프가 작업큐의 함수들을 콜스택에 넣어준다.  
