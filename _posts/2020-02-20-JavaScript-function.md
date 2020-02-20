---
title: "자바스크립트 함수"
toc: true
toc_sticky: true
date: 2020-02-20 12:39:20 -0400
categories: JavaScript
tag:
  - JavaScript
  - Function
---

## 함수란?

함수(function)란 하나의 특별한 목적의 작업을 수행하도록 설계된 독립적인 블록을 의미.  
필요할 때마다 호출하여 작업을 반복 수행 가능.

```javascript
function addNum(x, y) {
  return x + y;
}

document.write(addNum(2, 3));
```

> 자바스크립트에서는 함수도 **하나의 타입(datatype)**.

## 변수의 유효 범위 (variable scope)

자바스크립트에서 객체나 함수는 모두 변수(variable)이다.

변수의 유효 범위(scope)란 해당 변수가 접근할 수 있는 변수, 객체 그리고 함수의 집합을 의미.

두가지로 분류

1. 지역 변수 (local variable)
2. 전역 변수 (global variable)

### 지역 변수 (local variable)

함수 내에서 선언된 변수.

변수가 선언된 함수 내에서만 유효.

함수가 종료되면 메모리에서 사라진다.

```javascript
function localNum() {
  var num = 10; // 지역 변수 num에 숫자 10을 대입
  document.write(
    "함수 내부에서 변수 num의 타입은" + typeof num + "입니다.<br>"
  ); // number
}

localNum(); // 함수 localNum()을 호출
document.write(
  "함수의 호출이 끝난 뒤 변수 num의 타입은 " + typeof num + "입니다."
); // undefined
```

### 전역 변수 (global variable)

함수의 외부에서 선언된 변수.

프로그램의 어느 영역에서나 접근할 수 있다.

웹 페이지가 닫혀야만 메모리에서 사라진다.

```javascript
var num = 10; // 전역 변수 num을 선언함과 동시에 10을 대입

function gloabalNum() {
  document.write("함수 내부에서 변수 num의 값은 " + num + "입니다.<br>"); // 10
  num = 20; // 전역 변수 num의 값을 함수 내부에서 변경
}

globalNum(); // 함수 globalNum()을 호출함.
document.write("함수의 호출이 끝난 뒤 변수 num의 값은" + num + "입니다."); // 20
```

> 함수 내부에서 var (혹은 let, const) 키워드를 사용하지 않고 변수를 선언하면, 해당 변수는 지역 변수가 아닌 **전역 변수로 선언**된다.

## 함수의 유효 범위 (function scope)

자바스크립트에서는 함수를 블록 대신 사용.

자바스크립트에서 함수는 자신이 정의된 범위 안에서 정의된 모든 변수 및 함수에 접근할 수 있다.

**전역 함수**는 모든 전역 변수와 전역 함수에 접근할 수 있다.

반면, 다른 함수 내에 정의된 **내부 함수**는 그 함수의 부모 함수(parent function)에서 정의된 모든 변수 및 부모 함수가 접근할 수 있는 모든 다른 변수까지도 접근할 수 있다.

```javascript
// x, y, name을 전역 변수로 선언
var x = 10,
  y = 20;

// sub()를 전역 함수로 선언
function sub() {
  return x - y; // 전역 변수인 x, y에 접근
}

document.write(sub() + "<br>");

//parentFunc()을 전역 함수로 선언
function parentFunc() {
  var x = 1,
    y = 2; // 전역 변수와 같은 이름으로 선언하여 전역 변수의 범위를 제한함

  function add() {
    // add() 함수는 내부 함수로 선언됨
    return x + y; // 전역 변수가 아닌 지역 변수 x, y에 접근함
  }

  return add();
}

document.write(parentFunc());
```

## 함수 호이스팅(hoisting)

자바스크립트에서 함수의 유효 범위라는 것은 함수 안에서 선언된 모든 변수는 함수 전체에 걸쳐 유효하다는 의미.

그런데 이 유효 범위의 적용이 변수가 선언되기 전에도 똑같이 적용된다.

이러한 특징을 **함수 호이스팅(hoisting)**이라고 한다.

```javascript
var globalNum = 10; // globalNum을 전역 변수로 선언

function printNum() {
  document.write(
    "지역 변수 globalNum 선언 전의 globalNum의 값은 " +
      globalNum +
      "입니다.<br>"
  ); // [1]

  var globalNum = 20; // globalNum을 지역 변수로 선언 // [2]
  document.write(
    "지역 변수 globalNum 선언 후의 globalNum의 값은 " +
      globalNum +
      "입니다.<br>"
  );
}

printNum();
```

[1]의 시점에서 globalNum이라는 지역 변수가 선언만 되어 있고, 아직 초기화가 되지 않은 상태라 undefined가 출력.

[2]의 시점에서 globalNum을 지역 변수로 선언함과 동시에 20이라는 값을 대입 하여 20이 출력.

> 자바스크립트에서는 함수 호이스팅이 자동으로 수행되지만, **항상 함수 블록의 첫 부분에 변수를 선언**하는 것이 좋다.
