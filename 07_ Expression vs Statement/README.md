# 7. Expression vs Statement

- 식 vs 문

## 1. Expression, Statement

![https://shoark7.github.io/assets/img/knowledge/expression_statement.png](https://shoark7.github.io/assets/img/knowledge/expression_statement.png)

### 1-1. Expression

- result : value ( expression becomes(produces) values )
    - 어떠한 값이 나오는 것이면 expression
    - ex
        
        ```jsx
        10 
        10; // expression statement : expression을 statement로 만든 것
        
        4 + square(5) + square(square(5)) // subexpression의 결합
        
        const x = 5; //5가 expression
        ```
        
        - `const x = 5;`
            - expression : `5` , `x=5`
            - statement : 이 문장 자체(선언문 & 할당문)
                - 선언문의 side effect : 값을 할당
- 모든 expression은 statement이다.
    - ex
        
        ```jsx
        const y = getAnswer(); // getAnswer()는 expression statement
        ```
        
        - `const y = getAnswer();`
            - expression : getAnswer()
            - statement : 이 문장 자체(할당문), getAnswer()
                - side effect : 함수 호출해서 어떠한 행동 수행, 값 할당
            - getAnswer()는 expression이자 statement

### 1-2. Statement

- action ( statement produces behavior )
    - ex
        
        ```jsx
        if(num > 0) {
          return num;
        }
        
        while(counter <= n) {
          result = result * result;
        }
        
        for(let counter = 1; counter <= n; counter++){
          result *= counter;
        }
        ```
        
    - 어떠한 것을하고 side effect 를 가짐
        - side effect (부수 효과) ?
            - `x = 5` 할 때, 값을 할당하는 것이 side effect
            - `setTimeout()` 을 하면, 브라우저에서 타이머를 시작하는 것이 side effect
            - 밑에서 `foo()` 하면, a를 변경시킨 것은 side effect
                
                ```jsx
                let a = 1;
                
                function foo() {
                   a += 1;
                }
                
                foo(); // 결괏값: 'undefined', side effect: 'a'가 변경됨.
                ```
                
- statement 의 구분 : `;`
- statement를 expression으로 바꾸고 싶다면(값을 산출하도록 하고 싶으면?)
    - IIFE 사용
        
        ![https://github.com/douzone-javascript-33-study/javascript-33-concepts/blob/main/images/07_ifee.PNG?raw=true](https://github.com/douzone-javascript-33-study/javascript-33-concepts/blob/main/images/07_ifee.PNG?raw=true)
        

## 2. 왜 statement 와 expression을 구분해야 하는지?

### 2-1. expression이 예상되는 곳에 statement를 넣지 말기

- 어떠한 것이 expression될 수 있는지, 어떠한 것이 statement만 될 수 있는지 구분하기
    - 예시
        - `return`문 : statement
        - 함수 호출 대부분 : expression
        - 선언문 : statement (`const x`)
        - 할당문 : expression (`x=5`)
            - 보통 연산자의 결과물은 expression
    - 보통 browser 개발자 도구에서 console로 찍어서 값이 나오면 expression
- 기본적으로 어떠한 함수 호출시 parameter에는 statement가 아닌 expression이 예상됨
    - `if()` 에서 괄호 안에는 expression이 예상됨
        - error : `if(return 200)`
    - `console.log()` 에서 괄호 안에는 expression이 예상됨
        - error : `console.log(const x); //error`
    - 연산자 : 피연산자는 항상 expression
        - `=` 할당 연산자의 오른쪽은 expression이 예상됨
            - error: `let b = if(x>10) {return 100;}; //error`
        - `&&` 연산자
            - error : `x == y && return 30` , return문은 statement
            - `=` 와 함께 쓰는 경우 괄호와 함께 써야함(우선순위 관련)
                - `(x=5) && (y=30)`
- React 에서 사용하는 JSX에서 `{}` 내에는 expression만 가능
    - 즉, if문등을 사용할 수 없음
        - if 대신 `&&` 연산자나 `?`등을 활용해야 함
            
            ```jsx
            class Layout extends Component {
                render() {
                    return (
                        <div className={'contacts'}>
                            {
                                addButton ? 
                                    <Contacts /> : 
                                    <Enrollment />
                            }
                        </div>
                    );
                }
            }
            ```
            
        - if를 사용하고 싶으면 함수로 감싸야 함(IIFE사용)
            
            ```jsx
            class Layout extends Component {
                render() {
                    return (
                        <div className={'contacts'}>
                            {
                                (() => {
            	                    if(addButton){ 
            	                        return <Contacts />
            	                    } else {
            	                        return <Enrollment />
            	                    }
            										})()
                            }
                        </div>
                    );
                }
            }
            ```
            

### 2-2. expression을 활용하여 코드 길이 줄이기

- statement에서 어떠한 side effect를 가지는 지, 다른 statement와 어떠한 관련이 있는 지 알면 두 개 이상의 statement를 하나의 statement로 합칠 수 있다.
    - side effect에서 하는 일이 expression이면 하나로 합치기
        - 수정 전 : 두 개의 if 문
            
            ```jsx
            function vowels(str) {
               let matches;
            
               if (str) {
                  // 첫 if : 할당 side effect만 가짐
                  // 다른 부수 효과는 없으며, 할당은 그 자체로 expression
                  matches = str.match(/[aeiou]/g);
            
                  if (matches) {
                     // 두 번째 if : 할당된 것을 반환
                     return matches;
                  }
               }
            }
            ```
            
        - 수정 후  : 하나의 if문
            
            ```jsx
            function vowels(str) {
               let matches;
               
               // 할당문은 그 자체로 expression이 됨
               if (str && (matches = str.match(/[aeiou]/g))) {
                  return matches;
               }
            }
            ```
            

### 2-3. Function expression VS Function Declaration(statement)

- Function expression (함수 표현식)
    
    ```jsx
    funcExpression(); // error : 정의되기 전에 사용 불가
    var funcExpression = function(){
    	return 'a function expression';
    }
    
    funcExpression(); // 정상 작동
    ```
    
- Function declaration (함수 선언문)
    
    ```jsx
    funcDecelaration(); // 정상 작동 : 정의되기 전에 사용 가능
    function funcDeclaration() {
        return 'A function declaration';
    }
    ```
    
- 두 개 차이점?
    - hoisting 관련
        - 선언문(declaration;statement)은 메모리상에 올려질 때 코드 상 가장 위에 위치한 것처럼 행동
        - 할당문(expression)은 본래 코드가 위치한 위치에서 할당 이루어짐
    - function expression (위의 코드가 hoisting 되는 것을 표현)
        
        ```jsx
        var funcExpression = undefined; // hoisting
        
        funcExpression(); // error : 할당되기 전에 사용됨
        funcExpression = function(){
        	return 'a function expression';
        }
        
        funcExpression(); // 정상 작동
        ```
        
    - function declaration (위의 코드가 hoisting 되는 것을 표현)
        
        ```jsx
        // hoisting
        function funcDeclaration() {
            return 'A function declaration';
        }
        
        funcDecelaration(); // 정상 작동
        ```
        
- 문제
    - 문제 1
        
        ```jsx
        function foo(){
            function bar() {
                return 3;
            }
            return bar();
            function bar() {
                return 8;
            }
        }
        alert(foo());
        ```
        
    - 문제 2
        
        ```jsx
        function foo(){
            var bar = function() {
                return 3;
            };
            return bar();
            var bar = function() {
                return 8;
            };
        }
        alert(foo());
        ```
        
    - 문제 3
        
        ```jsx
        alert(foo());
        function foo(){
            var bar = function() {
                return 3;
            };
            return bar();
            var bar = function() {
                return 8;
            };
        }
        ```
        
    - 문제 4
        
        ```jsx
        function foo(){
            return bar();
            var bar = function() {
                return 3;
            };
            var bar = function() {
                return 8;
            };
        }
        alert(foo());
        ```
        
- 답
    - 문제 1 : 8
        
        ```jsx
        function foo(){
            function bar() {
                return 3;
            }
            function bar() {
                return 8;
            } // 재정의
            return bar(); // 8
        }
        alert(foo());
        ```
        
    - 문제 2:  3
        
        ```jsx
        function foo(){
            var bar = undefined;
            bar = function() {
                return 3;
            };
            return bar(); // 3
            bar = function() {
                return 8;
            };
        }
        alert(foo());
        ```
        
    - 문제 3 : 3
        
        ```jsx
        // hoisted
        function foo(){
            var bar = undefined;
            bar = function() {
                return 3;
            };
            return bar(); // 3
            bar = function() {
                return 8;
            };
        }
        alert(foo());
        ```
        
    - 문제 4 : [Type Error: bar is not a function]
        
        ```jsx
        function foo(){
            var bar = undefined;
            return bar(); // undefined
            bar = function() {
                return 3;
            };
            bar = function() {
                return 8;
            };
        }
        alert(foo());
        ```
        

## 참고

- statement의 side effect
    - [https://velog.io/@_uchanlee/문Statement과-표현식Expression](https://velog.io/@_uchanlee/%EB%AC%B8Statement%EA%B3%BC-%ED%91%9C%ED%98%84%EC%8B%9DExpression)
- function expression, declaration 문제, 답
    - [https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
