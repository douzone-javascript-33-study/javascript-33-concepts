## == 동등 / 동등 연산자 / Double Equals / 느슨한 비교 / Equal Operator

- **느슨한 동등성을 확인하는 연산자. 자동으로 타입 강제 변환(type coercion conversion)을 수행**

## === 동일성 / 일치 연산자 / Triple Equals / 엄격한 비교 / Strict Equal Operator

- **엄격한 동일성을 확인하는 연산자. 타입과 값 모두 동일하면 true를 반환하며 그렇지 않을 경우 false를 반환**

## **기본 타입**

```jsx
let a = 1;
let b = "1";
console.log(a == b); // true
console.log(a === b); // false

console.log(null == undefined); // true
console.log(null === undefined); // false

console.log(true == 1); // true
console.log(true === 1); // false

console.log(0 == "0"); // true
console.log(0 === "0"); // false
console.log(0 == ""); // true
console.log(0 === ""); // false

console.log(NaN == NaN); // false
console.log(NaN === NaN); // false
```

## **객체 타입**

```jsx
let a = [1,2,3];
let b = [1,2,3];
console.log(a == b); // false
console.log(a === b); // false

// 참조하는 메모리의 주소가 다르기 때문에 두 a, b는 같지 않다

let a = [1,2,3];
let b = [1,2,3];
let c = b;
console.log(b === c); // true
console.log(b == c); // ture

let x = {};
let y = {};
let z = y;
console.log(x == y) // false
console.log(x === y) // false
console.log(y === z) // true
console.log(y == z) // true

0 == "0" // true
0 == []  // true
'0' === []  // false
```

## **거짓 같은 값 (Falsy, falsey로 쓰이기도 함)**

## **값은 불리언 문맥에서 false로 평가되는 값**

## **거짓 같은 값**

```
false, null, undefined, 0, -0, 0n, NaN, ''
```

---

## typeof

- **typeof는 피연산자의 타입을 반환하는 연산자. 피연산자가 선언되지않은 변수일 경우 undefined를 반환**

## **typeof로 리턴받을 수 있는 type은?**

- **`UndefinedStringNumberBooleanObjectFunctionSymbolbigint`**

## **typeof**

```jsx
// undefined
console.log(typeof undefined);

// string
console.log(typeof '');
console.log(typeof 'ㅎㅇ');
console.log(typeof `template literal`);
console.log(typeof '1');

// number
console.log(typeof 37);
console.log(typeof 3.14);
console.log(typeof NaN);

// boolean
console.log(typeof true);
console.log(typeof !!(0));         // !!  느낌표 두개 연산자    Double Exclamation Marks

// object
console.log(typeof { a: 1 });
console.log(typeof [1, 2, 4]);
console.log(typeof new Date());
console.log(typeof null);

// function
console.log(typeof function() {});
console.log(typeof class C {});
console.log(typeof Math.sin);

// symbol
console.log(typeof Symbol());
console.log(typeof Symbol('kartel'));

// bigint
console.log(typeof 42n);
```

## **+ 느낌표 두개 연산자 Double Exclamation Marks**

- **`!!`는 `boolean`으로 바꿔줌null이나 undefined 값을 false로 변환할 때 사용할 수가 있음정의되지 않은 변수 undefined 값을 가진 내용의 논리 연산 시에도 확실한 true / false를 가지도록 하는게 목적조건 검사할때 true false로 체크하게 해놨는데 다른게 들어가있으면 의도대로 동작 안할 수 있기 때문 → 어떤 타입이 return되던지 boolean값으로 처리하도록**

## **느낌표 두개 연산자 1**

```jsx
let case1;  // undefined
console.log("case1  : " + (case1));    // case1  : undefined
console.log("!case1 : " + (!case1));   // !case1 : true
console.log("!!case1: " + (!!case1));  // !!case1: false

const case2 = true; // 불리언 데이터
console.log("case2  : " + (case2));    // case2  : true
console.log("!case2 : " + (!case2));   // !case2 : false
console.log("!!case2: " + (!!case2));  // !!case2: true

const case3 = null; // null
console.log("case3  : " + (case3));    // case3  : null
console.log("!case3 : " + (!case3));   // !case3 : true
console.log("!!case3: " + (!!case3));  // !!case3: false
```

## **느낌표 두개 연산자 2**

```jsx
!!false === false // true
!!true === true   // true

!!0 === false     // true
!!parseInt("foo") === false // true   NaN은 false
!!1 === true      // true
!!-1 === true     // true

!!"" === false      // true
!!"foo" === true    // true
!!"false" === true  // true

!!window.foo === false // true    정의 되지 않은 변수는 false
!!null === false       // true    null은 false

!!{} === true  // true
!![] === true  // true
```

---

## **null을 typeof로 검사하면 object → === 로 비교 (JS 초기버그)**

```jsx
const n = null;
typeof n // 'object'
n == null // true
n === null // true
toString.call(null) // [object Null]
```

+ Array, Date, 정규표현식, 사용자 정의 객체, DOM요소, null 등은 object로 반환 → 그럼 뭘로?

---

## **+ 다양한 타입 확인하는 방법**

1. `Array.isArray([]) (Array만)`
2. Object.prototype.toString.call([])
    1. `toString()`은 모든 객체에 사용되어 해당 객체의 클래스를 가져올 수 있다
        1. [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/toString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
3. `[] instanceof Array`
    1. iframe을 통해서 작동하지 않기 때문에 올바르지 않은 방법
4. `[].constructor`
5. `&&`와`[].constructor`

```jsx
// Array.isArray  (ES5)
const arr = [];
Array.isArray(arr) // true
const obj = {};
Array.isArray(obj) // false

// instanceof
arr instanceof Array // true

// .constructor
// 배열의 constructor 프로퍼티는 전역객체인 Array를 레퍼런스로 가진다
arr.constructor === Array // true

// Object.prototype.toString.call()
// 이 메서드는 모든 Object에 대해 작동하므로 JavaScript에서 유형 검사를 입력하는 가장 좋은 방법
// 장황하지만 모든 기본 유형 및 모든 객체에 대해 작동함. 항상 변수에 대한 생성자 이름을 반환함
Object.prototype.toString.call([]) === '[object Array]'  // true
Object.prototype.toString.call(arr) === '[object Array]' // true
toString.call(new Date);    // [object Date]
toString.call(new String);  // [object String]
toString.call(Math);        // [object Math]
toString.call(undefined);   // [object Undefined]
toString.call(null);        // [object Null]
```

성능은 Object.prototype.toString.call ([]) 가 다른 메서드들에 비해 조금 느리게 나오긴하는데 여전히 빠르긴 빠름

5가지 방법 참고: [https://ichi.pro/ko/javascripteseo-baeyeol-eul-hwag-inhaneun-bangbeob-117450435333665](https://ichi.pro/ko/javascripteseo-baeyeol-eul-hwag-inhaneun-bangbeob-117450435333665)

---

## [Object.is](http://object.is/)() (ES6)

- **==처럼 타입변환을 안하고 ===와 기본적인 동작은 같지만 NaN 의 비교와 -0, 0 비교가 가능하다는 차이가 있다.**
- [Object.is](http://object.is/)(비교할 첫 번째 값, 비교할 두 번째 값); 반환값 Boolean

## **[Object.is](http://object.is/)()**

```jsx
console.log(Object.is(NaN, NaN)); 	// true
console.log(NaN === NaN); 	 	      // false

console.log(Object.is(NaN, 0/0));   // true

// +0과 -0 비교 결과
console.log(Object.is(+0, -0)); 	  // false
console.log(+0 === -0);			        // true

console.log(Object.is(-0, -0));     // true
```

Object.is() MDN: [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

[https://dev.to/kennethlum/why-reactjs-using-object-is-comparison-is-better-than-using-1kf3](https://dev.to/kennethlum/why-reactjs-using-object-is-comparison-is-better-than-using-1kf3)

---

## **참고 TMI**

==, === 변환 과정: [https://medium.com/jung-han/js-2%ED%83%84-%EA%B7%B8%EB%A6%AC%EA%B3%A0-object-is-e58b72e90443](https://medium.com/jung-han/js-2%ED%83%84-%EA%B7%B8%EB%A6%AC%EA%B3%A0-object-is-e58b72e90443)

== 연산자 테스트: [https://felix-kling.de/js-loose-comparison/](https://felix-kling.de/js-loose-comparison/)

## **==, ===, [Object.is](http://object.is/)() 이미지**

![https://i.stack.imgur.com/zETNR.png](https://i.stack.imgur.com/zETNR.png)
