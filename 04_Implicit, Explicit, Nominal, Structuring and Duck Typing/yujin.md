# 4. Implicit, Explicit, Nominal, Structuring and Duck Typing

## 1. 형변환

### 1-1. 일반적인 변환 방식

- 원시 타입 → Number
    - string → number로 변환되는 것 이외에 NaN
    - booleans → true : 1, false : 0
    - null → 0
    - undefined → NaN
- 원시 타입 → booleans
    - numbers → 0, NaN 이외에는 true
    - string → '' 이외에는 true
    - null → false
    - undefined → false
- 참조 타입(objects : object, function, array) → ?
    - number 로 변환 : valueOf() 사용
    - string 로 변환 : toString() 사용
    - boolean 로 변환 : 항상 true
    

### 1-2. operator에서 암시적 형변환

- logical operator (`&&`, `||`)
    - 검사할 당시에는 boolean으로 암시적으로 형변환(implicitly convert)
    - 결과값은 형변환한 boolean이 아닌 형변환 전의 값을 return함
    - ex
        
        ```jsx
        const value = 0 || 'apple';
        const value2 = 'apple' || 0;
        const value3 = 0 && 'apple';
        
        console.log(value, value2, value3); //apple apple 0
        ```
        
- mathmatical operator( `+`, `-`, `*`, `%`)
    - mathmatical  operand와 함께 쓰이는 경우 숫자로 암시적 형변환 일어남
    - `-` , `*` , `%`
        - 모든 타입 → 숫자로 형변환
        
        ```jsx
        const value = null - 5 + true;
        console.log(value); // 6 (0 + 5 + 1)
        ```
        
    - `+`
        - 문자열 > 숫자
            - 문자열 + 모든 타입(숫자 포함) → 문자열 (숫자 → 문자로 형변환)
            - 숫자 + 숫자로 변환되지 않는 타입 → 문자열 (숫자를 문자로 형변환)
            - 숫자 + 숫자로 변환되는 타입 → 숫자
        - 숫자나 문자열이 아닌 타입끼리 연산하는 경우
            - 숫자 친화적 타입 → 숫자로 변환후 연산
                - boolean, null, undefined끼리만 연산하면 숫자로 변환
            - 문자 친화적 타입 → 문자로 변환후 연산
                - function, object, array가 하나라도 있으면 모두 문자로 변환
            - 나머지는 모두 문자열로 변환
        
        ```jsx
        const func = () => {};
        const num = 1;
        const str = 'str';
        const bool = true;
        const null_ = null;
        const undefined_ = undefined;
        
        console.log(func + func) // 문자열 변환 : () => {}() => {}
        console.log(num + func) // 문자열 변환 : 1() => {}
        console.log(str + num) // 문자열 변환 : 1str
        console.log(bool + func) // 문자열 변환 : true() => {}
        console.log(undefined_ + str) // 문자열 변환 : undefinedstr
        
        console.log(bool + bool) // 숫자 변환 : 2
        console.log(null_ + null_); // 숫자 변환 : 0
        console.log(undefined_ + undefined_) // 숫자 변환 : NaN
        console.log(null_ + undefined_) // 숫자 변환 : NaN
        ```
        
- relational operator ( `<` , `>` , `≤` , `≥` )
    - number로 암시적 형변환 ( date 까지 )
        - `null`도 0으로 형변환
    - string 끼리 : 알파벳 순서 비교
    - NaN 이 operand에 있으면 항상 false
        - `console.log(undefined < 1)` : `false`
- equality operator ( `==`, `!=` )
    - **비교 타입이 다른 경우** 한 쪽을 암시적 타입 변환해서 비교
        - NaN이 operand에 있으면 항상 false
        - null 은 0이 아닌 undefined로 변환됨
        
        ```jsx
        const func = () => {};
        const undefined_ = undefined;
        
        console.log(undefined_ == Number(func)) // false
        
        console.log(null >= 0) // true (null -> 0)
        console.log(null == 0) // false (null -> undefined)
        ```
        
    

### 1-3. 추가 형변환 관련

- `if` vs `switch`
    - if
        - 표현식에 있는 부분이 boolean으로 값이 나오지 않는 경우, 암시적 형변환함
    - switch
        - case 에 갈 때 형변환 X
    
    ```jsx
    const value = 'string';
    
    if(value){
        console.log('if 통과') // 실행 -> 암시적 형변환 일어남
    } else {
        console.log('if 통과 X')
    }
    
    switch (value){
        case true:
            console.log('switch 통과')
    				break;
        default :
            console.log('switch 통과 X') // 실행 -> 암시적 형변환 일어나지 않음
    }
    ```
    

## 2. Nominal VS. Structural VS. Duck Typing

- 쓰이는 언어 비교
    - Nominal Typing : Java, C++
    - Structural Typing : TypeScript
    - Duck Typing : JavaScript, Python, Ruby (동적인 언어에서 사용)
    
- 정적 VS. 동적 타입 체커
    - 정적 타입 체커 : Nominal Typing, Structural Typing
        - 실행 전에 타입을 체크해서 에러 보냄
    - 동적 타입 체커 : Duck Typing
        - 실행 후에 method들을 확인하여 타입을 정한다.
        - 따라서 런타임 에러가 타입으로 인해 일어날 수 있다.

- 코드의 간결성
    - Duck Typing > Structural Typing > Nominal Typing

### 2-1. Nominal Typing (명칭적 타이핑)

- nominal typing : 특정 키워드(`int`, `char`)를 통해서 타입 지정해서 사용
    - 보통 C, C++, Java등의 언어에서 사용
    - **이름** 으로 검사
    - 키워드(이름)이 다르면 그냥 다른 타입
- nominal typing으로 type 검사
    
    ```java
    int num = 10;
    char str = "a";
    
    num = str; // error
    num = "a"; // error
    str = 10; // error
    ```
    

### 2-2. Structural Typing (구조적 타이핑)

- Structural Typing: 변수가 가져야할 타입 구조를 적음
    - TypeScript에서 사용 : 컴파일 타임에 Duck Typing방식을 적용
    - 타입 구조를 비교해서 호환되는 타입인지 검사한다.
        
        ```jsx
        const message: string = 1; // error - 호환X : message는 string type 구조, 1은 number type 구조
        const message2: string = 'hello world';
        
        const messages: string[] = ['hello','world'];
        ```
        
    - 한 타입이 다른 타입이 가지는 멤버를 모두 가지는 경우 호환되는 타입!
        
        ```jsx
        interface People {
        	name: string
        }
        
        const people: People;
        const p = {name : 'yujin', location: 'busan'}
        people = p;
        ```
        
        - `p`가 가지는 `string` type의 `name` 을 people도 동일한 구조로 가진다. 따라서 people에 p를 대입할 수 있다.

### 2-3. Duck Typing

- Duck Typing : 객체의 **변수 및 메소드 집합** 이 **객체의 타입**을 결정
    - JavaScript, Python, Ruby등의 언어에서 사용
    - "어떤 새가 꽥꽥 울고, 뒤뚱뒤뚱 걷는다면 그 새는 오리라고 간주한다."
        - 어떤 새의 이름이 '짹짹이'든 '멍멍이'든 **이름**과는 상관없이 그 새의 **행동**을 보고 어떠한 타입이라고 결정하는 것
        - 어떠한 객체의 이름 상관없이 변수가 어떠한 행동(함수등등)이 똑같다면 같은 객체로 간주한다는 것
        
        ```jsx
        class Duck{
          sound(){
        		console.log("꽥꽥");
        	}
        }
        
        class Dog{
          sound(){
        		console.log("멍멍");
        	}
        }
        
        function get_sound(animal){
        	animal.sound();
        }
        
        bird = Duck()
        dog = Dog()
        
        get_sound(bird)
        get_sound(dog)
        ```
        
        - Nominal이나 Structural typing에서는 Dog와 Duck를 다른 타입으로 간주하고 get_sound의 파라미터로 animal이 전달이 되지 않고, 실행이 되지 않을 것이다. 이 두 typing에서는 Duck과 Dog가 같은 타입으로 간주되려면 상속이나 interface등이 필요하다.
        - Duck Typing을 쓰는 JavaScript의 경우에는 Duck과 Dog의 행동(sound 라는 함수 둘다 존재)이 같기 때문에 같은 타입이라고 생각해서 animal에 Duck이 들어갈 수도 있고,Dog가 들어갈 수 도 있다.
        - Duck Typing은 Nominal이나 Structural에 비해 **코드를 간결화할 수 있는 장점**이 있다. 하지만, 그만큼 **실행시 오류가 발생**할 수 있다. 그래서 **테스트 코드를 작성하는 것이 좋다.**
- TypeScript 를 JavaScript로 변환?
    - TypeScript
        
        ```jsx
        interface People {
        	name: string
        }
        
        let people: People;
        const p = {name : 'yujin', location: 'busan'}
        people = p;
        
        console.log(people);
        ```
        
    - JavaScript
        
        ```jsx
        "use strict";
        let people;
        const p = { name: 'yujin', location: 'busan' };
        people = p;
        console.log(people);
        ```
        
    - JavaScript에서는 interface가 필요없는 것을 볼 수 있다.
- 예제
    
    ```jsx
    calculate = (a,b,c) => a + b + c;
    
    console.log(calculate(1,2,3))                   // 6
    console.log(calculate([1,2,3],[4,5,6],2))       // 1,2,34,5,62
    console.log(calculate('apple',' orange ',3))    // apple orange 3
    ```
    
    - a,b,c가 무엇이든 간에 인자로 넘겨줄 수 있다. 이를 위해서 따로 interface등을 지정할 필요가 없음
- 결론
    - 장점 : JavaScript적인 프로그래밍은 두 타입이 같은지 보기위해서의 interface, 상속등이 필요가 없다. 따라서 interface, 상속으로 인한 종속성관련 문제가 Nominal typing 보다 적다. (기능을 확장하기 위해 interface등을 사용하기는 한다.하지만 그게 타입을 같게하려고 하는 것이 아님) 타입은 나중에 생각한다.
    - 단점 : 하지만 그만큼 TDD가 중요한 언어

## 참고

### Nominal typing, Structural Typing

[https://velog.io/@vlwkaos/Structural-vs-Nominal-Subtyping-그리고-TypeScript](https://velog.io/@vlwkaos/Structural-vs-Nominal-Subtyping-%EA%B7%B8%EB%A6%AC%EA%B3%A0-TypeScript)

[https://alstn2468.github.io/Javascript/2020-05-11-Implicit_Explict_Nominal_Structuring_DuckTyping/](https://alstn2468.github.io/Javascript/2020-05-11-Implicit_Explict_Nominal_Structuring_DuckTyping/)

### Duck Typing

[https://medium.com/spacewalk-blog/javascript-duck-typing-5dfbb7d26769](https://medium.com/spacewalk-blog/javascript-duck-typing-5dfbb7d26769)

[https://nesoy.github.io/articles/2018-02/Duck-Typing](https://nesoy.github.io/articles/2018-02/Duck-Typing)

[https://yujuwon.tistory.com/177](https://yujuwon.tistory.com/177)
