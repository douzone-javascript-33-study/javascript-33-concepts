# 5. == vs === vs typeof

## 1. === 연산자

- 형변환X
- call stack에 있는 값으로만 비교
    - reference type은 내용이 같은 객체라도 주소가 다르면 `false`

## 2. == 연산자

- 형변환해서 비교
- 비교하는 두 타입이 다르다면 대부분 숫자로 형변환해서 비교
    - object는 string으로 먼저 변환하기는 함
- call stack에 있는 값으로만 비교
    - reference type은 내용이 같은 객체라도 주소가 다르면 `false`

### 2-1. 연산 방식

<img src="https://cdn.filestackcontent.com/eTIpVrOQcqBNTN6Ma8i4" width="600px" />

- 먼저 type이 같은지부터 검사함
    - 같을 때
        - 기본적으로 call stack에 담긴 값을 비교함
            - 둘 다 같은 원시 타입(primitive type)류인 경우 : 값이 같은지 비교
                - undefined, null ( undefined와 null은 같다고 침 ) 끼리 비교
                    - `undefined == null` : `true`
                - number 형 끼리 비교
                    - `1 == 1` : `true`
                    - `NaN` 은 number 형이긴 한데 아무것도 같지 않음
                        - `NaN == NaN` : `false`
                - string 형 끼리 비교
                - boolean 형 끼리 비교
                - symbol 형 끼리 비교
                    - `Symbol(1) == Symbol(1)` : `false`
                - big int 형 끼리 비교
            - 둘 다 같은 참조 타입(reference type)류인 경우 : 주소가 같은지 비교
                - 따라서 `{ num: 1 } == { num: 1 }` 결과값은 `false`
                - 주소 복사인 경우 비교한다면 `true`
                    
                    ```jsx
                    const a = {};
                    const b = a;
                    
                    console.log(a == b); // true
                    ```
                    
    - 다를 때
        1. primitive type으로 변환 (object인 경우)
            
            1) `valueOf()` 사용해서 reference type이면 2) 수행
            
            2) `toString()` 사용
            
        2. number형으로 변환 (`Number(input)`)
            - `undefined` → `NaN`
            - `null` → 0
            - `boolean` → `true` 면 1, `false` 면 0
            - `string` → parse해서 number형 반환, number형이 아니면 `NaN`
                - `""` 는 `0` 으로 변환
- 예시
    - `[] == 0` → `"" == 0` → `0 == 0` → `true`
    - `[] == "0"` → `"" == "0"` → `false`
    - `false == 1` → `0 == 1` → `false`
    - `{} == false` → `{} == 0` → `"[object Object]" == 0` → `NaN == 0` → `false`
    - `undefined == false` → `undefined == 0` → `false`
    - `[1,2,3] == 123` → `"1,2,3" == 123` → `NaN == 123` → `false`
    - `[123] == 123` → `"123" == 123` → `123 == 123` → `true`
    - 객체 x의 toString, valueOf overriding
        
        ```jsx
        var x = {
          a: '...',
          toString: function () {
            return false;
          },
          valueOf: function () {
            return new Boolean(true); // 객체임!!
          }
        };
        
        console.log(x == "0"); // true
        //x.valueOf():객체 -> x.toString(): false -> false == "0" -> 0 == "0" -> 0 == 0
        ```
        
        ```jsx
        const x = {
            a: '...',
            valueOf: function () {
                return true;
            },
            toString: function () {
                return false;
            },
        };
        
        console.log(x == "0"); // false
        //x.valueOf() : true -> true == "0" -> 1 == "0" -> 1 == 0
        ```
        

## 3. typeof

```jsx
// primitives
console.log(typeof 3)            // number
console.log(typeof "abc")        // string
console.log(typeof true)         // boolean
console.log(typeof undefined)    // undefined
console.log(typeof null)         // object  !!
console.log(typeof Symbol(2))    // symbol
console.log(typeof 1n)           // bigint

console.log(typeof NaN)          // number  !!
  
// references  
console.log(typeof {name: 1})    // object
console.log(typeof [1,2,3])      // object  !!
console.log(typeof function(){}) // function

console.log(typeof new String(1)) // object !!
```

- 배열을 object라고 반환함
    - Array를 확인하고 싶을때?
        - `instanceof` 사용 가능 : `[1,2,3] instanceof Array`
            - 참고로 primitive type은 `instanceof` 사용 불가능
                - `3 instanceof Number` : `false`
            - cross-window 문제가 있음. 따라서 쓰는 것 별로 좋지는 않음
        - `constructor` 사용 가능 : `[1,2,3].constructor === Array`
        - `Array.isArray([1,2,3])` 사용
- `null` 을 object라고 반환함 : 이거는 그냥 에러
    - 객체의 key가 존재하는지 확인하고 싶을 때?
        - `in` 사용
            
            ```jsx
            var obj1 = {}
            var obj2 = {
              key: undefined
            }
            
            // key의 여부를 알 수 없음
            console.log(obj1.key) // undefined
            console.log(obj2.key) // undefined
            
            // key의 여부를 아는 방법?
            onsole.log('key' in obj1) // false
            console.log('key' in obj2) // true
            ```
            
        - 더 좋은 방법 : `hasOwnProperty` 사용 (`obj.hasOwnProperty(key)`)
            - Object가 이미 가지고 있는 key인 경우(`constructor` 처럼) 오브젝트 내에서 새로 정의한건지 `in` 으로는 모름
- Wrapper 객체도 object로 반환함
    - Wrapper 객체가 뭘 감싼건지 알고 싶을때?
        - `instanceof` 사용
        - `constructor` 사용
- 숫자의 값이 있는지, 무한하지 않은지 확인할 때?
    - `isFinite()`  추가로 사용 (`NaN` 과 `Infinity` 를 `false`로 반환함)

## 4. 결론

- `===` 쓰자
    - `==`  : 복잡한 형변환 규칙으로 결과 예측이 힘들다.
- 타입 검사시에 `typeof` 는 완전하지 않으므로 `instanceof` 나 `constructor` 등 다른 방법도 쓸 수 있다.

## 참고

- == 연산자 동작 방식
    
    [https://www.codementor.io/javascript/tutorial/double-equals-and-coercion-in-javascript](https://www.codementor.io/javascript/tutorial/double-equals-and-coercion-in-javascript)
    
- typeof
    
    [https://webbjocke.com/javascript-check-data-types/](https://webbjocke.com/javascript-check-data-types/)
    
    [https://tomeraberba.ch/html/post/checking-for-the-absence-of-a-value-in-javascript.html](https://tomeraberba.ch/html/post/checking-for-the-absence-of-a-value-in-javascript.html)
