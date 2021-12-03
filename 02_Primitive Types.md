# 원시 자료형이란?

- 자바스크립트에서 원시 타입의 데이터는 객체가 아니면서 method를 가지지 않는 7가지의 타입
- 원시 자료형의 보관함인 변수에는 하나의 데이터만 담을 수 있습니다.

# 원시 자료형 7가지
- string
- number
- boolean
- undefined
- null
- symbol (ES2015)
- bigint (ES2020)

# 7가지 예제

- number : 숫자 (정수, 실수 가능, 연산 가능)

```jsx
let A = 3;
let B = 3.141592;
console.log(A + B); // 6.141592
```

- string : 문자 (큰따옴표, 작은따옴표 둘 다 가능)

```jsx
let str = "Hello";
let str = 'Hello';
```

- boolean : true & false

```jsx
let bool = true;
let bool = false;
```

- undefined : 변수가 정의되지 않았거나 값이 없다.

```jsx
let age;
console.log(age); // undefined
```

- null : 의도적으로 비어있음을 표현하기 위해 null 이라는 것이 들어있다.

```jsx
let nothing = null;
```

- symbol : 심볼(symbol)은 유일한 식별자(unique identifier)를 만들고 싶을 때 사용합니다. (+ES2015)

```jsx
let id1 = Symbol("id"); let id2 = Symbol("id"); console.log(id1 == id2); // false
```

- bigint : number 타입이 가지는 정수 한계보다 큰 숫자를 보관시에 사용합니다. (+ES2020)

```jsx
console.log(2 ** 53 - 1); // 9007199254740991 ->자바스크립트에서 Number로서 연산할 수 있는 가장 큰 수
let bigInt = 1234567890123456789012345678901234567890n;
```
