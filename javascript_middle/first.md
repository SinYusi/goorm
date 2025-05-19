## 템플릿 리터럴

ES6는 새로운 문자열 표기법으로 템플릿 리터럴을 도입했다. 이게 뭐냐면 빽틱(```)을 사용해서 문자열을 나타내는 것이다.

```jsx
const template = `템플릿 리터럴은 '작은따옴표(single quotes)'과 "큰따옴표(double quotes)"를 혼용할 수 있다.`;

console.log(template);
```

일반 문자열은 줄바꿈이 안되고, 공백 표현이 어려웠는데, 템플릿 리터럴은 여러 줄에 걸쳐 작성할 수도 있고, 공백도 그대로 적용된다. 또한, 문자열 안에 변수도 사용할 수 있다는 장점이 있다.

## Rest 파라미터

- `Rest Parameter` : 나머지 매개변수는 함수에 전달된 인수들의 목록을 배열로 전달받음.
    
    ```jsx
    function foo(...rest) {
      console.log(Array.isArray(rest)); // true
      console.log(rest); // [ 1, 2, 3, 4, 5 ]
    }
    
    foo(1, 2, 3, 4, 5);
    
    // 함수에 전달된 인수들은 순차적으로 파라미터와 rest 파라미터에 할당됨
    function foo(param, ...rest) {
      console.log(param); // 1
      console.log(rest);  // [ 2, 3, 4, 5 ]
    }
    
    foo(1, 2, 3, 4, 5);
    
    function bar(param1, param2, ...rest) {
      console.log(param1); // 1
      console.log(param2); // 2
      console.log(rest);   // [ 3, 4, 5 ]
    }
    
    bar(1, 2, 3, 4, 5);
    ```
    

즉, 나머지 매개변수라는 이름 그대로 먼저 선언된 파라미터에 할당된 인수를 제외한 나머지 인수들이 모두 배열에 담겨 할당된다.

그래서 Rest 파라미터는 반드시 마지막 파라미터여야 한다.

ES5에서는 함수의 매개변수 개수를 사전에 알 수 없는 경우를 위해 arguments 객체를 사용했다.

arguments 객체는 배열로 반환해주는 복잡한 과정을 거쳐야 했다.

하지만 ES6의 Rest 파라미터가 나오면서 귀찮은 과정이 사라진 것이다.

Rest 파라미터가 매개변수들을 배열로 받아오니까.

- ES5에서 Rest 파라미터 대신 사용했던 문법
    
    ```jsx
    function sum(...args) {
      console.log(arguments); // Arguments(5) [1, 2, 3, 4, 5, callee: (...), Symbol(Symbol.iterator): ƒ]
      let changeArguments = Array.prototype.slice.call(arguments); // 객체를 배열로 변환
      console.log(changeArguments); // (5) [1, 2, 3, 4, 5]
      
      console.log(args); // (5) [1, 2, 3, 4, 5]
      console.log(Array.isArray(args)); // true
      
      return args.reduce((pre, cur) => pre + cur);
    }
    
    console.log(sum(1, 2, 3, 4, 5)); // 15
    ```
    
    ES6에 추가된 화살표 함수에는 arguments 프로퍼티가 없다는 것을 주의하자 → ES6에서의 화살표 함수로는 arguments를 활용한 Rest 파라미터 작동 불가
    

## Spread 문법

스프레드 연산자(`…`)는 대상을 개별 요소로 분리한다. 단, 대상은 반드시 이터러블이어야 한다.

- `…[1, 2, 3]` 는 `[1, 2, 3]` 을 개별 요소로 분리한다(→ 1, 2, 3)
    
    ```jsx
    console.log(...[1, 2, 3]) // 1, 2, 3
    ```
    
- 문자열은 이터러블이다.
    
    ```jsx
    console.log(...'Hello');  // H e l l o
    ```
    
- `Map`과 `Set`은 이터러블이다.
    
    ```jsx
    console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ] [ 'b', '2' ]
    console.log(...new Set([1, 2, 3]));  // 1 2 3
    ```
    
- 이터러블이 아닌 일반 객체는 Spread 문법의 대상이 될 수 없다.
    
    ```jsx
    console.log(...{ a: 1, b: 2 });
    // TypeError: Found non-callable @@iterator
    ```
    

ES6의 Spread 문법(`…`)을 사용한 배열을 인수로 함수에 전달하면, 배열의 요소를 분해하여 순차적으로 파라미터에 할당하게 된다.

- 예시
    - 다음 함수가 있다.
        
        ```jsx
        function foo(x, y, z) {
          console.log(x); // 1
          console.log(y); // 2
          console.log(z); // 3
        }
        ```
        
    - 다음 배열의 각 요소를 foo 함수의 인자로 전달하려고 한다.
        
        ```jsx
        const arr = [1, 2, 3];
        ```
        
    - `…[1, 2, 3]` 은 `[1, 2, 3]` 을 개별 요소로 분리한다(→ 1, 2, 3). spread 문법에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
        
        ```jsx
        foo(...arr);
        ```
        
    - Rest 파라미터는 spread 문법을 사용하여 파라미터를 정의한 것을 의미한다. 형태가 동일하기에 혼동할 수 있다. Spread 문법을 사용한 매개변수를 “정의”하는 것이 Rest 파라미터이고, `…rest` 는 분리된 요소들을 함수 내부에 배열로 전달한다.
        
        ```jsx
        function foo(param, ...rest) {
          console.log(param); // 1
          console.log(rest);  // [ 2, 3 ]
        }
        foo(1, 2, 3);
        ```
        
    - Spread 문법을 사용한 인수는 배열 인수를 분리하여 순차적으로 매개변수에 할당한다. 반면, 함수에 인수로 “넘겨줄 때” 사용하는 것이 Spread 문법이다. `…[1, 2, 3]` 는 `[1, 2, 3]` 을 개별 요소로 분리한다(→ 1, 2, 3). spread 문법에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
        
        ```jsx
        function bar(x, y, z) {
          console.log(x); // 1
          console.log(y); // 2
          console.log(z); // 3
        }
        bar(...[1, 2, 3]);
        ```
        
- spread 문법을 어떻게 유용하게 쓸까?
    - `concat()`
        
        ```jsx
        // ✅ ES5
        var arr = [1, 2, 3];
        console.log(arr.concat([4, 5, 6])); // [ 1, 2, 3, 4, 5, 6 ]
        
        // ✅ ES6
        const arr = [1, 2, 3];
        // ...arr은 [1, 2, 3]을 개별 요소로 분리한다
        console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]
        ```
        
    - `push()` : 배열에 배열을 push하고 싶을 때
        
        ```jsx
        // ✅ ES5
        var arr1 = [1, 2, 3];
        var arr2 = [4, 5, 6];
        
        // apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
        Array.prototype.push.apply(arr1, arr2);
        
        console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
        
        // ✅ ES6
        const arr1 = [1, 2, 3];
        const arr2 = [4, 5, 6];
        
        // ...arr2는 [4, 5, 6]을 개별 요소로 분리한다
        arr1.push(...arr2); // == arr1.push(4, 5, 6);
        
        console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
        ```
        
    - `slice()` : 간단하게 배열 복사 가능
        
        ```jsx
        // ✅ ES5
        var arr  = [1, 2, 3];
        var copy = arr.slice();
        
        console.log(copy); // [ 1, 2, 3 ]
        
        // copy를 변경한다.
        copy.push(4);
        
        console.log(copy); // [ 1, 2, 3, 4 ]
        // arr은 변경되지 않는다.
        console.log(arr);  // [ 1, 2, 3 ]
        
        // ✅ ES6
        const arr = [1, 2, 3];
        // ...arr은 [1, 2, 3]을 개별 요소로 분리한다
        const copy = [...arr];
        
        console.log(copy); // [ 1, 2, 3 ]
        
        // copy를 변경한다.
        copy.push(4);
        
        console.log(copy); // [ 1, 2, 3, 4 ]
        // arr은 변경되지 않는다.
        console.log(arr);  // [ 1, 2, 3 ]
        ```
        

## 구조 분해 할당 (Destructuring)

배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript의 표현식이다.

아래 코드를 먼저 살펴보자

```jsx
let a, b, rest; // 변수 한번에 선언

[a, b] = [10, 20]; // a에는 10이 들어가고, b에는 20이 들어감(같은 자리에 할당됨)
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20

({ a, b, ...rest } = { a: 10, b: 20, c: 30, d: 40 });
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```

- 배열 구조 분해
    
    우선 기본 변수 할당 방식은 아래와 같다. 일반적인 방법이라고 할 수 있다.
    
    ```jsx
    let foo = ["one", "two", "three"];
    
    let [red, yellow, green] = foo; // foo배열과 똑같은 구성에 안에 변수만 만들어주면 됨
    console.log(red); // "one"
    console.log(yellow); // "two"
    console.log(green); // "three"
    ```
    
    변수의 선언을 따로 분리하고 싶다면?
    
    ```jsx
    let a, b;
    
    [a, b] = [1, 2];
    console.log(a); // 1
    console.log(b); // 2
    ```
    
    변수 값 교환도 가능하다만, 헷갈릴 수 있으므로 가급적 사용을 자제하는 것이 좋다.
    
    ```jsx
    let a = 1;
    let b = 3;
    
    [a, b] = [b, a];
    console.log(a); // 3
    console.log(b); // 1
    ```
    
    변수에 배열의 나머지를 할당할 수도 있다. (with spread)
    
    ```jsx
    let [a, ...b] = [1, 2, 3];
    console.log(a); // 1
    console.log(b); // [2, 3]
    ```
    
- 객체 구조 분해
    
    기본 객체를 구조 분해 할당하는 방법이다.
    
    key값을 변수처럼 사용하여 가져오면 된다.
    
    ```jsx
    let o = { p: 42, q: true };
    let { p, q } = o;
    
    console.log(p); // 42
    console.log(q); // true
    ```
    
    key값 말고, 새로운 이름의 변수에 값을 할당하고 싶다면
    
    ```jsx
    let o = { p: 42, q: true };
    let { p: foo, q: bar } = o;
    
    console.log(foo); // 42
    console.log(bar); // true
    ```
    

## 스코프란? (= Scope, 유효범위)

자바스크립트에서 스코프를 구분하면 전역/지역 스코프로 나눌 수 있다.

1. 전역 스코프: 코드 어디에서든지 참조 가능
2. 지역 스코프(혹은 함수 레벨 스코프): 함수 코드 블록이 만든 스코프. 즉, 함수 자신과 하위 함수에서만 참조 가능

또한 모든 변수는 스코프를 갖는다. 변수 관점에서 스코프를 구분하면

1. 전역 변수: 전역에서 선언된 변수, 어디에서든지 참조 가능
2. 지역 변수: 지역(함수) 내에서 선언된 변수, 그 지역과 그 지역의 하부 지역에서만 참조 가능

```jsx
// Error!
function exampleFunction() {
	// 변수 x는 지역 변수가 되어 이 함수안에서만 사용 가능합니다.
  const x = "declared inside function"; 
  console.log("Inside function");
  console.log(x);
}

console.log(x); // Causes error: 함수 안의 변수 접근 불가능

// ✅ 변수를 함수 외부로 옮겨 전역 변수로 만들면 가능
const x = "declared outside function";

exampleFunction();

function exampleFunction() {
  console.log("Inside function");
  console.log(x); // 전역 변수니까 함수 안에서도 사용 가능
}

console.log("Outside function");
console.log(x);
```

자바스크립트는 기본적으로 함수 레벨 스코프로 동작하는 프로그래밍 언어였다.

하지만 ES6 이후 도입된 `let`, `const` 키워드를 통해 블록 레벨 스코프를 도입하게 되었다.

1. 함수 레벨 스코프
    
    함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다.
    
    즉, 함수 내부에서 선언한 변수는 지역 변수이며, 함수 외부에서 선언한 변수는 모두 전역 변수이다.
    
    ```jsx
    // 함수 레벨 스코프인 var는 함수가 아닌 일반 코드 블럭{}에 선언하면 전역 변수가 됨
    {
      var x = 1;
    }
    console.log(x); // 1 -> 코드 블럭 외부에서 참조 가능
    
    // 함수 안에서 선언하면 지역 변수가 됨
    function functionLevel () {
    	var y = 1 // 함수 안에 선언되어 지역 변수가 됨, 함수 밖에서 접근 불가능
    	console.log(y)
    }
    functionLevel() // 1
    console.log(y) // ReferenceError: y is not defined
    ```
    
    그렇기에 if문, for문과 같은 코드 블럭은 인식되지 않기에, 의도치 않은 저역 변수 선언과 재할당과 같은 부작용이 발생할 수 있다.
    
2. 블록 레벨 스코프
    
    모든 코드 블록(함수, if문, for문, while문, try/catch문 등 `{ }` 를 활용하는 코드) 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.
    
    즉, 코드 블록 내부에서 선언한 변수는 지역 변수이다.
    
    ```jsx
    // 블록 레벨 스코프는 코드 블럭도 로컬 스코프로 인식함
    // 로컬 스코프로 인식하기 때문에 해당 코드 블록에서만 사용할 수 있는 지역 변수가 됨
    {
      const x = 1;
      console.log(x); // 1
    }
    console.log(x); // ReferenceError: x is not defined
    ```
    

## `var` vs `let` vs `const`

- `var`
    
    `var` 키워드는 왜 버려졌을까?
    
    아래와 같은 특징은 주의를 기울이지 않으면 심각한 문제를 일으키기 때문이다.
    
    1. 함수 레벨 스코프를 따름
        
        ```jsx
        // var 로 선언하면 for문을 위해 선언한 변수가 외부에서 참조 가능함..
        for(var a = 0; a < 5; a++) {
        	console.log(a)
        }
        
        console.log('?? :', a) // 값을 가져와버림..
        
        // 반대로 let 키워드로 선언하면
        for(let b = 0; b < 5; b++) {
        	console.log(b) // 여기서만 b 변수 참조 가능
        }
        
        console.log('!! :', b) // 여기서는 b 변수 참조 불가능(이게 정상이지)
        ```
        
        1. 함수의 코드 블록만 스코프로 인정하기 때문에 그 외는 전부 전역 변수가 됨
    2. `var` 키워드 생략 허용
        
        아무도 모르게 변수 만들어서 암묵적 전역 변수를 양산할 가능성이 크다.
        
    3. 변수 중복 선언(+초기화) 허용
        
        의도하지 않은 변수값의 변경이 일어날 가능성이 있다. 변수를 모두 외울 수는 없기 때문.
        
    4. 변수 호이스팅으로 선언하기 전 사용 가능
        
        ```jsx
        console.log(B);  // undefined
        
        var B = 10;
        
        console.log(B);  // 10
        ```
        
        `var`로 선언하면 변수를 선언하기 전에도 참조할 수 있다.
        
- `let` & `const` 차이점
    - `let`
        
        값의 재할당이 가능하다. 변수 선언 및 초기화 이후에 반복해서 다른 값이 재할당이 가능하단 것이다.
        
        ```jsx
        // ✅ 값 재할당 가능
        let name = 'lisa'
        name = 'mandoo'
        console.log(name) // mandoo
        
        // ✅ 변수만 선언해두고, 나중에 값을 할당해도 문제 없음
        let name;
        name = 'mandoo'
        console.log(name)
        ```
        
    - `const`
        
        값의 재할당 불가능
        
        1. 처음에 선언 및 초기화하고 나면 다른 값 재할당이 불가능 (한 번 정해지면 끝)
        2. `const` 변수는 선언과 동시에 정의해야 함
        3. 
        
        ```jsx
        // ❌ 이미 값이 정해진 변수에 재할당 불가능
        const name = 'lisa'
        name = 'mandoo'
        console.log(name)
        
        // ✅ 선언과 동시에 정의하면 문제 없음
        const bbb = 3;
        console.log(bbb)
        
        // ❌ 변수 선언만 하고 값을 정의하지 않았을 때 에러남
        const aaa;
        aaa = 3;
        console.log(aaa) // SyntaxError: Missing initializer in const declaration
        ```
        
- `let` & `const` 공통점
    1. 블록 레벨 스코프
        
        실수로 전역 변수를 만들 일이 거의 없다.
        
    2. 중복 선언 불가능
        
        이미 선언한 변수를 다시 선언할 경우, 에러가 발생한다 → 훨씬 안전
        
    3. 변수 호이스팅 발생하지만 `var` 와는 다른 방식으로 작동
        
        `var`는 변수를 정의하는 코드 전에도 해당 변수를 사용할 수 있었다. 하지만, `let` 과 `const` 는 변수 호이스팅이 일어나지만, 초기화는 진행하지 않는다.
        
        - `var`
            
            ```jsx
            console.log(a);  // undefined -> 에러는 안남
            var a = 10;
            console.log(a); // 10
            ```
            
        - `var` 코드 동작 순서를 코드로 표현(이해를 돕기 위함)
            
            ```jsx
            var a = undefined; // 아래에 있던 변수를 상단으로 끌어올린 후 할당된 값이 있음에도 불구하고 undefined로 초기화 값을 넣음
            console.log(a) // 그래서 에러 안나고 undefined 출력
            a = 10; // 이제 값이 할당됨
            console.log(a) // 이제는 제대로 할당된 값이 출력
            ```
            
        - `let`
            
            ```jsx
            console.log(a);  // ReferenceError: a is not defined -> 에러남
            let a = 10;
            ```
            
        - `let` 코드 동작 순서를 코드로 표현
            
            ```jsx
            let a; // 아래에 있던 변수만 끌어올려 선언만 하고 값을 정의는 하지 않음
            console.log(a);  // ReferenceError: a is not defined -> 당연히 할당된 값이 없으니 a 라는 변수만 있고 값은 없어서 출력할 수가 없음
            a = 10; // 이제야 값이 제대로 할당됨
            console.log(a); // 제대로 할당된 값이 출력됨
            ```
            

## 호이스팅 Hoisting

자바스크립트는 모든 선언(let, const, var, function, class)을 호이스팅한다.

- 호이스팅이란?
    
    코드를 실행하기 전에 함수, 변수, 클래스 또는 import의 선언문을 해당 범우의 맨 위로 끌어올리는 것처럼 보이는 현상을 말함.
    
    즉, 변수 선언, 함수 선언 등을 코드의 맨 위로 끌어 올려지는 것처럼 보이는 현상이라고 볼 수 있음
    
- 호이스팅이 발생하는 원인
    
    이유는 자바스크립트의 변수 생성과 초기화 작업이 분리돼서 진행되기 때문이다.
    
    예제를 먼저 보자.
    
    ```jsx
    console.log(a()); // 'a'
    console.log(b()); // Uncaught TypeError: b is not a function
    console.log(c()); // Uncaught TypeError: b is not a function
    
    // 함수 선언식
    function a() {
        return 'a';
    }
    // 기명 함수 표현식
    var b = function bb() {
        return 'bb';
    }
    // 익명 함수 표현식
    var c = function() {
        return 'c';
    }
    ```
    
    위 코드를 보면, a 함수 실행 시에는 에러가 안나고, 값도 출력된다.
    
    a 함수가 정의 되기도 전에 사용했는데 에러가 나지 않는다. << 이상함
    
    이렇게 되는 이유는 호이스팅에 의해 실제 자바스크립트 컴파일은 아래와 같이 이뤄지기 때문이다.
    
    아래 코드를 살펴보자. 실제로 코드가 이렇게 바뀐다는 것은 아니다. 이해를 돕기 위해 코드를 옮긴 것
    
    ```jsx
    // ⚠️ 실제로 코드가 이렇게 바뀐다는 것은 아님, 이해를 돕기 위해 코드를 옮긴 것입니다.
    
    // 함수 선언식으로 정의된 함수는 가장 상단에 함수 코드가 전부 끌어올려집니다.
    function a() {
        return 'a';
    }
    
    // 함수 표현식으로 정의된 함수는 해당 함수명의 선언 부분만 올라옵니다. (함수본문은 올라오지X)
    // 즉, 얘네는 아직 그냥 변수에 불과합니다.
    var b;
    var c; 
    
    console.log(a()); // 함수 본문 코드까지 위에 올라왔으니 여기서 사용 가능해짐
    console.log(b()); // 함수명 즉, 변수명만 있어서 b가 함수인지도 모르니 에러가 나는 것임
    console.log(c()); // 위에서 에러나서 얘는 실행도 안됨
    
    // 이제서야 해당 변수에 함수 본문 코드가 값으로 할당됨
    b = function bb() {
        return 'bb';
    }
    // 이제서야 해당 변수에 함수 본문 코드가 값으로 할당됨
    c = function() {
        return 'c';
    }
    ```
    
    함수 선언식인지, 함수 표현식인지에 따라 호이스팅되는 방식이 다르다.
    
    ```jsx
    // 함수 선언식 -> 함수 전체가 호이스팅됨
    function add(x, y) {
      return x + y;
    }
    
    // 함수 표현식 -> 함수명 즉, 변수 선언만 호이스팅됨 (✅ 권장)
    const add = function(x, y) {
      return x + y;
    };
    ```
    
    함수 표현식을 권장하는 이유는 위에서 아래로 읽어내려가는 것이 익숙한 인간 개발자에게 예측 가능한 코드를 작성할 수 있도록 하기 위함이다.
    
    호이스팅이 필요하다면 선언식을 사용하면 되고, 그게 아니라면 표현식을 사용하면 된다. 정답이란건 없다.
    
    이제 변수 호이스팅에 대해 알아보자.
    
    먼저, var로 변수를 만들면 어떻게 되는지 보자.
    
    ```jsx
    var globalNum = 10;     // globalNum을 전역 변수로 선언함.
    
    function printNum() {
        console.log(globalNum);
        var globalNum = 20; // globalNum을 지역 변수로 선언함.
        console.log(globalNum);
    }
    
    printNum(); 
    // 출력 결과
    // undefined
    // 20
    ```
    
    왜 `undefined` 가 뜰까? 그것은 바로 호이스팅 때문이다.
    
    ```jsx
    // ⚠️ 변수 호이스팅 이해를 돕기 위한 코드
    
    var globalNum = 10;
    
    function printNum() {
    		// 함수 호이스팅에 의해 변수의 선언 부분이 함수의 맨 처음 부분으로 이동됨
    		// 심지어 var 로 선언되었기 때문에 undefined 값으로 초기값이 할당됨
        var globalNum; // 함수 내에서도 호이스팅이 일어난다는 것임
        console.log(globalNum); // undefined -> 함수 내부에 변수가 있기 때문에 함수 밖에 있는 변수에 접근할 필요 없음
        globalNum = 20; // 이제서야 제대로 된 값 할당됨
        console.log(globalNum); // 20
    }
    
    printNum();
    ```
    
    이번엔 `let`, `const` 의 호이스팅 방식을 알아보자.
    
    ```jsx
    console.log(a);  // ReferenceError: a is not defined
    let a = 20;  // 지역변수 a 선언
    
    // ⚠️ 위 코드의 변수 호이스팅 이해를 돕기 위한 코드입니다
    
    let a; // 변수 선언 부분만 끌어올려지고 아무 값도 할당되지 않습니다 = TDZ라고 합니다
    console.log(a);  // ReferenceError: a is not defined -> 변수에 값이 없으니 에러가 납니다
    a = 20;  // 이제야 값이 할당됩니다
    ```
    
    - TDZ = Temporal Dead Zone, 변수의 선언과 초기화 사이에 일시적으로 변수 값을 참조할 수 없는 구간
    
    전역 변수, 지역 변수가 있을 때에는 어떻게 될까?
    
    ```jsx
    let name = 'lisa'
    
    if(true) {
        console.log(name) // ReferenceError: Cannot access 'name' before initialization
        let name = 'mandoo'
    }
    ```
    
    위 코드에서 같은 변수를 지역 변수로 if문에 다시 선언했다.
    
    같은 이름의 전역 변수가 있지만 에러가 발생한다. 호이스팅 때문
    
    ```jsx
    // ⚠️ 위 코드의 변수 호이스팅 이해를 돕기 위한 코드
    
    let name = 'lisa'
    
    if(true) {
    		let name; // 변수 선언 부분만 코드 블럭 최상단으로 끌어올려짐 = TDZ
        console.log(name) // 해당 변수에 할당된 값이 없기 때문에 에러
        name = 'mandoo' // 이제서야 값이 할당됩니다
    }
    ```
    
    참고로 지역변수가 전역 변수보다 우선 순위를 가진다. 그래서 `console.log(name)` 에서 코드 블록 안의 지여견수 name을 먼저 찾은 것이다.
    

## Class 문법 살펴보기 (ES6 클래스 문법 기준)

일반 함수와 생성자 함수(클래스)의 구분을 위해, 생성자 함수 이름은 파스칼 케이스(PascalCase)로 작성해야 한다. 이렇게 정의한 생성자 함수를 Class라고 부른다.

- 생성자 함수 = 클래스
- 인스턴스 : new 키워드로 호출하는 생성자 함수로부터 반환되는 데이터
- 예시 코드
    
    ```jsx
    class Person {
       // 생성자 함수 본문 코드는 클래스 안에 `constructor`라는 이름으로 정의
       constructor({name, age}) { // 실질적 생성자 함수
         this.name = name;
         this.age = age;
       }
       // 객체에서 메소드를 정의할 때 사용하던 문법을 그대로 사용하면, 
       // 메소드가 자동으로 `Person.prototype`에 저장됨
       // 즉, 이 introduce 메소드가 Person이라는 객체의 프로토타입에 저장됨.
       introduce() {
         return `안녕하세요, 제 이름은 ${this.name}입니다.`;
       }
    }
    
    // 여기서 person이 인스턴스 입니다.
    const person = new Person({name: '만두', age: 2});
    
    console.log(person.introduce()); // 안녕하세요, 제 이름은 만두입니다.
    ```
    
- `constructor` : 인스턴스를 생성하고 클래스 필드를 초기화하기 위한 특수 메서드 (클래스 내에 1개만 존재)
    
    ```jsx
    class Person {
       height = 180; // 인스턴스 변수
    
       // constructor는 이름을 바꿀 수 없다.
       constructor(name, age) {
          // this는 클래스가 생성할 인스턴스를 가리킨다. 즉, 아래 person1 에서는 person1 = this
          this.name = name;
          this.age = age;
       }
    }
    
    let person1 = new Person('john', 23);
    
    console.log(person1.name); // john
    console.log(person1.age); // 23
    console.log(person1.height); // 180
    ```
    
- `메서드 정의`
    
    ```jsx
    class Calculator {
       add(x, y) {
         return x + y;
       }
       subtract(x, y) {
         return x - y;
       }
     }
     
     let calc = new Calculator();
     
     console.log(calc.add(1,10)); // 11
     console.log(calc.subtract(10,1)); // 9
    ```
    
- `extends` : 클래스 상속 기능. 한 클래스의 기능을 다른 클래스에서 재사용이 가능하다.
    
    ```jsx
    class Parent {
      // ...
    }
    
    class Child extends Parent {
      // ...
    }
    ```
    
- `#` : 클래스의 모든 메서드는 `public`으로 지정되는데, `#` 을 사용하면 비공개로 설정이 가능하다.
    
    ```jsx
    // ✅ private을 사용하지 않았을 때
    class myClass {
    		// private 변수
        #num = 100
        
        // public 메서드
        privMethod(){
            console.log(this.#num); // 프라이빗 변수 호출
        }
        
        publicMethod() {
            this.privMethod(); // public 메소드 호출
        }    
    }
     
    let newClass = new myClass();
    
    // ✅ private을 사용하지 않은 메서드이기 때문에 인스턴스를 통해 호출 가능
    newClass.publicMethod() // 100
    newClass.privMethod() // 100
    
    // private을 사용할 때
    class myClass {
    		// private 변수
        #num = 100
        
        // private 메서드
        #privMethod(){
            console.log(this.#num); // 프라이빗 변수 호출
        }
        
        publicMethod() {
            this.#privMethod(); // 프라이빗 메소드 호출
        }    
    }
     
    let newClass = new myClass();
    
    // public메서드는 호출 가능, private 메서드는 호출 불가(접근할 수 없음)
    newClass.publicMethod() // 100
    newClass.privMethod() // TypeError: newClass.privMethod is not a function
    ```
    

## 객체 지향 프로그래밍이란? (OOP)

실시계에 존재하고 인지하고 있는 객체(Object)를 소프트웨어 세계에서 표현하기 위해 객체의 핵심적인 개념 또는 기능만을 추출하는 추상화(abstraction)를 통해 모델링하려는 프로그래밍 패러다임이다.

쉽게 말해, 코드를 정리하는 하나의 방식이다. 데이터에 대한 생각, 구조 방식이라고도 볼 수 있다.

예시로, 게임을 만든다고 가정할 때 플레이어 객체가 필요하다.

각 플레이어마다 가지고 있는 데이터는 모두 다를 것이다.

아래처럼 플레이어 데이터 객체를 만들 수 있지만, 플레이어가 1천명으로 늘어난다면 객체를 1천개 만들어야 한다.

```jsx
const player1 = {
	name: 'mandoo',
	age: 2,
	health: 99,
	skill: '벌러덩 스킬'
}
const player2 = {
	name: 'gogi-mandoo',
	age: 1,
	health: 100,
	skill: '만두 깨물기 스킬'
}
// ... 숫자가 늘어나면 객체를 그만큼 만들어야 함 🤮
```

만들다 보면 패턴이 보인다. 계속해서 공통적으로 들어가야하는 부분들 말이다.

```jsx
// 모든 플레이어 객체가 같은 프로퍼티(key)를 가지고 있다. 다른점은 데이터(value) 뿐
name: 'mandoo',
age: 2,
health: 99,
skill: '벌러덩 스킬'
```

또한, 객체를 직접 선언하며 코드를 쓰다보면 사람이 작성하는지라 오타를 낼 수도, 속성을 빼먹을 수도 있다.

만약 플레이어에게 또 다른 새로운 속성을 추가하고 싶다면, 일일히 객체에 추가해줘야 한다.

이렇게 번거로운 작업들이 생겨날 수 있기에 어떠한 틀이 있으면 되지 않을까 싶다.

그 때 사용하는 개념이 `Class` 이다.

클래스는 객체를 위한 붕어빵 틀같은 것이다.

같은 틀에서 나온 붕어빵이지만, 속에는 피자, 슈크림, 팥 등이 들어갈수도 있는 것이다.

- 위 예시를 클래스에 적용해보면
    
    ```jsx
    // 위 예시를 클래스 문법에 적용해 본다면
    
    // 붕어빵 틀을 만들어주고
    class Player {
    	// 클래스에 들어가는 함수를 메서드라고 함.
    	// constructor 가 인스턴스를 생성하기 위한 메서드
    	constructor(name, age, health, skill) {
    		this.name = name;
    		this.age = age;
    		this.health = health;
    		this.skill = skill;
    		this.xp = 0; // 경험치 속성 1만번 추가할 필요 없음
    	}
    	playerHeal() {
    		this.health = 100
    	}
    	playerTakeHit() {
    		this.health = this.health - 5
    	}
    }
    
    // 편하게 갖다 씁니다, 이제 코드 복사할 필요 없음
    const mandoo = new Player("mandoo", 2, 99, "발라당 스킬")
    mandoo.playerTakeHit()
    console.log(mandoo)
    mandoo.playerHeal()
    console.log(mandoo)
    const gogiMandoo = new Player("gogi-mandoo", 1, 100, "만두 깨물기 스킬")
    ```