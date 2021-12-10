- javascript engine
    - heap + single call stack(단일 스레드)
        
        <img src="https://joshua1988.github.io/images/posts/web/translation/how-js-works/js-engine-structure.png" width="500px" />
        
        - run time :  WEB API, Callback Queue, Event Loop, JS Engine
            
            <img src="https://miro.medium.com/max/875/1*4lHHyfEhVB0LnQ3HlhSs8g.png" width="500px" />
            

- call stack
    - 개념
        - 여러 함수를 호출하는 script에서 해당 함수들의 위치를 추적하는 인터프리터에 대한 메커니즘
        - 함수 호출 스택 방식으로 기록하는 데이터 구조
        - 단일로 존재 : 위에서 아래로 수행 - 동기식 수행
    - 무엇이 쌓이는가?
        - execution context
            - javascript 코드가 실행되는 환경
            - call stack에 쌓이는 것
            - 종류
                - global execution context
                - function execution context
    - stack overflow ?
        - 스택 공간보다 많은 함수가 쌓일 경우 발생
        - 대개는 종료점이 없는 재귀함수 호출시 발생
    - 실행
        - 프로그램 실행시 global execution context 생성
        - 함수가 실행될 떄 call stack에 순차적으로 push
        - call stack에 있는 함수를 순차적으로 실행하고 pop
        
        ```jsx
        let a = 'Hello World!';
        function first() {
          console.log('Inside first function');
          second();
          console.log('Again inside first function');
        }
        function second() {
          console.log('Inside second function');
        }
        first();
        console.log('Inside Global Execution Context');
        ```
        
        ![https://miro.medium.com/max/2000/1*ACtBy8CIepVTOSYcVwZ34Q.png](https://miro.medium.com/max/2000/1*ACtBy8CIepVTOSYcVwZ34Q.png)
        
        ![https://miro.medium.com/max/875/1*ctt_X7TP0GyR4W9XKuwQWQ.png](https://miro.medium.com/max/875/1*ctt_X7TP0GyR4W9XKuwQWQ.png)
        
- heap
    - 객체, 변수 메모리 할당
- callback queue
    - 메세지 대기열 : 처리할 메시지 목록 + 콜백함수
    - task(처리할 작업) 임시 저장소(대기 장소)
    - call stack이 빈 상태인 경우, 먼저 대기열에 들어온 순서대로 수행
    
    ![https://miro.medium.com/max/875/1*-MMBHKy_ZxCrouecRqvsBg.png](https://miro.medium.com/max/875/1*-MMBHKy_ZxCrouecRqvsBg.png)
    
- event loop
    - single thread
    - [What is the JS Event Loop and Call Stack? (github.com)](https://gist.github.com/jesstelford/9a35d20a2aa044df8bf241e00d7bc2d0)
    
- 코딩시 주의
    - 호출 스택 관련 에러 : **Maximum call stack size exceeded**
    - 비동기 코드의 이점
        - 동기 코드 : callback queue에 쌓이는거가 아니라 call stack 자리를 차지하며 코드 실행함. 함수를 중첩으로 사용하는 경우, 동기로만 짜게 되면 스택 최대치를 초과하여 에러를 발생시킴. 이러한 경우 비동기로 만들면 어느정도 해결이 되긴 한다.그러면 최소한 호출 스택이 터지지는 않기 때문이다.
            - 비동기로 만드는 법 : setTimeout하고 0ms으로 주기
        - 비동기 코드 : callback stack에 자리를 차지하며 그 코드만 실행하는 것이 아니라 callback queue에 담아두고 다른 함수들도 실행하며 비동기 코드도 실행됨
        - 예시 코드
            
            ```jsx
            //동기
            [1,2,3,4].forEach(function(i) {
            	console.log('processing sync')
            	delay();
            });
            
            //비동기
            function asyncForEach(array, cb){
            	array.forEach(function() {
            		setTimeout(cb,0);
                });
            }
            
            asyncForEach([1,2,3,4], function(i) {
            	console.log('processing async',i)
            	delay();
            });
            ```
            
- 참고 사이트
    - 코드 실제로 실행시키며 call stack, callback queue, web api 보기
        - [http://latentflip.com/loupe](http://latentflip.com/loupe)
        - sample code
            
            ```jsx
            $.on('button', 'click', function onClick() {
                setTimeout(function timer() {
                    console.log('You clicked the button!');    
                }, 2000);
            });
            
            console.log("Hi!");
            
            setTimeout(function timeout() {
                console.log("Click the button!");
            }, 5000);
            
            console.log("Welcome to loupe.");
            ```
            
    
    ## Question
    
    1. 비동기코드를 사용하는 것이 좋은것인지?
