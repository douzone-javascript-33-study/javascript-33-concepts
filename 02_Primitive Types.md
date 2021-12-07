# 원시 자료형이란?

- 자바스크립트에서 원시 타입의 데이터는 객체가 아니면서 method를 가지지 않는 7가지의 타입
- 원시 자료형의 보관함인 변수에는 하나의 데이터만 담을 수 있습니다.

# 원시 자료형 7가지
- string
- number
- boolean
- undefined
- null
- symbol (+ES2015)
- bigint (+ES2020)

## 자바스크립트는 느슨한 타입의 언어이다. (혹은 동적 언어라고도 말함)

- 이 말은 곧 변수의 타입을 미리 지정할 필요가 없다는 뜻이다.
- 타입은 프로그램이 처리되는 과정에서 자동으로 파악된다.
- 같은 변수에 여러 타입의 값을 넣을 수 있다.
- 느슨한 타입 ↔ 엄격한 타입

`let A = 3; // 숫자 타입`

`A = '이재성'; // 문자 타입`

`console.log(A); // 이재성`

## 자바스크립트 타입 종류

![http://wiki.duzon.com:8080/download/attachments/127134205/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-12-02%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.20.25.png?version=1&modificationDate=1638425531771&api=v2](http://wiki.duzon.com:8080/download/attachments/127134205/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-12-02%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.20.25.png?version=1&modificationDate=1638425531771&api=v2)

자바스크립트의 자료형은 ***원시 타입(Primitive Type)***과 ***참조 타입(Reference Type)***으로 나뉜다.원시 타입 데이터는 변수에 값이 할당되어 선언, 덮어쓰기 등을 수행할 때 메모리 영역에 직접적으로 접근하게 된다.반면 참조 타입 데이터는 값이 변수에 직접 저장되는 것은 아니며, `힙(Heap)`이라는 저장소에 해당 데이터가 들어있는 주소값을 저장하게 된다.

## 콜 스택(Call stack)과 힙(Heap)

- 콜 스택 : 원시타입 값과 함수 호출의 실행 컨텍스트(Execution Context) 저장
- 힙 : 객체, 배열, 함수와 같이 크기가 동적으로 변할 수 있는 참조타입 값 저장

![http://wiki.duzon.com:8080/download/attachments/127134205/javascript_runtime.png?version=1&modificationDate=1638765114981&api=v2](http://wiki.duzon.com:8080/download/attachments/127134205/javascript_runtime.png?version=1&modificationDate=1638765114981&api=v2)

## 원시 자료형 (Primitive data type) = 원시 타입 (Primitive Types)

- 객체가 아니면서 method를 가지지 않는 7가지의 타입이 있다.
- 원시 자료형은 모두 “하나”의 정보, 즉, 데이터를 담고 있다.
- number, string, boolean, undefined, null, symbol, bigint<7 가지>
- `number : 숫자 (정수, 실수 가능, 연산 가능)`

`let A = 3;`

`let B = 3.141592;`

`console.log(A + B); // 6.141592`

- `string : 문자 (큰따옴표, 작은따옴표 둘 다 가능)`

`let str = "Hello";`

`let str = 'Hello';`

- `boolean :` true & false

`let bool = true;`

`let bool = false;`

- `undefined :` 변수가 정의되지 않았거나 값이 없다.

`let age;`

`console.log(age); // undefined`

- `null :` 의도적으로 비어있음을 표현하기 위해 null 이라는 것이 들어있다.

`let nothing = null;`

`console.log(nothing); // null`

- `symbol : 심볼(symbol)은 유일한 식별자(unique identifier)를 만들고 싶을 때 사용합니다. (+ES2015)`

`let id1 = Symbol("이재성");`

`let id2 = Symbol("이재성");`

`console.log(id1 == id2); // false`

`console.log(id1.description); // 이재성`

- `bigint : number 타입이 가지는 정수 한계보다 큰 숫자를 보관시에 사용합니다. (+ES2020)`

`console.log(2 ** 53 - 1); // 9007199254740991 -> 자바스크립트에서 Number로서 연산할 수 있는 가장 큰 수`

`let bigInt = 1234567890123456789012345678901234567890n;`

## typeof 연산자를 이용해서 자료형을 확인할 수 있다.

`console.log(typeof` `3); // number`

`console.log(typeof` `"이재성"); // string`

`console.log(typeof` `true); // boolean`

`console.log(typeof` `undefined); // undefined`

`console.log(typeof` `null); // object`

`console.log(typeof` `Symbol("id")); // symbol`

`console.log(typeof` `10n); // bigint`

## 추가내용 및 의문점

![http://wiki.duzon.com:8080/s/ko_KR/7701/445126ab56584205167f1c035c86df495c7c4192/_/images/icons/emoticons/add.svg](http://wiki.duzon.com:8080/s/ko_KR/7701/445126ab56584205167f1c035c86df495c7c4192/_/images/icons/emoticons/add.svg)

## typeof null === object 라고 나오는것은 자바스크립트 오류

- 자바스크립트 초기버전의 버그이다.
- typeof가 자료형을 검사할 때 null에 대한 확인 절차가 없어서 생기는 오류이다.
- 버그를 수정하지 않는 이유는 이미 수많은 사이트의 코드들이 기존의 typeof를 이용해서 작성되있어서, 수정시에 많은 문제가 발생하기 때문에 안 고친다.

`if(is_undefined?){ // undefined 체크`

`return` `undefined;`

`}else` `if(is_object?){ // object 체크`

`if(is_function?){ // function 체크`

`return` `function;`

`}else{`

`return` `object;`

`}`

`}else` `if(is_number?){ // number 체크`

`return` `number`

`}else` `if(is_string?){ // string 체크`

`return` `string`

`}else` `if(is_boolean?){ // boolean 체크`

`return` `boolean`

`}`

- 그래서 null 에 대한 타입체크를 원한다면, 일치연산자( === )를 이용하면 체크가 가능하다

`let A = null;`

`A === null; // true`

## null 과 undefined

- null 은 존재하지않음 이라는 값 (의도적으로 비어있음을 표현하기 위함)
- undefined 는 정의되지 않음 이라는 값이다. (값을 할당하지 않은 변수)

`let A = null; // null`

`let B; // undefined`

## bigint 와 number

- bigint와 number는 동등은 하지만 일치하지는 않다. (값은 같지만 타입이 다르다.)
- 자바스크립트에서 number가 표현할 수 있는 최대값 ( 2 ** 53 - 1 )

![http://wiki.duzon.com:8080/download/attachments/127134205/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-12-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.10.41.png?version=1&modificationDate=1638766941318&api=v2](http://wiki.duzon.com:8080/download/attachments/127134205/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-12-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.10.41.png?version=1&modificationDate=1638766941318&api=v2)

- bigint가 더 큰 수를 표현하는 방법
    - 문자열로 변환해서 관리한다.
    - 부호와 절대값을 분리해서 관리한다.

`10n == 10 // true`

`10n === 10 // false`

## Symbol은 언제 사용하는가?

- 객체의 값을 숨기기 위해서 사용

    `let obj = {`

    `name: "이재성",`

    `age: 27,`

    `[Symbol('phoneNumber')]: "01022256816"`

    `}`

    `Object.keys(obj); // ["name", "age"] 이렇게 phoneNumber 키값을 제외하고 보여준다.`

    `Object.values(obj); // ["이재성", 27]`

- 객체의 가장 unique한 property key에 사용

## 

## 래퍼객체(Wrapper object)

- 래퍼객체란 원시타입의 값을 감싸는 형태의 객체이다.
- 원시타입을 new 키워드로 생성하면 원시타입에 대한 래퍼객체가 생성된다.
- 원시타입을 객체 타입으로 메소드를 사용하고 프로퍼티에 접근하기 위해서 존재한다.
- 원시타입에 대응하는 래퍼객체가 존재한다. ( null, undefined 제외)
- 종류
    - String
    - Number
    - Boolean
    - Symbol
    - Bigint
- 예시

`let str = "dog";              // 문자열 리터럴 생성`

`let strObj = new` `String(str); // 문자열 객체 생성`

`strObj.length;                // 3 리터럴 값은 내부적으로 래퍼 객체를 생성한 후에 length 프로퍼티를 참조함.`

`str == strObj;                // true - 동등 연산자는 리터럴 값과 해당 래퍼 객체를 동일하게 봄.`

`str === strObj;               // false - 일치 연산자는 리터럴 값과 해당 래퍼 객체를 구별함.`

`typeof` `str;                   // string 타입`

`typeof` `strObj;                // object 타입`

`// strObj`

`{`

`0: "d",`

`1: "o",`

`2: "g",`

`length : 3`

`}`

`strObj[0] // d`

`strObj[1] // o`

`strObj[2] // g`

`strObj.length // 3`

## 

## 그런데 원시타입으로 프로퍼티와 메소드를 사용할 수 있는 이유?

`str[0] // d`

`str[1] // o`

`str[2] // g`

`str.length // 3`

- 오토박싱(Auto-Boxing)
    - 원시타입을 래퍼객체로 자동 변환해주는 과정
    - str 이라는 string 원시타입을 자바스크립트가 임시적으로 Object 타입으로 자동으로 변환해주는 것
    - 변환해줌으로써 메소드와 프로퍼티를 사용할 수 있게되고, 사용이 끝나게되면 다시 원시타입으로 되돌아간다.
    - 사용이 끝난 객체는 가비지 컬랙션의 대상이되어 자동으로 메모리가 정리된다.

## 참조타입(Reference Type)

- 원시자료형을 제외한 모든 타입을 참조타입이라고 한다.
- 원시타입처럼 변수에 직접 값을 저장하지 않고, 값은 힙 영역에 저장되고 변수에는 그 힙영역에 값을 가리키는 포인터 주소가 저장된다.
- 종류
    - 배열 (Array)
    - 객체 (Object)
    - 함수 (Function)
- Object 예시

`let obj = {`

`name: "이재성",`

`age: 27`

`}`

`obj.name // 이재성`

`obj.age // 27`

`typeof` `obj // object`

## Infinity

