왜 배열리터럴로 생성하는걸 권장?

배열을 생성할 때 Array(1, 2, 3, 4, 5)와 같이 생성해도 되지만 [1, 2, 3, 4, 5]와 같이 선언하라는 의미다. 개인적으로 전자와 같은 문법을 좋아하는데 배열 생성자가 의도하지않은 결과를 반환하지 않을 수 있다고 한다.

객체도 

객체 리터럴 방식이 있다면 생성자 함수 방식을 쓸 필요 없지만 생성자 함수 방식이 가지는 기능이 무엇인지는 알아야한다. 바로 인자를 넘길 수 있다는 것이다. 이것이 생성자 함수 방식의 문제이다. 인자에 따라서 원하는 결과와 다른 결과가 나올 수 있기 때문이다. 다시 말하지만 new Object 대신 객체 리터럴을 사용하라.

```jsx
var o = new Object();
console.log(o.constructor); // function Object() { [native code] }

var o = new Object(1);
console.log(o.constructor); // function Number() { [native code] }
console.log(o.toString(10)); // 1

var o = new Object("혁진");
console.log(o.constructor); // function String() { [native code] }
console.log(o.length); // 2

var o = new Object(true);
console.log(o.constructor); // function Boolean() { [native code] }

출처: https://itmining.tistory.com/73 [IT 마이닝]
```

shift 배열에서 제거한 요소. 빈 배열의 경우 `[undefined](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined)` 를 반환합니다.

unshift 맨앞에 요소추가 후 새로운 배열 길이 반환

push 맨 끝에 요소추가 후 새로운 배열 길이 반환

호이스팅

함수 선언 방식

함수 선언식

함수 표현식

- 장점
    
    클로저로 사용
    
    콜백으로 사용 (다른 함수의 인자로 넘길 수 있음)
    

배열할당 [], push()맨 마지막, unshift() 맨앞

최적화 방법 : 배열을 사용할 때는 리터럴 형식으로 객체를 생성하고 Array.push( ) 메서드보다는 접근자[ ]를 사용해 데이터를 추가하는 코드를 작성하는 것이 좀 더 최적화된 배열 사용법입니다.

### 객체

---

객체 리터럴 도 마찬가지

```jsx
let o = {
	'': '' // 키로 빈 문자열 사용 가능
}
```

- 프로퍼티 키에 **문자열** 또는 **심벌** 값이 아닌 값들을 사용할 경우 암묵적으로 문자열로 타입 변환이 이뤄진다.
- 이미 존재하는 프로퍼티 키를 중복 선언할 경우 마지막으로 선언한 프로퍼티 가 노출된다.
