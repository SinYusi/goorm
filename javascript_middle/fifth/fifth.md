## 이벤트 버블링 & 캡쳐링

예시 코드를 먼저 보자.

아래 코드를 실행해보면 이벤트 핸들러는 `div`에 있는데 `em`, `code` 태그를 클릭해도 동작한다.

```jsx
<div onclick="alert('div에 할당한 핸들러!')">
  <em><code>EM</code>을 클릭했는데도 <code>DIV</code>에 할당한 핸들러가 동작합니다.</em>
</div>
```

이 때 필요한 개념이 버블링과 캡쳐링이다.

- 버블링 bubbling
    
    한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작한다.
    
    가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작한다.
    
    코드를 실행시켜보자.
    
    아래 코드는 `form` > `div` > `p` 의 중첩된 구조인데 요소 각각에 클릭 이벤트 핸들러가 할당되어 있다.
    
    ```jsx
    <style>
      body * {
        margin: 10px;
        border: 1px solid blue;
      }
    </style>
    
    <form onclick="alert('form')">FORM
      <div onclick="alert('div')">DIV
        <p onclick="alert('p')">P</p>
      </div>
    </form>
    ```
    
    위 코드에서 `p` 코드를 클릭하면 다음과 같은 순서대로 벌어진다.
    
    1. `<p>` 에 할당된 `onClick` 핸들러가 동작
    2. 바깥의 `<div>` 에 할당된 핸들러가 동작
    3. 그 바깥의 `<form>` 에 할당된 핸들러가 동작
    4. `document` 객체를 만날 때까지, 각 요소에 할당된 `onClick` 핸들러가 동작
    
    위 흐름이 바로 이벤트 버블링이다.
    
    거의 모든 이벤트는 버블링된다고 보면 된다.
    
    그럼 버블링을 막을 수는 없을까?
    
    핸들러에게 이벤트를 완전히 처리 후 버블링을 중단하도록 명령할 수 있다.
    
    그 명령어는 `event.stopPropagation()` 이다.
    
    ```jsx
    <body onclick="alert(`버블링은 여기까지 도달하지 못합니다.`)">
      <button onclick="event.stopPropagation()">클릭해 주세요.</button>
    </body>
    ```
    
    하지만 꼭 필요한 경우를 제외하고는 버블링을 막지 않는 것이 좋다.
    
- 캡처링 capturing
    
    자주 쓰이지는 않지만 개념은 알아두자.
    
    캡처링은 이벤트가 하위 요소로 전파되는 단계다.
    
    캡처링 단계를 이용해야 하는 경우는 흔치 않기에, 캡처링에 관한 코드를 발견하는 일은 거의 없을 것이다.
    
    그럼에도 캡처링을 써야하는 상황이라면 `addEventListener` 의 `capture` 옵션을 `true` 로 설정해주면 된다.
    
    기본값은 `false` 로 버블링 단계에서 동작한다.
    
    ```jsx
    elem.addEventListener(..., {capture: true})
    // 아니면, 아래 같이 {capture: true} 대신, true를 써줘도 됩니다.
    elem.addEventListener(..., true)
    ```
    
    - 캡처링 예시 코드
        
        ```jsx
        <style>
          body * {
            margin: 10px;
            border: 1px solid blue;
          }
        </style>
        
        <form>FORM
          <div>DIV
            <p>P</p>
          </div>
        </form>
        
        <script>
          for(let elem of document.querySelectorAll('*')) {
            elem.addEventListener("click", e => alert(`캡쳐링: ${elem.tagName}`), true);
            elem.addEventListener("click", e => alert(`버블링: ${elem.tagName}`));
          }
        </script>
        ```
        
        위 코드에서 `<p>` 를 클릭하면 다음과 같은 순서로 이벤트가 전달된다.
        
        1. HTML → BODY → FORM → DIV (캡처링 단계, 첫 번째 리스너)
        2. P (타깃 단계, 캡쳐링과 버블링 둘 다에 리스너를 설정했기에 두 번 호출)
        3. DIV →