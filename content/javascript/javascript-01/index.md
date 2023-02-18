---
title: 자바스크립트 변수
date: '2022-02-09 00:00:00'
author: 이용민
tags: javascript 
categories: javascript
---
![javascript-logo.png](javascript-logo.png)

변수는 값을 저장하고 참조하기 위해 사용하고, 언어 관점에서 데이터를 관리하기 위한 핵심요소중의 하나이다.

## 변수 선언
```bash
var a = 10;
```
보통 변수를 선언할 때, 위와 같은 방식을 사용한다.   
이것은 정확히 얘기하면 변수 선언과 값의 할당을 한번에 표현한 것이다.

변수 a는 사람을 위한 식별자이고 자바스크립트 엔진은 변수 a를 메모리 주소로 파악하고 메모리에 접근한다.

자바스크립트 엔진은 변수 선언을 선언, 초기화 2단계에 걸쳐서 수행한다.

* 선언 단계: 엔진이 변수 이름을 인식하는 단계
* 초기화 단계: 값을 저장할 공간을 확보하고 undefined를 할당하여 초기화 하는 단계

```bash
var a;
console.log(a);

> undefined
```
그렇기 때문에 변수에 값을 할당하지 않았을 때, undefined가 출력된다.

초기화 단계를 거침으로써 쓰레기 값(garbage value)을 참조하는 위험으로부터 안전한 것이다.

## 값의 할당
변수 선언은 코드를 읽어들이는 시점인 런타임 이전에 실행되고   
값의 할당은 런타임에 실행된다.   
``` bash
console.log(a);
a = 1; // 값의 할당
var a; // 변수 선언
console.log(a);

> undefined
> 1
```
실행 시기가 다르기 때문에 위와 같은 결과가 출력된다.

## 호이스팅
자바스크립트 엔진의 특성이다.   
```bash
console.log(a);
var a;

> undefined
```
오류가 출력될 것 같지만 undefined가 출력된다.   
변수 선언이 런타임 이전에 실행되기 때문이다.

이처럼 선언문이 코드의 위로 끌어 올려진 것 처럼 동작하는 특징을 **호이스팅** 이라고 한다.

## var, const, let
자바스크립트의 변수 종류는 var, const, let 3가지가 있다.   

### ① var
var는 ES6 이전까지 변수를 선언할 수 있는 유일한 키워드였다.   
ES6에서 const, let의 탄생은 var의 단점으로부터 비롯된다.   
* 변수 중복 선언 허용   
> var 키워드는 변수의 중복 선언이 가능하다.
```bash
var a = 1;
var b = 2;

var a = 10;

console.log(a);

> 10
```
이와 같이 같은 변수에 중복 선언이 가능하기 때문에 먼저 선언된 변수의 값이 변경되는 부작용이 존재했다.  

* 함수 단위 스코프  
> var 키워드는 함수 단위의 스코프를 가진다. 
```bash
var a = 1;

if(true) {
  var a = 10;
}
console.log(a);

> 10
```
따라서, 전역 변수가 남발될 가능성이 있고 의도치 않게 위처럼 변수가 중복 선언되는 경우가 발생한다.

 * 변수 호이스팅  
> var 키워드는 호이스팅에 의해 변수 선언 이전에 호출해도 에러가 아닌 undefined를 출력한다.
```bash
console.log(a);
a = 1;
console.log(a);
var a;

> undefined
> 1
```
이는 가독성을 떨어뜨리고 오류를 발생시키는 여지를 남길 수 있다.

**❗️ 이러한 문제점들로 인해 let, const 변수가 등장했다.**   
### ② let   
* 변수 중복 선언 방지
> let 변수는 변수의 중복 선언을 막는다.
```bash
let a = 1;
let a = 2;

> Uncaught SyntaxError: Identifier 'a' has already been declared
```
위와 같이 문법 에러를 발생시켜 중복 선언을 방지한다.

* 블록 레벨 스코프
> let 키워드는 var 키워드와 달리 블록 단위의 스코프를 가진다.
```bash
let a = 1;
{
    let a = 2;
    let b = 10;
    console.log(a);
    console.log(b);
}
console.log(a);
console.log(b);

> 2
> 10
> 1
> Uncaught ReferenceError: b is not defined
```
위처럼 블록 레벨 스코프를 따른다.

* 변수 호이스팅
> let 키워드는 호이스팅을 방지한다.
```bash
console.log(a);
let a;

> Uncaught ReferenceError: Cannot access 'a' before initialization
```
위처럼 참조 에러를 발생시켜 호이스팅을 방지시킨다.

### ③ const
const 키워드는 상수를 선언할 때 사용하지만 상수 사용만을 위해 사용하지는 않는다.   

* 선언
> const 키워드는 선언과 동시에 초기화를 해주어야한다.
```bash
const a;

> Uncaught SyntaxError: Missing initializer in const declaration
```
선언만 한다면 위와 같은 에러가 출력된다.

* 재할당 방지
> const 키워드는 상수 값을 다루므로 재할당을 막는다.
```bash
const a = 1;
a = 1;

> Uncaught TypeError: Assignment to constant variable
```
위와 같이 값 재할당을 막는다.

---

📂 **참고자료**
* 모던 자바스크립트 Deep Dive 도서