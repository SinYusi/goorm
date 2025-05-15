## form 이벤트로 조작하기

- `focus` & `blur` 이벤트
    - `focus` 이벤트: 요소가 포커스 받을 때
    - `blur` 이벤트: 요소가 포커스를 잃을 때
    - 예시 코드
        
        ```jsx
        <!DOCTYPE html>
        <html lang="en">
          <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>Document</title>
            <style>
              .invalid {
                border-color: red;
              }
              #error {
                color: red;
              }
            </style>
          </head>
          <body>
            이메일: <input type="email" id="email-input" />
        
            <div id="error"></div>
        
            <script>
              const emailInput = document.getElementById("email-input");
              
              // blur 핸들러에선 필드에 이메일이 잘 입력되었는지 확인하고 
              // 잘 입력되지 않은 경우엔 에러를 보여줍니다.
              emailInput.onblur = function () {
                if (!emailInput.value.includes("@")) {
                  // @ 유무를 이용해 유효한 이메일 주소가 아닌지 체크
                  emailInput.classList.add("invalid");
                  error.innerHTML = "올바른 이메일 주소를 입력하세요.";
                }
              };
        
        			// focus 핸들러에선 에러 메시지를 숨깁니다(이메일 재확인은 blur 핸들러에서 합니다).
              emailInput.onfocus = function () {
                if (emailInput.classList.contains("invalid")) {
                  // 사용자가 새로운 값을 입력하려고 하므로 에러 메시지를 지움
                  emailInput.classList.remove("invalid");
                  error.innerHTML = "";
                }
              };
            </script>
          </body>
        </html>
        
        ```
        
    - 강제로 `focus()` 를 주기
        
        ```jsx
        <!DOCTYPE html>
        <html lang="en">
          <head>
            <meta charset="UTF-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>Document</title>
          </head>
          <body>
        	  <input id="myTextField" value="Text field." />
        		<button id="focusButton">Click to set focus on the text field</button>
        		
            <script>
        	    // focusButton 아이디 요소를 클릭하면 myTextField 아이디 요소에 강제 포커스
        	    document.getElementById("focusButton").addEventListener("click", () => {
        			  document.getElementById("myTextField").focus();
        			});
            </script>
            
          </body>
        </html>
        
        ```
        

## 데이터가 변경될 때 실행되는 이벤트

- `change` : 요소 변경이 끝나면 발생
    
    ```jsx
    // input 처럼 텍스트 입력 요소의 경우 포커스를 잃을 때 change 이벤트가 발생
    <input type="text" onchange="alert(this.value)"/>
    
    // select, checkbox, radio 는 선택값이 변경된 직후 이벤트 발생
    <select onchange="alert(this.value)">
      <option value="">선택하세요.</option>
      <option value="1">옵션 1</option>
      <option value="2">옵션 2</option>
      <option value="3">옵션 3</option>
    </select>
    ```
    
- `input` : 사용자가 값을 수정할 때마다 발생
    
    ```jsx
    // 값을 변경할 때 발생
    <input type="text" id="input"> 
    oninput: <span id="result"></span>
    
    <script>
      input.oninput = function() {
        result.innerHTML = input.value;
      };
    </script>
    ```
    
    - `oninput` 은 절대 못막음
- `cut, copy, paste` : 값을 잘라내기, 복사하기, 붙여넣기할 때 발생
    
    ```jsx
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <input type="text" id="input" />
        
        <script>
    	    // 여러 이벤트에 실행할 코드가 전부 같아서 동시에 작성해줍니다.
          input.oncut =
            input.oncopy =
            input.onpaste =
              function (event) {
                alert(event.type + " - " + event.target.value);
                return false;
              };
        </script>
      </body>
    </html>
    
    ```
    
- `submit` : 폼을 제출할 때 트리거됨
    - 트리거(trigger): 특정 조건이 충족될 때 자동으로 실행되는 코드나 명령
    - `submit` 이벤트는 주로 폼을 서버로 전송하기 전에 내용을 검증하거나 폼 전송을 취소할 때 사용
    - 폼을 전송하는 두 가지 방법
        1. `<input type=”submit”>` 클릭하기
            
            ```jsx
            <!DOCTYPE html>
            <html lang="en">
              <head>
                <meta charset="UTF-8" />
                <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                <title>Document</title>
              </head>
              <body>
                <form id="searchForm">
                  <input type="submit" value="폼 제출" />
                </form>
            
                <script>
                  let form = document.createElement("form");
                  form.action = "https://google.com/search";
                  form.method = "GET";
            
                  form.innerHTML = '<input name="q" value="테스트">';
            
                  // 폼을 제출하려면 반드시 폼이 문서 안에 있어야 합니다.
                  document.body.append(form);
            
                  document.getElementById("searchForm").onsubmit = function () {
                    form.submit();
                    return false;
                  };
                </script>
              </body>
            </html>
            ```
            
        2. `input` 필드에서 포커스 주고 Enter키 누르기
            
            ```jsx
            <!DOCTYPE html>
            <html lang="en">
              <head>
                <meta charset="UTF-8" />
                <meta name="viewport" content="width=device-width, initial-scale=1.0" />
                <title>Document</title>
              </head>
              <body>
                <form></form>
            
                <script>
                  let form = document.createElement("form");
                  form.action = "https://google.com/search";
                  form.method = "GET";
            
                  form.innerHTML = '<input name="q" value="테스트">';
            
                  // 폼을 제출하려면 반드시 폼이 문서 안에 있어야 합니다.
                  document.body.append(form);
                </script>
              </body>
            </html>
            ```
            

## 이벤트의 기본 동작 막기

- `event.preventDefault()`
    
    어떤 이벤트를 명시적으로 처이하지 않은 경우, 해당 이벤트에 대한 기본 동작을 실행하지 않도록 지정한다.
    
    아래 코드를 살펴보자. 원래는 `type=’checkbox’` 를 가진 `input` 을 클릭하면 체크가 되어야 하는 것이 기본 동작인데, `event.preventDefault()` 때문에 이 기본 동작이 막힌다.
    
    ```jsx
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
      </head>
      <body>
        <p>체크박스를 클릭해주세요.</p>
    
        <form>
          <label for="id-checkbox">체크박스:</label>
          <input type="checkbox" id="id-checkbox" />
        </form>
    
        <div id="output-box"></div>
    
        <script>
          const idCheckboxLabel = document.querySelector("#id-checkbox");
          const outputBox = document.getElementById("output-box");
    
          idCheckboxLabel.addEventListener(
            "click",
            function (event) {
              outputBox.innerHTML +=
                "죄송합니다! preventDefault() 때문에 체크할 수 없어요!<br>";
              event.preventDefault(); // 이거 주석처리해보면 기본 동작인 체크 정상 동작함
            },
            false
          );
        </script>
      </body>
    </html>
    
    ```
    
- `event.stopPropagation()`
    
    현재 이벤트가 캡처링/버블링 단계에서 더 이상 전파되지 않도록 방지한다.
    
    - 캡처링과 버블링이란?
        
        → 부모 요소 혹은 자식 요소로 이벤트가 전파되는 것
        
    
    전파를 방지해도 이벤트의 기본 동작은 실행되므로, `stopPropagation()` 이 링크나 버튼의 클릭을 막는 것은 아니다. 위 `preventDefault()` 랑 다르다는 것이다.
    
    ```jsx
    // 이벤트 전파 막기 전 코드
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta
          name="viewport"
          content="viewport-fit=cover, user-scalable=no, width=device-width, initial-scale=1, maximum-scale=1"
        />
        <title>예제1</title>
        <style>
          body {
            border: 2px solid red;
          }
          .div-button {
            background-color: lightblue;
            padding: 10px;
          }
        </style>
      </head>
      <body>
        <div>
          <div class="div-button">날 눌러보소</div>
        </div>
      </body>
      <script>
        document.querySelector(".div-button").addEventListener("click", (e) => {
          alert(".div-button 클릭!");
        });
    
        document.body.addEventListener("click", (e) => {
          alert("body 클릭!");
        });
      </script>
    </html>
    
    // 이벤트 전파 막아보기
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta
          name="viewport"
          content="viewport-fit=cover, user-scalable=no, width=device-width, initial-scale=1, maximum-scale=1"
        />
        <title>예제1</title>
        <style>
          body {
            border: 2px solid red;
          }
          .div-button {
            background-color: lightblue;
            padding: 10px;
          }
        </style>
      </head>
      <body>
        <div>
          <div class="div-button">날 눌러보소</div>
        </div>
      </body>
      <script>
        document.querySelector(".div-button").addEventListener("click", (e) => {
          e.stopPropagation();
          alert(".div-button 클릭!");
        });
    
        document.body.addEventListener("click", (e) => {
          alert("body 클릭!");
        });
      </script>
    </html>
    
    ```
    

## `DOMContentLoaded` 이벤트

브라우저가 HTML을 전부 읽고 DOM 트리를 완성하는 즉시 발생한다. 이미지 파일이나 스타일시트 등의 기타 자원은 기다리지 않는다.

`DOMContentLoaded` 이벤트는 `document 객체`에서 발생한다. 따라서 이 이벤트를 다루려면 `addEventListener`를 사용해야 한다.

다음 코드가 실행되었다는 것은 HTML을 전부 읽고 DOM 트리가 완성되었다는 뜻이다.

```jsx
window.addEventListener("DOMContentLoaded", (event) => {
  console.log("DOM fully loaded and parsed");
});
```

브라우저는 HTML 문서를 처리하는 도중에 `<script>` 태그를 만나면, DOM 트리 구성을 멈추고 `<script>` 를 실행한다.

스크립트 실행이 끝난 후에야 나머지 HTML 문서를 처리하는데, `<script>` 에 있는 스크립트가 DOM 조작 관련 로직을 담고 있을 수 있기에 이런 방지책이 만들어졌다.

따라서 `DOMContentLoaded` 이벤트 역시 `<script>` 안에 있는 스크립트가 처리되고 난 후에 발생한다.

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script>
	    // 아래 script 태그가 더 있으니 얘는 잠시 대기...
      document.addEventListener("DOMContentLoaded", () => {
        alert("DOM이 준비되었습니다!");
      });
    </script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.3.0/lodash.js"></script>

    <script>
      alert("라이브러리 로딩이 끝나고 인라인 스크립트가 실행되었습니다.");
    </script>
  </body>
</html>

```

하지만 예외가 있다. `DOMContentLoaded` 가 `script` 안의 처리를 기다리지 않는 예외사항 두가지를 살펴보자.

1. `async` 속성이 있는 스크립트는 `DOMContentLoaded` 를 막지 않는다.
2. `document.createElement(’script’)` 로 동적 생성되고, 웹페이지에 추가된 스크립트는 `DOMContentLoaded` 를 막지 않음

## 문서와 리소스 로딩: `defer` vs `async`

일반적인 스크립트의 로드 순서부터 알아보자.

![출처 : https://wormwlrm.github.io/2021/03/01/Async-Defer-Attributes-of-Script-Tag.html](attachment:5a5e0180-e187-41a9-a7e0-b74391c75ffc:image.png)

출처 : https://wormwlrm.github.io/2021/03/01/Async-Defer-Attributes-of-Script-Tag.html

위처럼 일반적인 로드 순서에 따라 계속 개발하게 되면 발생하는 문제점이 있다.

1. `script` 에서는 `script` 아래에 있는 DOM 요소에 접근할 수 없다. 따라서 DOM 요소에 핸들러를 추가하는 것과 같은 여러 행위가 불가능해진다.
2. 페이지 위쪽에 큰 용량의 `script` 가 있는 경우 `script` 가 페이지를 막아버린다. 즉, 큰 용량의 `script` 가 전부 다운받고 실행될 때까지 아래쪽 HTML은 볼 수도 없게 된다.

```jsx
<p>...스크립트 앞 콘텐츠...</p>

<script src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

// 1. 만약 위 script 에서 아래 HTML DOM 을 조작한다면? 접근 불가능
// 2. 스크립트 다운로드 및 실행이 끝나기 전까지 아래 내용이 보이지 않습니다.
<p>...스크립트 뒤 콘텐츠...</p>
```

지금까지 작성된 예제들을 보면 `script` 태그를 `body` 태그 끝나기 직전에 넣었다. 

그 이유가 바로 `script` 를 중간이나 위에 넣었을 경우 위에서 살펴보았던 문제점들 때문이었고, 브라우저가 `script` 태그를 읽을 때 HTML 읽는 것(파싱)을 중단하기 때문이었다.

하지만 `body` 직전에 넣는 것도 완벽한 해결책은 아니다. `HTML`이 완전 크다면 `HTML`을 전부 다운로드 받기 전까지 `script`를 다운받지 못하게 될테니 오래 걸리고 페이지도 느려질 것

그래서 브라우저가 스크립트를 병렬로 불러오는 방식을 사용하게 된다.

- `defer (= defer script, 지연 스크립트)`
    
    ![defer script load 순서를 나타낸 이미지](attachment:2cd4e977-62c6-476b-9018-5b1cb6d31523:image.png)
    
    defer script load 순서를 나타낸 이미지
    
    브라우저는 `defer` 속성이 있는 스크립트는 백그라운드에서 다운로드한다.
    
    즉, `defer` 속성이 있는 스크립트를 다운로드 하는 도중에 HTML 파싱이 멈추지 않는다는 것이다.
    
    하지만, defer 속성이 있는 스크립트 실행은 HTML 파싱이 끝날 때까지 지연된다. << `지연 스크립트`
    
    ```jsx
    <p>...스크립트 앞 콘텐츠...</p>
    
    // DOM 준비 완료 -> defer script 실행 -> DOMContentLoaded 이벤트 발생
    <script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>
    
    // 바로 볼 수 있음
    <p>...스크립트 뒤 콘텐츠...</p>
    ```
    
    ```jsx
    // 아래 예시 순서는 이렇습니다.
    // 1. 페이지 콘텐츠는 바로 출력
    // 2. 출력되는 사이에 defer script 다운로드 받아짐
    // 3. 페이지 콘텐츠 완료되면 defer script 실행
    // 4. DOMContentLoaded 는 defer script 실행을 기다렸다가 실행되면 그 이후에 이벤트 발생
    
    <p>...스크립트 앞 콘텐츠...</p>
    
    <script>
      document.addEventListener('DOMContentLoaded', () => alert("`defer` 스크립트가 실행된 후, DOM이 준비되었습니다!")); // (2)
    </script>
    
    <script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>
    
    <p>...스크립트 뒤 콘텐츠...</p>
    ```
    
    `defer` 속성은 외부 스크립트에만 유효하다. 즉, `<script>` 에 `src` 가 없으면 `defer` 속성은 무시된다.
    
    또한, script 실행될 때에는 아래와 같이 long script가 위에 있고, small script가 밑에 있다면 `long.js` 가 실행될 때까지 기다렸다가 `small.js` 가 실행된다. << 짧은 스크립트를 위에 적는 것이 좋음
    
    ```jsx
    <script defer src="long.js"/>
    <script defer src="small.js"/>
    ```
    
- `async (= async script, 비동기 스크립트)`
    
    ![async script load 순서를 나타낸 이미지](attachment:99ce0079-80a8-4634-8619-3e96f60e6c99:image.png)
    
    async script load 순서를 나타낸 이미지
    
    `async` 속성이 붙은 `script` 는 페이지와 완전히 독립적으로 동작한다.
    
    `defer` 와 마찬가지로 백그라운드에서 다운로드되는 것은 동일하다. 즉, HTML 파싱과 async script 다운로드가 동시에 되는 것
    
    그렇다면 defer와의 차이점은?
    
    1. `async` 스크립트가 실행 중일 때에는 HTML 파싱이 멈춤
    2. `DOMContentLoaded` 이벤트와 `async` 스크립트는 서로를 기다리지 않는다. 페이지 구성이 끝난 후에 `async` 스크립트 다운로드가 끝난 경우, `DOMContentLoaded` 는 `async` 스크립트 실행 전에 발생할 수 있다는 것이다.
        
        만약, `async` 스크립트가 너무 짧다면 `DOMContentLoaded`는 `async` 스크립트 실행 후에 발생할 수도 있음
        
        `DOMContentLoaded` 이벤트 외에 다른 스크립트들도 `async` 스크립트를 기다리지 않고, `async` 스크립트도 다른 스크립트를 기다리지 않음
        
    
    그러므로 `async` 스크립트는 실행 순서가 보장되지 않는다.
    
    위 이유 때문에 보통 `defer` 스크립트를 선호한다. `defer` 스크립트가 단순히 다운로드만 먼저 하고, 실행은 HTML 파싱이 끝난 뒤에 이뤄진다고 해도, `DOMContentLoaded` 이벤트가 발생되기 전에는 이미 실행되고, 또 실행 순서도 보장할 수 있기에 가장 범용적으로 사용된다.
    
- 마지막 요약
    - `defer` - DOM 전체에 필요한 스크립트 or 실행 순서가 중요한 경우 사용
    - `async` - 방문자 수 카운트 or 관고 관련 스크립트처럼 독립적인 스크립트 or 실행순서가 중요하지 않은 경우 사용

## `AJAX`란?

`Asynchronous JavaScript and XML`의 약자.

브라우저에 웹페이지를 요청하거나 링크를 클릭하면 화면 갱신이 발생한다. 이는 브라우저와 서버와의 통신에 의한 것

이렇게 서버에서 데이터를 받아오는 과정에서 `AJAX` 없이 원래 웹사이트의 라이프 사이클은 서버에서 요청받은 페이지(즉, `HTML`)를 반환하는데 이 때 HTML에서 로드하는 `CSS`, `JS` 파일도 같이 반환한다.

클라이언트 요청에 따라 서버가 정적인 파일을 반환할 수도, 서버 사이드 프로그램이 만들어낸 파일이나 데이터를 반환할 수도 있다.

서버로부터 웹페이지가 반환되면 클라이언트는 이를 렌더링하여 화면에 표시한다.

![출처 : https://poiemaweb.com/js-ajax](attachment:5b823ea6-d8a3-4a6a-bb27-79c00d8a4e0f:image.png)

출처 : https://poiemaweb.com/js-ajax

`AJAX`라는건 그럼 왜 태어났을까?

서버로부터 웹페이지가 반환되면 화면 전체를 갱신하는 것. 즉, 화면 전체를 새로 고침해준다는 것이 문제였다.

그렇게 `AJAX`가 이런 새로고침을 없애고 서버에게 `GET` 요청하는 `JS` 코드로 태어났다. 유저 몰래 서버로 데이터를 요청하는 것이다.

`AJAX` 는 이 문제를 페이지 일부만 갱신해도 동일한 효과를 볼 수 있도록 하는 방법으로 해결했다.

화면 전체를 새로 고침해주는 것보다 훨씬 빠를 것이고, 웹페이지 전환이 부드러운 화면을 보여줄 수 있다.

그렇기에 이 기술은 복잡하고 동적인 웹페이지를 구성하는 프로그래밍 방식이다.

![출처 : [https://velog.io/@dhrhghdql/React생활코딩16일차React-Ajax](https://velog.io/@dhrhghdql/React%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A916%EC%9D%BC%EC%B0%A8React-Ajax)](attachment:03117229-7bfb-49fb-b671-150e985937e4:image.png)

출처 : [https://velog.io/@dhrhghdql/React생활코딩16일차React-Ajax](https://velog.io/@dhrhghdql/React%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A916%EC%9D%BC%EC%B0%A8React-Ajax)

`AJAX` 를 사용하기 위해
`const XMLHttpRequestObj = newXMLHttpRequest();`
와 같은 코드를 쓰는 방식이 있지만, 이 방식은 너무 복잡하고, 잘 사용하지 않기에 다루지 않는다.

쉽게 사용할 수 있도록 나온 `fetch API` 를 주로 사용한다.

리액트는 axios라는 라이브러리를 사용한다.

## `fetch()` 를 통해 API 요청해보기

- `fetch(url, [options])`
    - `url(필수)` : 접근하고자 하는 url
    - `option(선택)` : method, header 등을 지정할 수 있음(아무것도 안하면 자동 GET)

`fetch()` 를 호출하면 브라우저는 네트워크 요청을 보내고 프라미스가 반환된다.

네트워크 문제나 존재하지 않는 사이트에 접속하려는 경우같이 HTTP 요청을 보낼 수 없는 상태에선 Promise가 거부된다.

```jsx
let response = await fetch(url);

if (response.ok) { // HTTP 상태 코드가 200~299일 경우
  // 응답 본문을 받습니다
  let json = await response.json();
} else {
  alert("HTTP-Error: " + response.status);
}
```

- HTTP 상태는 응답 프로퍼티를 사용해 확인할 수 있다.
    - `status` : HTTP 상태 코드(예, 200, 400…)
    - `ok` : boolean값(status가 200 ~ 299 사이면 true)

위 코드에서 response에는 promise가 반환된다. 이 promise를 기반으로 하는 다양한 메서드가 있는데 자주 쓰는 것만 알아보자.

- `response.text()` : 응답을 읽고 텍스트를 반환
- `response.json()` : 응답을 JSON 형태로 파싱
- `response.formData()` : 응답을 FormData 객체 형태로 반환

직접 fetch를 사용해보자. 그냥 fetch()를 사용했을 때 promise 값이 어떻게 반환되는지 보자.

```jsx
const response = fetch("https://jsonplaceholder.typicode.com/posts");

console.log(response);
```

이번엔 json 형태로 출력해보자.

```jsx
// 1. fetch 함수를 사용하여 API를 호출합니다.
fetch("https://jsonplaceholder.typicode.com/posts")
  // 2. 응답을 JSON 형태로 변환합니다.
  .then((response) => response.json())
  // 3. JSON 형태로 변환된 응답을 콘솔에 출력합니다.
  .then((json) => console.log(json));
```

여기서 주의할 점은, 본문을 읽을 때 사용되는 response 메서드는 딱 하나만 사용할 수 있다는 점이다. 만약, `response.json()` 으로 처리했다면 `response.text()` 는 동작하지 않는다.

이번엔 `fetch()` 에서 사용할 수 있는 요청 옵션들을 살펴보자.

- `method` : HTTP method 중에 하나를 선택
- `body` : 서버가 필요한 데이터를 담아 보내주는 것으로, 요청에 추가하고자하는 본문
- `headers` : API 요청에 추가하고자 하는 헤더들
- `mode` : 요청에 사용할 모드
- `credentials` : 브라우저가 쿠키, HTTP 인증 항목 등 자격 증명을 어떻게 취급할지 제어
    - `omit` : 브라우저가 요청에서 자격증명을 제외하도록 & 응답에 포함된 자격증명도 무시하도록
    - `same-origin` : 기본값, 브라우저가 동일 출처 URL 요청에 대해서는 자격증명을 보내고, 동일 출처 URL 응답에 포함된 자격증명도 사용하도록 지시
    - `include` : 브라우저 동일과 교차 출처 요청 모두에 자격증명을 보내고, 응답 자격증명도 모두 사용하도록 지시
- `cache` : 요청이 브라우저 HTTP 캐시와 어떻게 상호작용할지 제어(자세한 내용: https://developer.mozilla.org/ko/docs/Web/API/Request/cache)
- `redirect` : 리다이렉트 응답 처리법
    - `follow` : 기본값, 자동으로 리다이렉트 따라감
    - `error` : 리다이렉트 발생 시 오류와 함께 요청 중단
    - `manual` : 호출자가 응답을 다른 컨텍스트에서 처리해야 함

## 위 전체 내용 복습 예시 코드

```jsx
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => {
    // 200 ~ 299 사이 결과라면 ok 속성은 true
    // 만약 400, 500 에러가 뜨면 catch로 넘어감
    if (!response.ok) {
      throw new Error("HTTP 에러임, status = " + response.status);
    }
    return response.json();
  })
  .then((json) => console.log(json))
  // 400, 500 처럼 HTTP 에러가 뜨면 자동으로 catch로 안오기 때문에 위처럼 조건문 처리 해줘야함
  .catch((err) => console.log(err));
  
 //POST 요청
 fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    body: JSON.stringify({
      title: "foo",
      body: "bar",
      userId: 1,
    }),
    headers: {
      "Content-type": "application/json; charset=UTF-8", // headers로 JSON 포맷을 사용한다고 알려줘야함
    },
  })
    .then((response) => {
      // post 요청은 201 Created 라는 응답을 받게 될 것
      // 200 ~ 299 사이 결과라면 ok 속성은 true
      // 만약 400, 500 에러가 뜨면 catch로 넘어갈
      if (!response.ok) {
        throw new Error("HTTP 에러임, status = " + response.status);
      }
      return response.json();
    })
    .then((json) => console.log(json))
    // 400, 500 처럼 HTTP 에러가 뜨면 자동으로 catch 로 안 오기 때문
    .catch((err) => console.log(err));
    
	//PUT 요청
  fetch("https://jsonplaceholder.typicode.com/posts/1", {
    method: "PUT",
    body: JSON.stringify({
      id: 1,
      title: "foo",
      body: "bar",
      userId: 1,
    }),
    headers: {
      "Content-type": "application/json; charset=UTF-8",
    },
  })
    .then((response) => {
      if (!response.ok) {
        throw new Error("HTTP 에러임, status = " + response.status);
      }
      return response.json();
    })
    .then((json) => console.log(json))
    .catch((err) => console.log(err));
  
```

## HTTP Request 메서드(의미만 대충)

- `GET` : 서버 자원을 조회하는 것 → 보낼 데이터가 없으니 옵션 인자가 필요 없음
- `POST` : 서버에 새로운 자원을 추가하는 것 → 보내줄 데이터를 body 에 넣어 보냅니다.
- `PUT` : 서버 자원을 통째로 교체하는 것 → 보내줄 데이터를 body 에 넣어 보냅니다.
- `PATCH` : 서버 자원을 일부만 교체하는 것
- `DELETE` : 서버 자원을 제거하는 것 → 보낼 데이터가 없으니 header, body 옵션 필요 X
- `HEAD` : 서버 자원에 대한 HTTP 헤더만 확인하는 메서드
- `OPTIONS` : 보통 CORS 때 많이 활용을 하는데 해당 자원에 대해 어떤 메서드들을 지원하는지 알아내기 위함
- `PUT` vs `PATCH`
    
    ```jsx
    const obj = {name: "mandoo", age: 2}
    
    // PUT {age: 20} 를 하면 
    obj = {age: 20} // 통째로 바뀜
    
    // PATCH {age: 25} 를 하면
    obj = {name: "mandoo", age: 25} // age 만 바뀜
    ```
    

## `Map`, `Set`이란

지금까지 객체, 배열과 같이 복잡한 자료구조를 배워왔다. 하지만 이 두 개로도 부족한 상황이 발생하여 `Map`과 `Set`이란 것들이 존재한다.

- `Map(맵)`
    
    키가 있는 데이터를 저장한다는 점에서 객체와 굉장히 유사하다. 하지만 맵은 키-값 쌍과 키의 원래 삽입 순서를 기억하고, 키에 다양한 자료형을 허용한다.
    
    Map에서 사용되는 주요 메서드와 프로퍼티를 살펴보자.
    
    - `new Map()` : 맵을 만듦
    - `map.set(key, value)` : `key`를 이용해 `value`를 저장
    - `map.get(key)` : `key` 에 해당하는 값을 반환. `key` 가 존재하지 않으면 `undefined` 반환
    - `map.has(key)` : `key` 가 존재하면 `true`, 존재하지 않으면 false를 반환
    - `map.delete(key)` : `key`에 해당하는 값을 삭제
    - `map.clear()` : 맵 안의 모든 요소 제거
    - `map.size` : 요소의 개수를 반환
    
    예시 코드를 보자.
    
    ```jsx
    // ex1
    const map1 = new Map();
    
    map1.set("a", 1);
    map1.set("b", 2);
    map1.set("c", 3);
    
    console.log(map1.get("a"));
    // Expected output: 1
    
    map1.set("a", 97);
    
    console.log(map1.get("a"));
    // Expected output: 97
    
    console.log(map1.size);
    // Expected output: 3
    
    map1.delete("b");
    
    console.log(map1.size);
    // Expected output: 2
    
    ```
    
    객체처럼 사용하면 안된다. 사용법과 생김새는 유사하지만 올바르게 작동하지 않는다.
    
    ```jsx
    // ❌ wrong
    const wrongMap = new Map();
    wrongMap["bla"] = "blaa";
    wrongMap["bla2"] = "blaaa2";
    
    console.log(wrongMap); // Map(0) {bla: 'blaa', bla2: 'blaaa2', size: 0}
    console.log(wrongMap.get("bla")); // undefined
    
    // ✅ good
    const correctMap = new Map();
    correctMap.set("bla", "blaa")
    correctMap.set("bla2", "blaaa2")
    
    console.log(correctMap); // Map(2) {'bla' => 'blaa', 'bla2' => 'blaaa2'}
    console.log(correctMap.get("bla")); // blaa
    
    // ✅ good 2 : 맵에 데이터를 저장하는 올바른 방법
    const contacts = new Map();
    contacts.set("Jessie", { phone: "213-555-1234", address: "123 N 1st Ave" });
    contacts.has("Jessie"); // true
    contacts.get("Hilary"); // undefined
    contacts.set("Hilary", { phone: "617-555-4321", address: "321 S 2nd St" });
    contacts.get("Jessie"); // {phone: "213-555-1234", address: "123 N 1st Ave"}
    contacts.delete("Raymond"); // false
    contacts.delete("Jessie"); // true
    console.log(contacts.size); // 1
    ```
    
    키 값에서도 객체와의 차이점을 가진다는 것도 알아야 한다. 예시 코드를 보자.
    
    ```jsx
    const myMap = new Map();
    
    const keyString = "a string";
    const keyObj = {};
    const keyFunc = function () {};
    
    // 값 설정
    myMap.set(keyString, "value associated with 'a string'");
    myMap.set(keyObj, "value associated with keyObj");
    myMap.set(keyFunc, "value associated with keyFunc");
    
    console.log(myMap.size); // 3
    
    // 값 불러오기
    console.log(myMap.get(keyString)); // "value associated with 'a string'"
    console.log(myMap.get(keyObj)); // "value associated with keyObj"
    console.log(myMap.get(keyFunc)); // "value associated with keyFunc"
    ```
    
    `Map`의 요소 반복 작업하는 법
    
    - `map.keys()` : 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환
    - `map.values()` : 각 요소의 값을 모든 이터러블 객체 반환
    - `map.entries()` : 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체 반환.
    
    위에서 이터러블 객체는 for…of 반복문의 기초로 쓰인다. 예시 코드를 보자.
    
    ```jsx
    let recipeMap = new Map([
      ['cucumber', 500],
      ['tomatoes', 350],
      ['onion',    50]
    ]);
    
    let recipeMap = new Map([
      ['cucumber', 500],
      ['tomatoes', 350],
      ['onion',    50]
    ]);
    
    console.log(recipeMap.keys())
    // 키(vegetable)를 대상으로 순회합니다.
    for (let vegetable of recipeMap.keys()) {
      console.log(vegetable); // cucumber, tomatoes, onion
    }
    
    console.log(recipeMap.values())
    // 값(amount)을 대상으로 순회합니다.
    for (let amount of recipeMap.values()) {
      console.log(amount); // 500, 350, 50
    }
    
    // [키, 값] 쌍을 대상으로 순회합니다.
    for (let entry of recipeMap) { 
      console.log(entry); // cucumber,500 ...
    }
    
    // forEach 도 지원함, 각 (키, 값) 쌍을 대상으로 함수를 실행
    recipeMap.forEach( (value, key, map) => {
      console.log(`${key}: ${value}`); // cucumber: 500 ...
    });
    
    ```
    
- `Set(셋)`
    
    Set 객체는고유 값을 저장할 때 사용할 수 있다. 즉, `Set` 은 중복을 허용하지 않는 값을 모은 특별한 컬렉션이다.
    
    `Set`에 `key`가 없는 값이 저장된다.
    
    Set에서 사용되는 주요 메서드를 알아보자.
    
    - `new Set(iterable)` : 셋을 만듦. 이터러블 객체를 전달받으면(대부분 배열) 그 안의 값을 복사해 셋에 넣음
    - `set.add(value)` : 값을 추가하고 셋 자신을 반환
    - `set.delete(value)` : 값을 제거. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 `true`, 아니면 `false`를 반환
    - `set.has(value)` : 셋 내에 값이 존재하면 `true`, 아니면 `false` 반환
    - `set.clear()` : 셋을 비움
    - `set.size` : 셋에 몇 개의 값이 있는지 세줌
    
    예시 코드를 보자
    
    ```jsx
    let set = new Set();
    
    let john = { name: "John" };
    let pete = { name: "Pete" };
    let mary = { name: "Mary" };
    
    // 어떤 고객(john, mary)은 여러 번 방문
    set.add(john);
    set.add(pete);
    set.add(mary);
    set.add(john);
    set.add(mary);
    
    // 셋에는 유일무이한 값만 저장
    console.log( set.size ); // 3
    
    for (let user of set) {
      console.log(user.name); // // John, Pete, Mary 순으로 출력
    }
    ```
    
    Set에서 반복작업을 위한 메서드를 알아보자.
    
    - `set.keys()` : 셋 내의 모든 값을 포함하는 이터러블 객체를 반환
    - `set.values()` : `set.keys`와 동일한 작업함. `맵`과의 호환성을 위해 만들어진 메서드.
    - `set.entries()` – 셋 내의 각 값을 이용해 만든 `[value, value]` 배열을 포함하는 이터러블 객체를 반환.  이는 Map 과의 호환성을 위해 만들어짐
    
    `Set`에서는 개발자들이 흔히 아는 `forEach`와 조금 다르다.
    
    `forEach` 에 쓰인 콜백 함수는 세 개의 인수를 받는데, 첫 번째는 값, 두 번째도 같은 값인 `valueAgain`을 받고 있다. 세 번째는 목표하는 객체(Set)이고.
    
    즉 동일한 값이 인수에 두 번 등장하고 있다. 이렇게 구현된 이유는 맵과의 호환성 때문이다. 맵의 `forEach`에 쓰인 콜백이 세 개의 인수를 받을 때를 위해서이다. 덕분에 맵을 셋으로, 셋을 맵으로 교체하기 쉽다.