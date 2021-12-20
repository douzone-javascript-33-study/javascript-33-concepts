var 키워드와 let / const 키워드의 차이

- var은 함수 레벨 스코프를 가짐 - 블록스코프를 무시함 (화살표 함수의 블록스코프는 예외)
    - 전역변수 : 함수 외부에서 선언한 변수
    - 함수의 변수 : 함수 내부에서 선언한 변수
- let / const 는 블록 레벨 스코프를 가짐
    - 전역변수 : 어느 블록에도 속해있지 않은 변수
    - 지역변수 : 블록 내부에서 선언한 변수
    

블록이란?

- 중괄호 {} 세트 안에 있는 코드를 말한다.

## Scope (스코프)

- 범위라는 뜻을 가지고 있다.
- 자바스크립트에서는 변수에 접근할 수 있는 범위라고 볼 수 있다.
- 종류
    - global Scope (전역 스코프)
    - local Scope (지역 스코프)
        - Function Scope (함수 스코프)
        - Block Scope (블록 스코프)

```jsx
const a = 111; // 전역 스코프
 
function print() { // 지역 스코프
	const a = 222;
	console.log(a); // 222
}
 
print();
 
console.log(a); // 111
```

## Global Scope (전역 스코프)

- 전역에 선언되어 있어서 어느 곳에서든 해당 변수에 접근이 가능하다.
- 어느 {} 괄호안에 속하지 않으면 전역 변수라고 한다.
- 네이밍 충돌이 발생하는 경우가 생길 수 있기 때문에 자주쓰는것을 지양해야 한다.
    - Scope Pollution (스코프 오염)

```jsx
const a = 111; // 전역 스코프
 
function print() {
	console.log(a); // 111
}
 
print();
 
console.log(a); // 111
```

## Local Scope (지역 스코프)

- 해당 지역에서만 접근 가능하다.
- 코드 내 특정 구역에서만 사용가능한 변수를 지역변수라고 한다.
- 종류
    - Function Scope (함수 스코프)
    - Block Scope (블록 스코프)

```jsx
const a = 111; // 전역 스코프
 
function print() { // 지역 스코프
	const b = 222;
	console.log(a); // 111
	console.log(b); // 222
}
 
print();
 
console.log(a); // 111
console.log(b); // 접근불가
```

## Function Scope (함수 스코프)

- var로 변수를 선언 시에 함수 스코프가 생성된다.
- 함수를 선언하게되면 새로운 스코프가 생성되는거다.
- 함수 안에서 선언한 변수는 함수 안에서만 사용이 가능하다.
- 함수 내부 전체에서 유효한 값이 된다.
- 함수 밖에서는 접근 불가능하다.
- 화살표 함수는 함수 스코프가 아닌 블록 스코프를 가진다.

```jsx
function print() { // 함수 스코프
	var a = 111;
	if (true) {
		var b = 222;
	}
	console.log(a); // 111
	console.log(b); // 222
}
```

## Block Scope (블록 스코프)

- let / const로 변수를 선언 시에 블록 스코프가 생성된다.
- {} 괄호로 둘러쌓인 부분을 블록이라고 칭한다.
    - ex) 화살표 함수, 조건문, 반복문, try catch문
- {} 괄호 안에서 변수를 선언하면 괄호 안에서만 사용가능하다.
- 함수를 사용하기 위해서는 {} 괄호를 사용하기 때문에 블록 스코프는 함수 스코프의 부분집합이라고 할 수 있다.

```jsx
const print = () => { // 블록 스코프
	const a = 111;
	if (true) { // 블록 스코프
		const b = 222;
		console.log(a); // 111
		console.log(b); // 222
	}
	console.log(a); // 111
	console.log(b); // 접근 불가
}
```

## 스코프 규칙

- 상위스코프를 함수를 선언 시에 결정할지, 함수를 호출 시에 결정할지 정해놓은 규칙
- 종류
    - 렉시컬 스코프 규칙
    - 다이나믹 스코프 규칙

## Lexical Scope (렉시컬 스코프)

- 정적 스코프라고도 부른다.
- 함수를 어디서 선언했는지에 따라 상위 스코프를 결정하는 것을 의미한다.
- 함수의 호출은 중요하지않고 함수의 선언이 중요하다.
- 자바스크립트에서는 밑과 같은 코드를 작성할 때, 이미 실행 단계에서 코드들의 스코프를 결정한다.

```jsx
const a = 111; // global 범위

function first() { // first 함수 범위
  const a = 222;
  second();
}

function second() { // second 함수 범위
  console.log(a);
}

first(); // 111
second(); // 111
```

## ↔ Dynamic Scope (다이나믹 스코프)

- 동적 스코프라고도 부른다
- 함수의 호출에 따라 상위 스코프가 정해지는 것
- Perl, Bash Shell 등에서 동적스코프를 따른다.
- 대부분의 언어는 정적 스코프를 따른다.

```jsx
const a = 111;

function first() { // 호출 시 결정됨
  const a = 222;
  second();
}

function second() { // 호출 시 결정됨
  console.log(a);
}

first(); // 222
second(); // 111
```

## **var 키워드의 문제점**

- 함수 레벨 스코프(Function-level scope)
    - 전역 변수 남발
    - for문 초기화식에서 사용한 변수를 외부에서 참조할 수 있다.
- var 키워드 생략 허용
    - 의도하지 않은 변수의 전역화
- 중복 선언 허용
    - 의도하지 않은 변수값 변경
- 변수 호이스팅
    - 변수를 선언하기 전에 참조가 가능하다

## **중복 선언 허용**

- var 키워드는 재선언을 해도 아무런 에러가 발생하지 않는다.
- 의도하지 않은 변수값을 변경 할 수도있다.
- 그래서 재선언을 방지해주는 let 키워드를 사용하는게 좋다.

```jsx
var a = 1;
var a = 2;
console.log(a); // 2
```

```jsx
let a = 1;
let a = 2;
console.log(a); // 에러 발생
```

## Hoisting (호이스팅)

- 함수 안에 있는 선언들을 모두 상위로 끌어올려 해당 함수 유효 범위의 최상단에 선언하는 것을 의미한다.
- function 키워드와 함께 선언된 함수들은 항상 현재 스코프의 가장 위로 호이스팅이 된다.
- 함수 표현식으로 작성된 함수들은 현재 스코프의 가장 위로 호이스팅이 되지 않는다.
    - 함수 선언문의 경우에만 호이스팅 대상이 된다.
    - 함수는 항상 사용 전에 미리 선언하는 것이 좋다.

```jsx
function print() { // 함수 스코프
	var a = 111;
	if (true) {
		var b = 222;
	}
}
```

```jsx
// 호이스팅
function print() { // 함수 스코프
	var a; // 스코프의 최상단에 정의됨
	var b; // 스코프의 최상단에 정의됨
	a = 111;
	if (true) {
		b = 222;
	}
}
```

var를 사용하고 같은 변수명을 사용 시

```jsx
function print() { // 함수 스코프
	var a = 111;
	if (true) {
		var a = 222;
		console.log(a);
	}
	console.log(a);
}
```

```jsx
// 호이스팅
function print() { // 함수 스코프
	var a; // 스코프의 최상단에 정의됨
	var a; // 스코프의 최상단에 정의됨
	a = 111;
	if (true) {
		a = 222;
		console.log(a); // 222
	}
	console.log(a); // 222
}
```

let을 사용하고 같은 변수명을 사용 시

```jsx
function print() { // 함수 스코프
	let a = 111;
	if (true) {
		let a = 222;
		console.log(a);
	}
	console.log(a);
}
```

```jsx
// 호이스팅
function print() { // 함수 스코프
	let a; // 스코프의 최상단에 정의됨
	a = 111;
	if (true) {
		let a; // 스코프의 최상단에 정의됨
		a = 222;
		console.log(a); // 222
	}
	console.log(a); // 111
}
```

## 함수표현식의 호이스팅  예제

1

```jsx
count();

var count = function() {
    console.log('count는 1이다.');
}
```

```jsx
// 호이스팅
var count;

count(); // 변수를 호출하게 되므로 에러 발생

count = function() {
    console.log('count는 1이다.');
}
```

2

```jsx
var count = function() {
    console.log('count는 1이다.');
}

count();
```

```jsx
// 호이스팅
var count;

count = function() {
    console.log('count는 1이다.');
}

count(); // 정상적으로 호출 됨
```

## let / const는 호이스팅이 안된다?

- let / const도 호이스팅이 된다.
- 하지만 var의 호이스팅 같은 경우는 선언을 스코프 최상단으로 올리고 초기화를 해주지만,
    - 선언 - 초기화 - 할당
- let / const 의 경우에는 선언만 스코프 최상단으로 올리고 바로 초기화를 해주지 않는다.
    - 선언 - TDZ - 초기화 - 할당
    - 이처럼 TDZ(Temporal Dead Zone)라는 것이 개입해서 초기화가 되기 전에 변수에 접근하게 되면 TDZ에 의해 에러가 발생한다.
- 이렇듯 TDZ가 에러를 발생시키기 때문에 호이스팅이 되지 않는다고 오해하는 경우가 많다.

```jsx
var a; // 초기화 됨
console.log(a); // undefined
a = 10;
```

```jsx
let a; // 초기화 안됨
console.log(a); // 에러 발생
a = 10;
```

## **스코프 오염 (Scope Pollution)**

- 전역변수로 선언하면 항상 접근가능하니 편하다고 생각할 수 있지만, 너무 많은 전역변수가 있으면 오히려 나중에 문제가 발생할 수 있으니 주의해야 한다.
- 전역변수는 선언하게되면 이 변수들이 프로그램이 끝날때 까지 남아있기 때문에, 네임스페이스가 빠른 속도로 차버리게 된다.
- 이렇게 되면  전역 변수가 다른 로컬 변수와 출동하여 예상치 못한 동작을 하게될 수도 있다.

## 스코프 체인

- 스코프가 중첩되게 되면 계층적인 구조가 형성된다.
- 외부 스코프에서는 내부 스코프의 변수에 접근할 수 없지만, 내부 스코프는 외부 스코프의 변수에 접근가능하다.
- 자바스크립트 엔진은 식별자를 찾을 때 일단 자신이 속한 스코프에서 찾고, 그 스코프에 식별자가 없으면 상위 스코프에서 다시 찾아 나간다.
- 이렇게 계속해서 상위 스코프로 식별자를 찾는 현상을 스코프 체인이라고 한다.
- 스코프가 중첩되어있는 모든 상황에서 발생하게 된다.
- 이는 스코프가 함수의 중첩에 의해 계층적인 구조를 가질 수 있다는 것을 의미한다.

## Closures (클로저)

- 스코프 체인을 이용하여 이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 방법이다.
- 외부에서 내부 변수에 접근할 수 있도록 하는 함수이다.
- 함수안에 함수를 선언해서 클로저를 만든다.

클로저 만드는 형태 1 - 중첩 함수

```jsx
function outerFunction() {
  let x = 1;
  return function innerFunction(y) { // innerFunction 함수는 클로저다.
    return (x = x + y);
  };
}
let a = outerFunction(); // 외부함수 호출은 한번만. 이제 a 변수는 innerFn 함수를 참조한다.

console.log(a(2)); // 3
console.log(a(2)); // 5
console.log(a(2)); // 7
```

클로저 만드는 형태 2 - **전역에 선언한 변수를 박스 안에서 함수로 정의하고 전역에서 호출**

```jsx
let globalFunction;
{
  let x = 1;
  globalFunction = function(y) { // globalFunction 함수는 클로저다.
    return x = x + y;
  }
}
globalFunction(2); // 3
globalFunction(2); // 5
globalFunction(2); // 7
```
