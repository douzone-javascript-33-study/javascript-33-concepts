site: medium.com

- [https://medium.com/@su_bak/immutable을-사용하는-이유-24aa152237e0](https://medium.com/@su_bak/immutable%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-24aa152237e0)
- 자바스크립트의 숫자 타입은 모든 수를 실수로 처리
- Nullish coalescing operator (??) 연산자
    - **널 병합 연산자 (`??`)** 는 왼쪽 피연산자가 [null](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/null) 또는 [undefined](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined)일 때 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환하는 논리 연산자이다.
    - `||`은 0, 과 빈 문자열 등을 포함한 falsy한 값을 방지하고, `??`은 오직 nullish한 값을 방지한다.

''

```jsx

let name = 0;

console.log('hello', name); // 0
console.log('hello', name || '시명'); // '시명'
->
let example = 0;
console.log('hello', example ?? '대체'); // hello 0
example = '';
console.log('hello', example ?? '대체'); // hello 
example = null;
console.log('hello', example ?? '대체'); // hello 대체
example = undefined;
console.log('hello', example ?? '대체'); // hello 대체

example = 0;
console.log('hello', example || '대체'); // hello 대체
example = '';
console.log('hello', example || '대체'); // hello 대체
example = null;
console.log('hello', example || '대체'); // hello 대체
example = undefined;
console.log('hello', example || '대체'); // hello 대체
```

원시타입이 아닌 것은 `Object` (함수, 배열 포함)

원시타입 - immutable

재할당은 가능한데 할당되었던 원시타입의 값이 바뀌는 것이아니라 새 원시타입의 값이 들어가는 개념

원시타입은 값으로 저장되고 객체들은 참조로 저장된다.

```jsx
// 거짓 같은 값(Falsy, falsey로 쓰이기도 함) 값은 불리언 문맥에서 false로 평가되는 값입니다.

if (false)
if (null)
if (undefined)
if (0)
if (-0)
if (0n)
if (NaN)
if ("")

어제 유효성검사에서 빈값이면 그냥 !enteredName || 로 비교했던거도 falsy라서!
```

1급객체

1. 다른 함수의 인자값으로 넘겨질 수 있다.

2. 변수나 데이터에 할당 가능하다.

3. 객체의 리턴 값으로 리턴 가능하다.

→ 함수를 데이터(string, number, boolean, array, object)다루듯이 다룰 수 있다.

함수 오브젝트에 프로퍼티를 추가하지 않는것이 좋음. 만약 해야한다면 오브젝트를 사용

그래서?

- 고차함수를 만들 수 있다.  → 고차함수는 뒤에 나옴
- 콜백을 사용할 수 있다.

고차함수?

함수를 인자로 받거나 또는 함수를 반환(출력으로)함으로써(return) 작동하는 함수

(Array.prototype.map, Array.prototype.filter, Array.prototype.reduce) → built-in 고차함수

생성자 함수

```jsx
const Foo = function () {
	this.bar = "baz";
};
```

여기서 this는 Foo의 실행컨텍스트와 응답을 주고 받음.

전역 컨텍스트에서 실행시키게되면 전역 실행 컨텍스트시점인 this는 window임

오토박싱

우리가 특정한 원시타입에서 프로퍼티나 메소드를 호출하려 할 떄, 자바스크립트는 이것을 래퍼 오브젝트로 바꾼 뒤에 프로퍼티나 메소드에 접근하려 한다.

원시타입은 프로퍼티를 가질 수 없는데 할당하려고하면 에러 없이 된다 왜냐하면 프로퍼티를 할당할 떄 잠시 원시 타입을 이용한 래퍼 오브젝트를 만들고 거기에 할당하기 때문. (null, undefined 는 에러뜸)

**래퍼 객체**: 일시적으로 임시 객체를 만들어서 메서드나 프로퍼티를 사용할 수 있게 한 후, 역할이 끝나면 다시 원시값으로 돌아온다. 사용이 끝난 래퍼 객체는 가비지 컬렉션의 대상이 된다.

래퍼 객체의 존재이유

**1. 객체의 딜레마**

: 객체는 다양한 프로퍼티와 메서드가 있어서 유용하지만, **무겁고 느리다**는 단점이 있다.

**2. 원시타입의 딜레마**

: 원시타입은 가볍고 빠르지만, 그냥 **값 하나 뿐이라는 단점**이 있다.

**3. 해결책(?)**

: 원시타입을 그대로 쓰자! 대신, **메서드를 호출할 때만 잠깐 객체로** 바꾸자.

즉, 원시타입의 가벼움은 유지하면서, 객체의 유용한 기능도 쓰기 위한 방법인 것이다. 따라서, 특별한 경우를 제외하면, 객체를 따로 생성할 필요 없이, 원시타입을 그대로 사용하는게 권장된다.

### 요약

1. 자바스크립트의 모든 것이 Object(객체)인 것은 아니다.
2. 자바스크립트에는 6개의 원시 타입이 존재한다.
3. 원시 타입이 아닌 것들은 모두 Object(객체)이다.
4. 함수는 단순히 특별한 타입의 Object(객체)일 뿐이다.
5. 함수는 새로운 Object(객체)를 만들기 위해 사용될 수 있다. (생성자 함수)
6. Strings, Booleans, Numbers 는 원시 타입이면서 오브젝트이다. (래퍼 오브젝트를 갖는다.)
7. 자바스크립트 내부에 존재하는 오토박싱(Autoboxing)이라는 기능 때문에 몇몇 원시 타입들 (**Strings, Numbers, Booleans**) 는 Object(객체)처럼 동작한다.

`Infinity` , `NaN`  → ES5 부터 수정할 수 없는 읽기전용 상수로 바뀌었습니다.

어떤 수를 0으로 나누었을때 Infinity

`symbol`

은 함수를 통해 생성할 수 있으며 호출 될 때마다 고유한 값을 생성한다.

변경 불가능한 원시 타입의 값이며, 다른 값과 중복되지 않는 고유한 값

주로 다른 값과 충돌을 피하기위해 상수 값과 같은 문자열을 만들때 사용된다

심볼 값도 객체처럼 메서드를 사용하면 암묵적으로 *래퍼 객체를 생성한다. description 프로퍼티와 toString은 Symbol.prototype의 프로퍼티다. 심볼 값은 문자열이나 숫자 타입으로 변환되지 않는다. 단 불리언 타입으로는 타입 변환이 된다.

Usage

**1. 심볼과 상수: 자바스크립트에서 enum 사용하기**

**2. 심볼과 프로퍼티 키: 프로퍼티 은닉하기**

**3. 심볼과 표준 빌트인 객체 확장**

**4. Well-known Symbol: 표준 확장 또는 이터러블 타입 체킹**

### 원시형 타입 선언시 메모리 동작원리

---

변수영역과 데이터 영역에 따로 할당한다. 

- **변수 영역에 직접 값을 저장 할 경우**
    
    500 개 변수 * 8바이트(Number 자료형) = 4000 바이트
    
- **데이터 영역에 저장하고 주소를 저장할 경우**
    
    500 개 변수 + 8바이트(Number 자료형) = 1008 바이트
    
    무려 4배나 차이가 나게 되는데 이러한 부분을 보면 변수의 값 부분에 데이터를 바로 넣는 것보다 메모리 주소를 넣는 것이 더 효율적이라고 할 수 있다.
    

### Object.freeze()

---

Object.freeze는 동결된 객체를 반환할 뿐 재할당을 허용한다. (let 사용시) 

const 사용시에는 재할당, 속성변경이 불가능함
