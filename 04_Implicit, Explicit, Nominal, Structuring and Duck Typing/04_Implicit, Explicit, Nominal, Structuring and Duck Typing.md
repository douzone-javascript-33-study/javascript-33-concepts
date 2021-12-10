
### 형변환

+ 프로그램을 작성하면서 문자를 숫자로, 숫자로 문자로 변환해야하는 작업이 생긴다.

```javascript
let num = 10
console.log(num, typeof num) // 10 "number"

num = num.toString()
console.log(num, typeof num) // 10 "string"

num = parseInt(num)
console.log(num, typeof num) // 10 "number"
```

+ parseInt나 toString 같은 함수를 이용해서 형변환을 할 수 있다.
+ 하지만 JavaScript 에서 형변환을 하는 방법으로는 명시적 변환과 암시적 변환이 있다.
+ JavaScript 에서는 사용하지는 않지만 타입 검사 방법으로 Nominal, Structural, Duck 타이핑이 존재 한다.

### 명시적 변환

+ 명시적 변환은 개발자가 의도적으로 형변환을 하는 것이다.
+ 기본적인 형변환은 Object(), Number(), String(), Boolean() 과 같은 함수를 이용한다.

```javascript
let variable = 100

console.log(variable, typeof variable) // 100 "number"

variable = Object(variable)
console.log(variable, typeof variable) // Number {100} "object"

variable = String(variable)
console.log(variable, typeof variable) // 100 "string"

variable = Boolean(variable)
console.log(variable, typeof variable) // true "boolean"
```

+ Object(), Number(), String(), Boolean()과 같은 함수는 생성자 함수 이다. 하지만 new 연산자가 없으면 형변환에 사용된다.

#### Number Type 으로 변환하기

1. Number()

```javascript
console.log(Number('100000'), typeof Number('100000')) // 100000 "number"
console.log(Number('5' * 5), typeof Number('5' * 5)) // 25 "number"
console.log(Number('3.14'), typeof Number('3.14')) // 3.14 "number"
console.log(Number('a'), typeof Number('a')) // Nan "number"
console.log(Number(true), typeof Number(true)) // 1 "number"
console.log(Number(false), typeof Number(false)) // 0 "number"
console.log(Number(() => {}), typeof Number(Number(() => {}))) // NaN "number"
```

+ 정수형과 실수형 데이터를 숫자로 변환하여 숫자 데이터가 아닌 것은 Nan을 반환한다.
+ Boolean 데이터인 true와 false 는 각각 1과 0으로 변환 된다.

2. parseInt()

```javascript
console.log(parseInt('100000'), typeof parseInt('100000')) // 100000 "number"
console.log(parseInt('3.14'), typeof parseInt('3.14')) // 3 "number"
console.log(parseInt('a'), typeof parseInt('a')) // NaN "number"
console.log(parseInt(0033), typeof parseInt(0033)) // 27 "number"
console.log(parseInt('0033'), typeof parseInt('0033')) // 33 "number"
console.log(parseInt(0x1b), typeof parseInt(0x1b)) // 27 "number"
console.log(parseInt('0x1b'), typeof parseInt('0x1b')) // 27 "number"
console.log(parseInt(true), typeof parseInt(true)) // NaN "number"
console.log(parseInt(false), typeof parseInt(false)) // NaN "number"
console.log(parseInt(() => {}), typeof parseInt(() => {})) // NaN "number"
console.log(parseInt('    2'), typeof parseInt('    2')) // 2 "number"
console.log(parseInt('    2  '), typeof parseInt('    2  ')) // 2 "number"
console.log(parseInt('    2  ㄴ2'), typeof parseInt('    2  ㄴ2')) // 2 "number"
console.log(parseInt('      ㄴ2'), typeof parseInt('      ㄴ2')) // Nan "number"
```

+ parseInt() 함수는 정수형의 숫자로 변환된다.
+ 문자열이 숫자 0으로 시작시 8진수로 인식하고 0x, 0X로 시작시 16진수로 인식한다.
+ 또한 숫자가 아닌 데이터가 먼저 포함된 문자열이 들어올 경우 Nan을 반환한다.
+ 뒷부분에 공백이나 숫자가 아닌 데이터가 들어올 경우 앞의 데이터만 반환한다.
+ Number()와 다르게 Boolean값인 true 와 false 또한 Nan을 반환한다.

3. parseFloat()

```javascript
console.log(parseFloat('100000'), typeof parseFloat('100000')) // 100000 "number"
console.log(parseFloat('3.14'), typeof parseFloat('3.14')) // 3.14 "number"
console.log(parseFloat('a'), typeof parseFloat('a')) // NaN "number"
console.log(parseFloat(0033), typeof parseFloat(0033)) // 27 "number"
console.log(parseFloat('0033'), typeof parseFloat('0033')) // 33 "number"
console.log(parseFloat(0x1b), typeof parseFloat(0x1b)) // 27 "number"
console.log(parseFloat('0x1b'), typeof parseFloat('0x1b')) // 0 "number"
console.log(parseFloat(true), typeof parseFloat(true)) // NaN "number"
console.log(parseFloat(false), typeof parseFloat(false)) // NaN "number"
console.log(parseFloat(() => {}), typeof parseFloat(() => {})) // NaN "number"
console.log(parseFloat('    2'), typeof parseFloat('    2')) // 2 "number"
console.log(parseFloat('    2  '), typeof parseFloat('    2  ')) // 2 "number"
console.log(parseFloat('    2  ㄴ2'), typeof parseFloat('    2  ㄴ2')) // 2 "number"
console.log(parseFloat('      ㄴ2'), typeof parseInt('      ㄴ2')) // Nan "number"
```

+ parseFloat() 함수는 실수형의 숫자로 변환된다.
+ parseInt()와 비슷하지만 16진수 문자열 데이터 0x27의 경우 0을 반환한다.

#### String Type으로 변환하기

1. String

```javascript
console.log(String(10000), typeof String(10000)) // "10000" "string"
console.log(String(3.14), typeof String(3.14)) // "3.14" "string"
console.log(String(true), typeof String(true)) // "true" "string"
console.log(String(false), typeof String(false)) // "false" "string"
console.log(String(() => {}), typeof String(() => {})) // "() => {}" "string"
console.log(String({ foo: 'bar' }), typeof String({ foo: 'bar' })) // "[object Object]"
```

+ number나 boolean 데이터 그리고 () => {} 같은 함수도 문자열로 바뀌는 것을 확인할 수 있다.
+ {foo: "bar"}와 같은 객체도 string으로 변환 되긴 하지만  [object Object] 와 같이 표시 된다.

2. toString()

```javascript
console.log((10000).toString(), typeof (10000).toString()) // "10000" "string"
console.log((10000).toString(2), typeof (10000).toString(2)) // "10011100010000" "string"
console.log((10000).toString(8), typeof (10000).toString(8)) // "23420" "string"
console.log((3.14).toString(), typeof (3.14).toString()) // "3.14" "string"
console.log(true.toString(), typeof true.toString()) // "true" "string"
console.log(false.toString(), typeof false.toString()) // "false" "string"
console.log((() => {}).toString(), typeof (() => {}).toString()) // "() => {}" "string"
console.log({ foo: 'bar' }.toString(), typeof { foo: 'bar' }.toString()) // "[object Object]" "string"
```

+ toString() 함수도 String()과 비슷하지만 number데이터를 변환할 때 진수를 지정할 수 있다
+ 인자를 전달하지 않으면 기본적으로 10진수 값으로 number 데이터를 String으로 변환한다.

3. toFixed()

```javascript
console.log((10000).toFixed(), typeof (10000).toFixed()) // "10000" "string"
console.log((10000).toFixed(2), typeof (10000).toFixed(2)) // "10000.00" "string"
console.log((10000).toFixed(3), typeof (10000).toFixed(8)) // "10000.000" "string"
console.log((3.14).toFixed(), typeof (3.14).toFixed()) // "3" "string"
console.log((3.14).toFixed(1), typeof (3.14).toFixed()) // "3.1" "string"
console.log((3.16).toFixed(1), typeof (3.16).toFixed()) // "3.2" "string"
```

+ toFixed() 는 number 데이터에만 사용할 수 있다.
+ 인자에 주는 값은 인자의 값만큼 소수점 자리수를 표현한다.

#### Boolean Type 으로 변환하기

+ Boolean()

```javascript
Boolean(100); //true
Boolean(“1”); //true
Boolean(true); //true
Boolean(Object); //true
Boolean([]); //true
Boolean(0); //false
Boolean(NaN); //false
Boolean(null); //false
Boolean(undefined); //false
```

+ Boolean으로 변환하기 위해서는 Boolean()을 사용한다. 
+ 0, Nan, null, undefined 가 아닌 값들은 모두 true로 변환된다.

### 암시적 변환

+ 암시적 변환은 자바스크립트 엔진이 자동으로 데이터타입을 변환시키는 것이다.

```javascript
let num = 10
let str = '10'

console.log(num + str, typeof (num + str)) // "1010" "string"
```

+ 위와 같은 예제가 암시적 변환의 예시이다.

+ 일반적인 언어에서 타입이 다른 값들의 연산은 지원하지 않지만 자바스크립트는 가능하다.자바스크립트가 타입에 대하여 상당히 유연한 언어인 이유 중에 하나일 것이다.
+ 암시적 변환은 산술 연산자와 동등 연산자를 사용할 때 변환이 발생한다.

#### 산술 연산자에서의 암시적 변환

+ 더하기 연산자

  + 더하기 연산자에서는 문자의 우선순위가 숫자보다 높다.
  + 객체와 함수또한 문자보다 우선순위가 낮다.

+ Number + String

  ```javascript
  console.log(10 + '10', typeof (10 + '10')) // "1010" "string"
  console.log(10 + 'abc', typeof (10 + 'abc')) // "10abc" "string"
  console.log('10' + 10, typeof ('10' + 10)) // "1010" "string"
  console.log('abc' + 10, typeof ('abc' + 10)) // "abc10" "string"
  console.log(10 + 'abc' + 10, typeof (10 + 'abc' + 10)) // "10abc10" "string"
  ```

+ String + Boolean

  ```javascript
  console.log('abc' + true, typeof ('abc' + true)) // "abctrue" "string"
  console.log('abc' + false, typeof ('abc' + true)) // "abcfalse" "string"
  console.log(true + 'abc', typeof (true + 'abc')) // "trueabc" "string"
  console.log(false + 'abc', typeof (false + 'abc')) // "falseabc" "string"
  console.log(true + 'abc' + false, typeof (true + 'abc' + false)) // "trueabcfalse" "string"
  ```

+ String + Object

  ```javascript
  console.log('abc' + { foo: 'bar' }, typeof ('abc' + { foo: 'bar' })) // "abc[object Object]" "string"
  console.log('abc' + (() => {}), typeof ('abc' + (() => {}))) // "abc() => {}" "string"
  ```

+ 그 외 연산자(-, *,  /, %)

  + 더하기 연산자를 제외한 연산자에서는 숫자의 우선순위가 문자보다 높다.
  + 숫자가 아닌 문자열이 들어갈 경우 연산이 불가능해 Nan이 반환된다.

+ Number * String

  ```javascript
  console.log(10 * '10', typeof (10 * '10')) // 100 "number"
  console.log(10 * 'abc', typeof (10 * 'abc')) // Nan "number"
  console.log('10' * 10, typeof ('10' * 10)) // 100 "number"
  console.log('abc' * 10, typeof ('abc' * 10)) // Nan "number"
  console.log(10 * 'abc' * 10, typeof (10 * 'abc' * 10)) // Nan "number"
  ```

+ Number - String

  ```javascript
  console.log(10 - '10', typeof (10 - '10')) // 0 "number"
  console.log(10 - 'abc', typeof (10 - 'abc')) // Nan "number"
  console.log('10' - 10, typeof ('10' - 10)) // 0 "number"
  console.log('abc' - 10, typeof ('abc' - 10)) // Nan "number"
  console.log(10 - 'abc' - 10, typeof (10 - 'abc' - 10)) // Nan "number"
  ```

+ Number % String

  ```javascript
  console.log(10 % '10', typeof (10 % '10')) // 0 "number"
  console.log(10 % 'abc', typeof (10 % 'abc')) // Nan "number"
  console.log('10' % 10, typeof ('10' % 10)) // 0 "number"
  console.log('abc' % 10, typeof ('abc' % 10)) // Nan "number"
  console.log((10 % 'abc') % 10, typeof ((10 % 'abc') % 10)) // Nan "number"
  ```

+ Number(-, *,  /, %) Boolean

  ```javascript
  console.log(10 * true, 10 * false) // 10 0
  console.log(10 - true, 10 - false) // 9 10
  console.log(10 / true, 10 / false) // 10 Infinity
  console.log(10 % true, 10 % false) // 0 Nan
  ```

+ Boolean 타입의 경우 Number와 연산이 될 경우 true는 1, false는 0으로 계산

#### 동등 연산자에서의 암시적 변환

+ == 연산자를 사용할 경우에도 암시적 변환이 발생한다.

  ```javascript
  console.log(0 == '0') // true
  console.log(0 == false) // true
  console.log('0' == false) // true
  console.log(undefined == null) // true
  console.log('' == false) // true
  console.log('' == 0) // true
  console.log('' == '0') // false
  ```

  + Number 타입인 0과 String 타입인 "0"은 == 연산자를 사용할 경우 같다.
  + 0 과 "0" 은 Boolean 타입인 false와 같다는 것을 확인할 수 있다.
  + 비어있는 문자열인 ""은 fales와 0 과는 같지만 문자열 "0"과는 다르다.

  ```javascript
  console.log(1 == '1') // true
  console.log(1 == true) // true
  console.log('1' == true) // true
  ```

  + 1과 "1" , true도 동일한 관계를 갖는다.
  + 타입에 엄격하지 않은 == 연산자를 대체하여 엄격한 === 연산자를 사용해 동등 비교 한다.

### 명칭적 타이핑(Nominal Typing)

+ 명칭적 타이핑은 특정 키워드를 통하여 타입을 지정해 사용하는 방식이다.

  ```javascript
  int num = 10;
  char str = "a";
  
  num = str; // ERROR!!
  num = "a"; // ERROR!!
  str = 10; // ERROR!!
  ```

  + num  은 int 형으로 str은 char 형으로 선언 되었다.
  + 서로 타입이 맞지않는 값을 대입연산자를 이용해 대입하면 에러가 발생한다.

  ```javascript
  class Foo {};
  class Bar {};
  
  Foo foo = new Bar(); //ERROR
  ```

  + 클래스에서도 Foo와 Bar은 서로 호환이 불가능한 클래스 이다.

  ```javascript
  class Foo {};
  class Bar extends Foo {};
  
  Foo foo = new Bar();
  ```

  + extends를 이용해 서로 클래스 간의 상호 호환을 명시하면 클래스를 사용할 수 있다.

### 구조적 타이핑(Structural Typing)

+ 구조적 타이핑은 맴버에 따라 타입을 검사하는 방법이며 명칭적 타이핑과 반대되는 방법으로 TypeScript, Go 등에서 사용 된다.

+ 구조적 타이핑은 두 데이터의 타입 구조를 비교하여 호환되는 타입인지 검사한다.

+ 한 타입이 다른 타입이 갖는 맴버를 모두 가지고 있을 경우 두 타입은 호환되는 타입이다.

  ```javascript
  class Foo {
      public test(): void{}
  }
  
  class Bar {
      public test(): void{}
  }
  
  const foo: Foo = new Bar();
  ```

### 덕 타이핑(Duck Typing)

+ 덕 타이핑(Duck Typing)은 객체의 변수 및 메소드 집합이 객체의 타입을 결정하는 것이다.

+ 덕 타이핑(Duck Typing)이란 용어는 덕 테스트 에서 유래했다. => "어떤 새가 오리처럼 걷고, 헤엄치고, 소리를 낸다면 그 새를 오리라고 부를 것이다."

```javascript
class Pelican {
  walk() {
    console.log("Pelican walk");
  }

  quack() {
    console.log("Pelican quack");
  }

  dive() {
    console.log("Pelican dive");
  }
}

class Duck {
  walk() {
    console.log("Duck walk");
  }

  quack() {
    console.log("Duck quack");
  }

}

class Platypus {
  walk() {
    console.log("Platypus walk");
  }

  growl() {
    console.log("Platypus growl");
  }
}

function checkDuck(testObj) {
  if (typeof testObj.walk == "function" && typeof testObj.quack == "function") {
    return true;
  }
  return false;
}

let duck = new Duck();

let pelican = new Pelican();

let platypus = new Platypus();

console.log("Pelican is of Duck type: " + checkDuck(pelican)); //true
console.log("Duck is of Duck type: " + checkDuck(duck)); //true
console.log("Platypus is of Duck type: " + checkDuck(platypus)); //false
```

+ TypeScript 예시

```typescript
interface People {
    talk(): void;
    whoAmI: string;
}

class Human implements People {
    whoAmI = "human"
    talk = () => {
        console.log(`say ${this.whoAmI} : 말할 수 있어요`);
    }
}

class Robot {
    whoAmI = "robot"
    talk  = () => {
        console.log(`say ${this.whoAmI} : 말할 수 있어요`);
    }
}

const humanInstance = new Human(); 
const robotInstance = new Robot();

function startTalk(people: People): void {
    people.talk();
}

startTalk(humanInstance); // --- 1) "say human : 말할 수 있어요"
startTalk(robotInstance); // --- 2) "say robot : 말할 수 있어요"
```

