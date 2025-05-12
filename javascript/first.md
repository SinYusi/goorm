## 변수란?

- 변수 = 데이터 저장할 때 쓰이는 “이름이 붙은 저장소”
- 변수 만드는 법
    - let: 변할 수 있는 변수를 선언할 때 사용
        
        ```jsx
        let message; // message 라는 이름의 변수(저장소)를 생성
        
        message = "Hello"; // message 라는 변수에 문자열 저장
        ```
        
        - let으로 선언한 변수에 저장한 값은 다른 값으로 얼마든지 변경 가능
            
            ```jsx
            let message = 'Hello'; // 변수 생성과 동시에 문자열 저장
            
            message = 'World'; // 값을 변경
            ```
            
        - 변수의 데이터는 다른 변수에 복사 가능
            
            ```jsx
            let message = 'Hello';
            
            let another;
            
            another = message; // 'Hello'를 another에 복사
            ```
            
        - 같은 이름의 변수 중복 선언 불가
            
            ```jsx
            let message = "Hello";
            
            // 'let'을 반복하면 에러가 발생합니다.
            let message = "World"; // SyntaxError: 'message' has already been declared
            ```
            
    
    <aside>
    👉
    
    `var` 라는 명령어도 `let` 과 거의 동일하게 동작하지만, 오래된 방식이기에 사용하는걸 권장하지 않음
    
    </aside>
    
    - `const` : 변화하지 않는 변수를 선언할 때 사용(상수)
        
        ```jsx
        const hellowWorld = 'Hello World!';
        ```
        
        - const로 선언된 변수에 새로운 값을 할당하려고 하면 에러
            
            ```jsx
            const helloWorld = 'HelloWorld!';
            
            helloWorld = 'new world!'; // error: 재할당 불가능
            ```
            
        - 대문자 상수: 상수는 대문자와 밑줄(_)로 구성된 이름으로 변수명을 명명
            
            ```jsx
            // 예를 들어, 다양한 색상 코드를 반복적으로 사용한다고 했을 때 색상 코드 다 외울 순 없음.
            // 그런 기억하기 힘든 값을 대문자 상수로 만들어주는 것.
            const COLOR_RED = "#F00";
            const COLOR_GREEN = "#0F0";
            const COLOR_BLUE = "#00F";
            const COLOR_ORANGE = "#FF7F00";
            
            // 색상을 고르고 싶을 때 별칭을 사용할 수 있게 되었습니다.
            let color = COLOR_ORANGE;
            alert(color); // #FF7F00
            ```
            
        
        <aside>
        ❓
        
        일반 상수 vs 대문자 상수
        
        - 일반 상수: 코드가 실행된 이후 계산되어 할당되는 변하지 않는 상수
        - 대문자 상수: 코드가 실행되기 전에도 이미 그 값을 알고 있는 (하드코딩해주는) 상수
        </aside>
        

## 변수명에 대한 중요한 사실 1가지

→ 변수명은 간결하고, 명확해야 함

- 변수 명명 규칙(개발자들끼리의 약속)
    
    ```jsx
    // ✅ 올바른 변수명
    let $personal;
    let _personal;
    let personalData;
    let personal123;
    
    // ❌ 잘못된 변수명
    let 1A; // 숫자로 시작하면 안됨
    let my-name; // 하이픈은 변수명으로는 사용 안됨
    ```
    
    1. 변수명에는 문자, 숫자, 기호 중에서 `$`, `_` 만 들어갈 수 있음
    2. 첫 글자는 숫자 x
    3. 변수명 만들 때에는 [카멜케이스](https://en.wikipedia.org/wiki/Camel_case) 사용
    4. 대소문자 구별
    5. [예약어 목록](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#reserved_words)에 있는 단어는 변수명 사용 금지
- 바람직한 변수명을 위해 참고하면 좋은 규칙
    1. `userName` `userInfoData` 처럼 사람이 읽을 수 있는 이름 + 직관적인 이름 사용
    2. 줄임말 혹은 단순한 알파벳 회피
    3. `let data` x → `let userName` o : 간결하게 작성하지만 그 안에서도 최대한 구체적으로 명명
    4. 팀의 규칙을 따로 세우기

## 자료형

- JavaScript는 동적 타입 언어(Dynamically Typed)
    - 동적 타입 언어: 변수에 저장되는 값의 타입을 언제든지 바꿀 수 있는 언어
- Number Type
    - 일반 숫자값: 1, 2, 3, …
    - 특수 숫자값: Infinity(무한대), -Infinity, NaN(계산 중 에러가 발생했다는 것을 나타내는 값)
- String Type
    
    ```jsx
    let str = "Hello"; // 큰 따옴표 사용
    let str2 = 'Single quotes are ok too'; // 작은 다옴표 사용
    let phrase = `can embed another ${str}`; // 백틱 사용(${}로 변수 사용 가능)
    ```
    
    ```jsx
    let name = "Lisa";
    
    // 변수를 문자열 중간에 삽입할 수 있음
    alert( `Hello, ${name}!` ); // Hello, Lisa!
    ```
    
- Boolean Type
    - true(긍정)
    - false(부정)
- `null` 값
    - 오로지 null값만 포함하는 별도의 자료형
- `undefined` 값
    
    ```jsx
    let name;
    
    console.log(name); // undefined 출력됨
    ```
    
    - 변수를 선언하고 값 할당하지 않았을 때 undefined로 할당
- 객체(object) & 심볼(symbol)
    - 데이터 컬렉션이나 복잡한 개체를 표현할 수 있음
- `typeof` 연산자
    - 어떤 자료형인지 확인할 수 있는 연산자
        
        ```jsx
        let numberValue = 3; console.log(typeof numberValue)
        ```
        

<aside>
❗

`null` vs `undefined`

- js에서는 null과 undefined는 성격이 다름
- js에서 `null` = 존재하지 않는 값 / 비어 있는 값 / 알 수 없는 값
    - 개발자가 직접 `null`값을 넣음
- js에서 `undefined` = 값이 할당되지 않은 상태
    - 개발자가 직접 할당할 수는 있지만, null과 구분 짓기 위해 할당하지 않음
    - 할당되지 않은 변수 초기값을 위한 예약어
</aside>

## 유저와 상호작용할 수 있는 함수

- `alert`
    - 사용자가 확인 버튼을 누를 때까지 메시지를 보여주는 창이 뜸
    - `alert` 로 생성된 모달창을 확인 버튼으로 끄지 않으면 모달 창 이외의 영역은 건드릴 수 없음
- `prompt`
    - 텍스트 메시지와 입력 필드, 확인 및 취소 버튼이 있는 모달창이 뜸
    - 개발자 도구 콘솔창에 `prompt('Write your name')` 을 치고 실행해보자.
        - 확인 클릭 시 입력한 값 반환
        - 취소 클릭 시 `null` 반환
    - prompt로 입력받은 값을 변수로 담기
        
        ```jsx
        const name = prompt('Write your name')
        console.log(name)
        ```
        
- `confirm`
    - 매개변수로 받은 질문과 확인 및 취소 버튼이 있는 모달창이 뜸
    - 개발자 도구 콘솔창에 다음 코드를 실행해보자
        
        ```jsx
        let isBoss = confirm('당신이 주인인가요?');
        
        console.log(isBoss);
        ```
        

## 형변환

- 문자형으로 변환하는 방법
    
    ```jsx
    let value = true;
    console.log(typeof value); // boolean
    
    value = String(value); // 변수 value 에는 'true' 라는 문자열이 담길 거에요.
    console.log(typeof value); // string
    ```
    
- 숫자형으로 변환하는 방법
    - 수학 관련된 함수나 표현식에서 자동으로 변환됨(다음 코드를 한 번 실행해보자)
        
        ```jsx
        console.log( "6" / "2" );
        ```
        
    - 숫자 이외의 글자가 들어간 문자열은 `NaN`이 반환
        
        ```jsx
        let age = Number('hi');
        
        console.log(age); // NaN
        ```
        
    - 숫자형으로 변환될 때 적용되는 규칙
        - `Number(undefined)` → `NaN`
        - `Number(null)` → `0`
        - `Number(true)` → `1`
        - `Number(false`) → `0`
        - `Number(”123”)` → `123`
        - `Number(”    123    “)` → `123`
        - `Number(”123A”)` → `NaN`
- 불린형으로 변환하는 방법
    
    ```jsx
    console.log(Boolean(1)); // true
    console.log(Boolean(0)); //false
    
    console.log(Boolean("hello")); // true
    console.log(Boolean("")); // false
    ```
    
    - 불린형으로 변환할 때 적용되는 규칙
        - `숫자 0, 빈 문자열, null, undefined, NaN` → `false`
        - 그 외의 값 → `true`

## 기본 연산자

- 자바스크립트 수학 연산자 종류
    - 덧셈 연산자 +
    - 뺄셈 연산자 -
    - 곱셈 연산자 *
    - 나눗셈 연산자 /
    - 나머지 연산자 %
    - 거듭제곱 연산자 **
- `+`는 문자열 연결에도 사용
    
    ```jsx
    let s = "hello" + "world";
    console.log(s); // helloworld
    
    // 더하기 연산하는 피연산자 중 하나가 문자열이면 다른 하나도 문자열로 반환되어 계산됨
    console.log('1' + 2); // "12"
    
    // 만약 앞에 숫자 2개가 나오고 전부 덧셈이라면 숫자는 더해지고, 그 뒤에 문자열 붙고 문자열로 변환됨
    console.log(2 + 2 + '1') // 41
    console.log(typeof (2 + 2 + '1')) // string
    
    // 하지만 - , / 는 다름
    console.log(6 - '2') // 4 -> '2'를 숫자로 바꾼 후 연산하기 때문
    console.log('6' / '2') // 3 -> 두 문자열 모두 숫자로 변환 후 연산하기 때문
    ```
    

## 증감 연산자

- 증가 연산자: `++`
    - 변수를 1 증가시키는 연산자
        
        ```jsx
        let counter = 2;
        counter++; // counter = counter + 1과 동일하게 동작
        console.log( counter ); // 3
        ```
        
    - `++` 연산자가 변수 앞에 붙는지 뒤에 붙는지에 따라 반환값이 다름
        
        ```jsx
        // 뒤에 붙을 경우
        let counter = 2
        let a = counter++ // 뒤에 붙으면 값을 증가시키기는 하지만, 반환값은 기존 값
        console.log(a) // 2
        let b = a++ 
        console.log(b) // 2
        console.log(counter) // 3 -> counter는 증가된 상태니까 다시 확인해보면 증가해있음.
        
        // 앞에 붙을 경우
        let counter = 2
        let a = ++counter // 앞에 붙으면 값을 증가시키고, 반환값도 증가 시킨 값
        console.log(a) // 3
        let b = ++a
        console.log(b) // 4
        console.log(counter) // 3
        ```
        
- 감소 연산자: `--`
    - 변수를 1 감소시키는 연산자
        
        ```jsx
        let counter = 2;
        counter--; // counter = counter - 1과 동일하게 동작합
        console.log( counter ); // 1
        ```
        

## 비교 연산자

```jsx
console.log(2 > 1); // true
console.log(2 == 1); // false

console.log(2 == '2'); // true
console.log(2 == 2); // true

console.log(2 === '2'); // false
console.log(2 === 2); // true

console.log(2 != '2'); // false
console.log(2 !== '2'); // true

console.log(true == 1); // true
console.log(true === 1); // false

console.log(null == undefined); // true
console.log(null === undefined); // false

// == : 동등 연산자
// === : 일치 연산자(엄격한 동등 연산자, 자료형의 동등 여부까지 검사함)
```

> 웬만하면 연산자는 `===, !==` 를 사용하여 엄격하게 연산해주자. 에러 발생할 확률을 줄여줌
> 

## 논리 연산자

- `||` (OR)
    
    ```jsx
    // 둘 중 하나라도 true면 true, 그렇지 않으면 false
    console.log(true || true); // true
    console.log(true || false); // true
    console.log(false || true); // true
    console.log(false || false); // false
    ```
    
- 자바스크립트가 제공하는 OR의 추가 기능 → `단락 평가`
    - OR 연산자와 여러 개의 피연산자가 있을 때 왼쪽부터 true인지 판별
    → 만약 true라면 해당 피연산자의 불린형으로 변환하기 전 원래 값을 반환
        
        ```jsx
        console.log(1 || 0); // 1
        
        let nameA = ''
        let nameB = ''
        let nameC = 'C'
        console.log(nameA || nameB || nameC) // C
        
        let nameA = ''
        let nameB = ''
        let nameC = ''
        console.log(nameA || nameB || nameC || '셋다 이름 빈 문자열임') // 셋다 이름 빈 문자열임
        
        let nameA = undefined
        let nameB = 'BBB'
        let nameC = 'CCC'
        console.log(nameA || nameB || nameC) // BBB -> truthy한 값을 만나면 나머지는 평가하지 않은채 멈춤
        
        let nameA = null
        let nameB = 'BBB'
        console.log(nameA || nameB) // BBB
        
        let nameA = undefined
        let nameB = null
        console.log(nameA || nameB || 0) // 0 -> 셋다 falsy하기 때문에 그럴 땐 마지막 값 반환
        ```
        
    - 단락 평가는 언제 사용?
        - 연산자 왼쪽 값이 false인지 확인하고자 할 때 사용
            
            ```jsx
            true || alert("not printed"); // 왼쪽이 truthy하니까 거기서 평가 멈추기 때문에 alert 실행안됨
            false || alert("printed"); // 왼쪽이 falsy하니까 다음 피연산자를 평가하는데 명령어기 때문에 그대로 값 반환하며 alert() 실행됨
            ```
            
- `&&` (AND)
    
    ```jsx
    // 둘 중 하나라도 false 면 무조건 false 반환
    console.log(true && true); // true
    console.log(true && false); // false
    console.log(false && true); // false
    console.log(false && false); // false
    ```
    
- `!` (NOT)
    
    ```jsx
    // 피연산자를 불린형으로 변환하고, 해당 불린형의 역을 반환합니다.
    console.log(!true); // false
    console.log(!0); // true
    ```
    
    - `!!` : NOT을 2개 연달아 사용 시 값의 `불린형으로 변환`
        
        ```jsx
        console.log(!!null); // false
        console.log(!!"HELLO"); // true
        ```
        

## `??` nullish 병합 연산자

- `a ?? b` : a가 `null` 도 아니고 `undefined` 도 아니면 a값 반환 / 그외의 경우 b 반환
- `||` 와 차이점
    - `||` 연산자는 첫 번째 true값을 반환
    - `??` 연산자는 첫 번째 정의된(즉, null이나 undefined가 아닌) 값을 반환
    
    ```jsx
    // 예시
    let height = 0
    
    // 0은 fasly하므로 해당 콘솔은 100을 반환합니다.
    console.log(height || 100) 
    
    // height가 null,undefined가 아닌 0이라는 값이 할당되었기 때문에 0이 출력됩니다.
    console.log(height ?? 100) 
    
    ---
    
    // 만약, height 값이 undefined 라면?
    let height; // 아무 값도 할당하지 않았으므로 undefined
    
    // height가 undefined 이므로 100 출력됨
    console.log(height ?? 100) 
    ```
    

## 조건 처리하는 조건문 사용법

- `if문`
    
    ```jsx
    if(조건문) {
    	// 조건문이 true라면 해당 코드 블럭 실행됨
    }
    ```
    
    - 조건문에 뭐가 들어가든 불린값으로 변환됨
- `if else문`
    
    ```jsx
    if (1 === 1) {
    	// 조건문이 true이면 해당 코드 블럭이 실행됨
    } else {
    	// 조건문이 false이면 해당 코드 블럭이 실행됨
    }
    
    // 만약, 처리해야 할 조건문이 여러개라면?
    if (조건문1) {
    	// 조건문1 이 true이면 해당 코드 블럭이 실행됨
    } else if (조건문2) {
    	// 조건문2 가 true이면 해당 코드 블럭이 실행됨
    } else if (조건문3) {
    	// 조건문3 이 true이면 해당 코드 블럭이 실행됨
    } else {
    	// 조건문1,2,3이 전부 false이면 해당 코드 블럭이 실행됨
    }
    ```
    
- 조건부 연산자 `?` = 삼항 연산자
    - 단순한 조건에 따라 변수에 값을 달리 할당하고 싶을 때 유용
        
        ```jsx
        // if문을 활용한 버전
        let accessAllowed;
        let age = prompt('나이를 입력해 주세요');
        
        if (age > 18) {
        	accessAllowed = true;
        } else {
        	accessAllowed = false;
        }
        
        console.log(accessAllowed);
        
        // 삼항 연산자
        let accessAllowed;
        let age = prompt('나이를 입력해 주세요');
        
        accessAllowed = age > 18 ? true : false; // 비교 연산자 자체가 true,false를 반환하기 때문에 accessAllowed = age > 18; 만 적어도 정상동작함
        
        console.log(accessAllowed);
        ```
        
    - 다중 삼항 연산자 가능(가독성이 떨어짐)
        
        ```jsx
        age > 18 ? (age <= 20 ? 'hi' : 'ho') : 'he'
        ```
        

## 반복문의 종류

- `while문`
    
    ```jsx
    while (condition) {
    	// condition(조건)이 truthy이면 반복문 본문 코드 실행
    }
    
    // 예시
    let i = 0
    while (i < 3) {
    	console.log(i) // 0, 1, 2 가 순서대로 출력됨
    	i++
    }
    ```
    
- 조건문을 활용하지 않고 반복문을 탈출하는 법: `break`
    
    ```jsx
    while (true) {
    	if(condition) break;
    	// condition에 true가 아니라면 반복문 실행
    }
    ```
    
- `do…while` 문
    
    ```jsx
    // 조건문을 아래로 옮기는 방법
    // 단, 얘는 분문 코드를 최소 1번이라도 실행하고 싶을 때만 사용
    // 웬만하면 일반 while 문이 적합
    let i = 0
    do {
    	console.log(i) // 0, 1, 2 가 순서대로 출력됨
    	i++
    } while (i < 3)
    ```
    
- `for`문
    
    ```jsx
    for(begin; condition; step) {
    	// condition truthy 하다면 반복문 실행
    }
    
    // 예시
    // 1. i라는 변수가 0으로 할당되며 실행된다.
    // 2. i 가 3 보다 작은지 조건문이 확인된다.
    // 3. truthy하다면 반복문 본문 코드가 실행, 아니라면 반복문 멈춤
    // 4. 반복문 본문 실행됬다면 step을 실행하여 i++ 로 1 증가 시켜줌.
    // 5. 다시 조건문으로 돌아와서 1 증가된 i 가 3 보다 작은지 확인한다.
    // 6. truthy하다면 반복문 본문 코드가 실행, 아니라면 반복문 멈춤
    // 7. falsy하여 반복문 멈출 때까지 반복...
    for (let i = 0; i < 3; i++) { 
      console.log(i); // 0, 1, 2가 출력됩니다.
    }
    ```
    
    - `begin`: 반복문 진입 시 단 한 번 실행
    - `condition` : 반복마다 해당 조건이 확인되며, false면 반복문 멈춤
    - `step` : 각 반복의 body가 실행된 이후에 실행
    - `반복문 반복 코드` : 조건문이 truthy일 동안 계속해서 실행
- 반복문 중간에 스킵하는 법: `continue`
    
    ```jsx
    for (let i = 0; i < 10; i++) {
    
      // 조건이 참이라면 남아있는 본문은 실행되지 않습니다.
      if (i % 2 == 0) continue;
    
      console.log(i); // 1, 3, 5, 7, 9가 차례대로 출력됨
    }
    ```
    

## 가끔 쓰이는 `switch`문

- 복수의 `if` 조건문을 `switch`문으로 바꿀 수 있음
    
    ```jsx
    // x 에는 변수 가 들어갑니다
    switch(x) { 
      case 'value1':  // if (x === 'value1')
        ...
        break;
    
      case 'value2':  // if (x === 'value2')
        ...
        break;
    
      default:
        ...
        break;
    }
    
    // 예시
    let a = 2 + 2;
    
    switch (a) {
      case 3:
        console.log( '비교하려는 값보다 작습니다.' );
        break;
      case 4:
        console.log( '비교하려는 값과 일치합니다.' );
        break;
      case 5:
        console.log( '비교하려는 값보다 큽니다.' );
        break;
      default:
        console.log( "어떤 값인지 파악이 되지 않습니다." );
    }
    
    // 만약 break 를 적지 않는다면 조건에 해당하는 모든 케이스가 전부 실행되겠죠?
    ```
    

## 함수란?

- 함수는 일정 코드 블록을 만들고, 그 블록을 필요할 때 불러 쓸 수 있는 것
- 함수를 사용하면 가독성이 좋아지고 코드량이 짧아짐
- 함수 선언
    
    ```jsx
    function showMessage() {
    	console.log('show message')
    }
    
    // 함수 사용할 때
    showMessage() // show message
    showMessage() // show message
    ```
    
- 지역 변수 vs 외부 변수
    - 지역 변수: 함수 내에서 선언한 변수, 해당 함수 내에서만 접근이 가능
        
        ```jsx
        function showMessage() {
        	let msg = 'show message' // msg는 지역변수
        	console.log(msg)
        }
        showMessage() // show message
        console.log(msg) // ReferenceError: msg is not defined
        ```
        
    - 외부 변수: 함수 외부에서 선언한 변수, 함수 내에서도 접근 및 수정이 가능
        
        ```jsx
        // 외부 변수 접근하기
        let userName = 'Lisa';
        
        function showMessage() {
          let msg = 'Hello, ' + userName; // userName은 외부 변수니까 여기서도 접근 가능
          console.log(msg);
        }
        
        showMessage(); // Hello, Lisa
        console.log(userName); // Lisa
        
        // 외부 변수 수정하기
        let userName = 'Lisa';
        
        function showMessage() {
          userName = "Bob"; // (1) 외부 변수를 수정함
        
          let msg = 'Hello, ' + userName;
          console.log(msg); 
        }
        
        console.log( userName ); // 함수 호출 전이므로 John 이 출력됨
        
        showMessage(); // Hello, Bob
        
        console.log( userName ); // 함수에 의해 Bob 으로 값이 바뀜
        ```
        
- 매개변수(인자)
    - 함수에 필요한 데이터를 호출할 때 전달할 수 있는 매개체
        
        ```jsx
        function showMessage(text, writer) {
        	console.log(`${writer} : ${text}`)
        }
        
        showMessage('Hello', 'Lisa') // Lisa : Hello
        showMessage('Bye', 'Mandoo') // Mandoo : Bye
        showMessage('what') // undefined : what
        ```
        
    - 함수를 호출할 때 매개변수를 넘겨주지 않으면 undefined가 할당됨
    - 이를 방지하려면 기본값을 설정
        
        ```jsx
        function showMessage(text, writer = 'Lisa') {
        	console.log(`${writer} : ${text}`)
        }
        
        showMessage('Hello') // Lisa : Hello
        showMessage('Bye', 'Mandoo') // Mandoo : Bye
        ```
        
- 반환값
    - 특정 값을 반환하게 할 수 있음
        
        ```jsx
        function sum(a, b) {
          return a + b;
        }
        
        let result = sum(1, 2);
        console.log( result ); // 3
        
        // 만약 return문 없거나, return 지시자만 있는 경우는 undefined 반환함.
        ```
        
- 개발자들끼리의 함수 이름 짓는 방법
    - 함수명은 어떤 동작을 하는 함수인지 간결하고 명확하게 지어야 함
    - 동사를 접두어로 붙여 함수 이름을 만드는 것이 관습(규칙으로 설정도 함)
    - 예를 들어
        - `show…` 로 시작하는 함수 : 무언가를 보여주는 함수
        - `get…` 로 시작하는 함수 : 값을 반환함
        - `calc…` 로 시작하는 함수 : 무언가를 계산함
        - `create…` 로 시작하는 함수 : 무언가를 생성함
        - `check…` 로 시작하는 함수 : 무언가를 확인하고 불린값을 반환함
- 함수는 하나의 동작만 담당해야함

## 함수 표현식 vs 함수 선언식 vs 화살표 함수

- 함수 선언문
    
    ```jsx
    // 함수 선언문
    function 함수명() {
      // 함수 로직
    }
    
    function sum(a, b) {
      return a + b;
    }
    ```
    
- 함수 표현식(함수를 생성하고 변수에 값을 할당하듯 함수가 할당됨)
    
    ```jsx
    let sayHi = function() {
    	console.log('hi')
    }
    console.log(sayHi) //ƒ () {console.log('hi')} -> 함수 자체가 보임
    sayHi() // hi -> 함수가 실행됨(자바스크립트는 괄호가 있어야 함수가 실행됨)
    
    // 함수 복사도 가능
    function sayHi() {   // (1) 함수 생성
      console.log('hi')
    }
    
    let func = sayHi;    // (2) 함수 복사
    
    func(); // hi     // (3) 복사한 함수를 실행
    sayHi(); // hi    // (4) 본래 함수도 정상적으로 실행됩니다.
    
    // 함수 표현식 안에서도 종류가 있습니다.
    // 기명 함수 표현식 vs 익명 함수 표현식
    
    // 기명 함수 표현식(named function expression)
    var foo = function multiply(a, b) {
      return a * b;
    };
    
    // 익명 함수 표현식(anonymous function expression)
    var bar = function(a, b) {
      return a * b;
    };
    
    console.log(foo(10, 5)); // 50
    console.log(multiply(10, 5)); // Uncaught ReferenceError: multiply is not defined
    ```
    
- 콜백 함수
    - 콜백 함수란 함수를 값처럼 전달하는 것
    
    ```jsx
    // 콜백 함수를 위한 예시 함수
    // 함수에 질문을 하면, 사용자 답변에 따라 yes / no 를 출력하는 함수입니다.
    function ask(question, yes, no) {
      if (confirm(question)) yes()
      else no();
    }
    
    function showOk() {
      alert( "동의하셨습니다." );
    }
    
    function showCancel() {
      alert( "취소 버튼을 누르셨습니다." );
    }
    
    // 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
    // 즉, 여기서 showOk, showCancel 가 콜백 함수 라고 불리는 친구들
    ask("동의하십니까?", showOk, showCancel);
    ```
    
- 함수 표현식과 함수 선언식의 차이점
    - 함수 표현식: 실제 실행 흐름이 해당 함수에 도달했을 때 함수가 생성
    → 즉, 코드 실행 흐름이 함수에 도달했을 때부터 해당 함수를 사용할 수 있음
    - 함수 선언문: 함수 선언문이 정의되기 전에도 호출 가능
        
        ```jsx
        // 예시
        
        // 함수 선언문
        // 아래 코드 실행해보면 함수 정의한 것보다 함수 호출한 것이 위에 있어도 정상 동작됨
        sayHelloToName('lisa') // Hello, lisa
        
        function sayHelloToName(name) {
          console.log( `Hello, ${name}` );
        }
        
        // 함수 표현식
        // 반면, 아래 코드는 함수 정의하기 전에 함수를 호출했을 때 아직 정의되지 않았기 때문에 에러남
        sayHelloToName2('lisa') // ReferenceError: sayHelloToName2 is not defined
        
        let sayHelloToName2 = function (name) {
          console.log( `Hello, ${name}` );
        }
        ```
        
- 화살표 함수
    - 함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법
    
    ```jsx
    // 함수 선언식
    function sum(a, b) {
    	return a + b
    }
    
    // 화살표 함수 ex 1
    const sum = (a, b) => {
    	return a + b
    }
    
    // 만약 return 문 1줄만 필요할 경우 중괄호 생략 가능
    const sum = (a, b) => a + b
    
    // 화살표 함수 ex 2
    const printHello = () => console.log('hello')
    
    printHello() // hello
    ```
    

## 객체 기본 문법

- 자바스크립트의 객체는 `키(key) + 값(value)` 로 구성된 프로퍼티들의 집합
- 선언하기
    
    ```jsx
    // 빈 객체를 만드는 법
    let user = new Object() // 객체 생성자 문법
    let user = {} // 객체 리터럴 문법 (권장)
    ```
    
    - 중괄호 {…}를 이용해 겍체를 선언하는 것 = 객체 리터럴(권장)
    - new 키워드와 함께 객체를 생성하고 초기화하는 함수 = 객체 생성자
- 프로퍼티값 넣고 삭제해보기
    
    ```jsx
    const user = {     // 객체
      name: "John",  // 키: "name",  값: "John"
      age: 30        // 키: "age", 값: 30
    };
    
    console.log(user) // { name: 'John', age: 30}
    console.log(user.name) // John -> 객체 안에 있는 특정 키의 값을 꺼내고 싶을 때
    
    user.name = 'Lisa'
    
    console.log(user.name) // Lisa
    console.log(user['name']) // Lisa
    
    delete user.age // 객체의 프로퍼티 삭제하기
    
    console.log(user) // {name: 'Lisa'}
    ```
    
- 생성자 함수로 객체 사용해보기
    
    ```jsx
    // 생성자 함수는 객체를 생성하기 위한 탬플릿(클래스)처럼 사용할 수 있어요
    // 생성자 함수 Person -> 생성자 함수는 대문자로 시작함
    function Person(name, gender) {
      this.name = name;
      this.gender = gender;
      this.sayHello = function(){
        console.log('Hi! My name is ' + this.name);
      };
    }
    
    // 인스턴스의 생성 -> person1, person2 를 인스턴스라고 합니다.
    var person1 = new Person('Lee', 'male');
    var person2 = new Person('Kim', 'female');
    
    console.log('person1: ', typeof person1); // person1:  object
    console.log('person2: ', typeof person2); // person2:  object
    console.log('person1: ', person1); // person1:  Person {name: 'Lee', gender: 'male', sayHello: ƒ}
    console.log('person2: ', person2); // person2:  Person {name: 'Kim', gender: 'female', sayHello: ƒ}
    
    person1.sayHello(); // Hi! My name is Lee
    person2.sayHello(); // Hi! My name is Kim
    ```
    
- 객체를 만들 때 단축 프로퍼티로 줄여쓸 수 있음
    
    ```jsx
    function createUserInfo(name, age) {
    	return {
    		name: name, // 이렇게 키, 값 이름이 변수의 이름과 동일할 때 사용할 수 있는 단축 프로퍼티
    		age: age
    	}
    }
    
    const user = createUserInfo("Lisa", 30)
    console.log(user)
    
    // 단축 프로퍼티로 수정해보면
    function createUserInfo(name, age) {
    	return {
    		name, // name: name 과 같은 의미 입니다.
    		age
    	}
    }
    
    const user = createUserInfo("Lisa", 30)
    console.log(user)
    ```
    
- `in` 연산자로 객체 프로퍼티 존재 여부를 확인할 수 있음
    
    ```jsx
    "key" in object
    
    // example
    const user = {name: "Lisa", age: 30}
    console.log("age" in user) // true
    console.log("city" in user) // false
    ```
    
- `for…in` 반복문은 객체의 모든 키를 순회할 수 있음
    
    ```jsx
    for (key in object) {
      // 각 프로퍼티 키(key)를 이용하여 본문(body)을 실행합니다.
    }
    
    let user = {
      name: "John",
      age: 30,
      isAdmin: true
    };
    
    for (let key in user) {
      // 키
      console.log( key );  // name, age, isAdmin
      // 키에 해당하는 값
      console.log( user[key] ); // John, 30, true
    }
    ```
    
- 객체 정렬 방식
    - 객체 프로퍼티(key)가 정수 프로퍼티이면 자동으로 정렬되고, 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬
    
    ```jsx
    let codes = {
      "49": "독일",
      "41": "스위스",
      "44": "영국",
      "1": "미국"
    };
    
    for (let code in codes) {
      console.log(code); // 1, 41, 44, 49
    }
    
    let userInfos = {
      "lisa": "lisa",
      "john": "john",
      "bob": "bob",
      "mandoo": "mandoo"
    };
    
    for (let userInfo in userInfos) {
      console.log(userInfo); // lisa, john, bob, mandoo
    }
    
    // 만약, 숫자를 쓰고 싶은데 자동 정렬을 막고 싶다면 + 를 붙여 속임수를 쓰세요
    let codes = {
      "+49": "독일",
      "+41": "스위스",
      "+44": "영국",
      // ..,
      "+1": "미국"
    };
    
    for (let code in codes) {
      console.log( +code ); // 49, 41, 44, 1
    }
    ```
    
- 단항 연산자 `+`
    - JS에서는 숫자로 변환하는 연산자로도 사용
    
    ```jsx
    // 예시
    console.log(+"49"); // 49 (문자열 → 숫자)
    console.log(+"hello"); // NaN (숫자로 변환 불가능)
    console.log(+true); // 1
    console.log(+false); // 0
    
    // 그래서 우리 위 코드에서 + 연산자가 있기 때문에 문자열을 숫자로 변환하려고 시도하게 됩니다.
    // 즉, console.log( +"+49" ) 에서 "+49" 앞에 + 가 붙었으니
    // 해당 문자열을 숫자로 바꾸려고 시도하여 49 가 출력되는 것임
    
    ```