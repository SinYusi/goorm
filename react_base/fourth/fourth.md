## Context Hooks

`Context` 는 컴포넌트가 props를 전달하지 않고도 멀리 있는 부모 컴포넌트로부터 정보를 받을 수 있게 해준다.

- `useContext`
    
    `useContext` 는 컴포넌트에서 이러한 `Context` 를 읽고 구독할 수 있는 hook이다.
    
    - 기본 사용 문법
        
        ```jsx
        const value = useContext(SomeContext)
        ```
        
        - `SomeContext` : `createContext` 로 생성한 `Context` 이다. `Context` 자체는 정보를 담고 있지 않으며, 컴포넌트에서 제공하거나 읽을 수 있는 정보의 종류를 나타낸다.
            
            여기서 `createContext` 가 무엇인지 빠르게 짚고 가보자.
            
            아래와 같이 기본 값을 넣어서 `Context` 를 만들어주는 함수다.
            
            ```jsx
            const SomeContext = createContext(defaultValue)
            ```
            
            이걸 사용할 때에는 아래와 같이 사용한다.
            
            아래 코드에서 `ThemeContext.Provider` 는 컴포넌트를 Context 제공자로 감싸서 이 `Context` 의 값을 모든 내부 컴포넌트에 지정한다.
            
            ```jsx
            import { createContext } from 'react';
            
            const ThemeContext = createContext('light');
            
            function App() {
              const [theme, setTheme] = useState('light');
              // ...
              return (
            	  // 여기서 value는 이 제공자 내부의 컨텍스트를 읽는 모든 컴포넌트에 전달하려는 값
                <ThemeContext.Provider value={theme}>
                  <Page />
                  <Button>
                </ThemeContext.Provider>
              );
            }
            ```
            
            그럼 이제 자식 컴포넌트에서 `useContext` 로 `value` 로 받아와서 사용이 가능하다.
            
            ```jsx
            function Button() {
              const theme = useContext(ThemeContext);
              return <button className={theme} />;
            }
            ```
            
    
    그럼 `useContext` 를 활용한 예제들을 보며 익혀보자.
    
    1. 다크모드 예제: https://codesandbox.io/p/sandbox/f2vfvn?file=%2Fsrc%2FApp.js
        
        이 예시에서 `MyApp` 컴포넌트는 `State` 변수를 가지고 있고, 이 `State` 변수는 `ThemeContext Provider` 로 전달된다.
        
        “Use dark mode” 체크박스를 체크하면 `State` 가 업데이트되고, 제공된 값을 변경하면 해당 `Context` 를 사용하는 모든 컴포넌트가 다시 렌더링된다.
        
    2. 객체 업데이트: https://codesandbox.io/p/sandbox/splzmh?file=%2Fsrc%2FApp.js
        
        이 예시에서는 객체를 가지고 있는 `currentUser` State 변수가 있다.
        
        `{ currentUser, setCurrentUser }` 를 하나의 객체로 결합하여 `value={}` 내부의 Context를 통해 전달하고 있다.
        
        이렇게 하면 `LoginButton` 과 같은 하위의 모든 컴포넌트가 `currentUser` 와 `setCurrentUser` 를 모두 읽은 다음 필요할 때 `setCurrentUser` 를 호출할 수 있다.
        
    3. 여러 개 Context 사용 가능: https://codesandbox.io/p/sandbox/xpwp5d?file=%2Fsrc%2FApp.js
        
        이 예시에서는 두 개의 독립적인 Context가 있다.
        
        `ThemeContext` 는 현재 테마를 문자열로 제공하고, `CurrentUserContext` 는 현재 사용자를 나타내는 객체를 보유하고 있다.
        

## Ref Hooks

`Ref` 를 사용하면 컴포넌트가 DOM 노드나 Timer ID같이 렌더링에 사용되지 않는 일부 정보를 보유할 수 있다.

state와 달리, `Ref` 는 업데이트를 해도 컴포넌트가 다시 렌더링되지 않는다.

그래서 이런 `Ref` 는 내장된 브라우저 API와 같이, React가 아닌 시스템으로 작업해야할 때 유용하다.

- `useRef` : 렌더링에 필요하지 않은 값을 참조할 수 있는 React Hook
    
    ```jsx
    const ref = useRef(initialValue)
    ```
    
    - `initialValue` : `ref` 객체의 `current` 프로퍼티 초기 설정값이다. 여기에는 어떤 유형의 값이든 지정할 수 이싿. 이 인자는 초기 렌더링 이후부터는 무시된다.
    
    - `useRef`는 어떤 값을 반환할까?
        
        `useRef` 는 단일 프로퍼티를 가진 객체를 반환한다.
        
        그 단일 프로퍼티는 바로 `current` 이다.
        
        - `current` : 처음에는 전달한 `initialValue` 로 설정된다. 후에 다른 값으로 바꿀 수 있다. ref 객체를 JSX 노드의 `ref` 어트리뷰트로 React에 전달하면 React는 `current` 프로퍼티를 설정한다.
    - 실제 사용 예시
        
        ```jsx
        import { useRef } from "react";
        
        // 이 컴포넌트는 ref를 사용하여 버튼이 클릭된 횟수를 추적합니다. 
        // 이때 클릭 횟수는 이벤트 핸들러에서만 읽고 쓰기 때문에 
        // 여기서는 state 대신 ref를 사용해도 괜찮습니다.
        export default function Counter() {
          let ref = useRef(0);
        
          function handleClick() {
            ref.current = ref.current + 1;
            alert("You clicked " + ref.current + " times!");
          }
        
          return <button onClick={handleClick}>Click me!</button>;
        }
        ```
        
    - 또 다른 사용 예시
        
        아래 예시는 state와 ref의 조합인데, `startTime` 과 `now` 는 모두 렌더링에 사용되기 때문에 state 변수다.
        
        그러나 버튼을 누를 때 `interval` 을 멈출 수 있게 하기 위해 `interval ID` 도 기억하고 있어야 한다.
        
        이 때 `interval ID` 는 렌더링에 사용되지 않으므로 `ref` 에 보관하고 수동으로 업데이트하는 것이 적절한다.
        
        ```jsx
        import { useState, useRef } from 'react';
        
        export default function Stopwatch() {
          const [startTime, setStartTime] = useState(null);
          const [now, setNow] = useState(null);
          const intervalRef = useRef(null);
        
          function handleStart() {
            setStartTime(Date.now());
            setNow(Date.now());
        
            clearInterval(intervalRef.current);
            intervalRef.current = setInterval(() => {
              setNow(Date.now());
            }, 10);
          }
        
          function handleStop() {
            clearInterval(intervalRef.current);
          }
        
          let secondsPassed = 0;
          if (startTime != null && now != null) {
            secondsPassed = (now - startTime) / 1000;
          }
        
          return (
            <>
              <h1>Time passed: {secondsPassed.toFixed(3)}</h1>
              <button onClick={handleStart}>
                Start
              </button>
              <button onClick={handleStop}>
                Stop
              </button>
            </>
          );
        }
        ```
        
    
    `useRef` 를 사용할 때 주의할 점은 `ref.current` 를 렌더링 중에 절대 읽거나 쓰면 안된다는 것이다.
    
    ```jsx
    function MyComponent() {
      // ...
      // ❌ 렌더링 중에는 절대 쓰지 말기
      myRef.current = 123;
      // ...
      // ❌ 렌더링 중에는 절대 읽지 말기
      return <h1>{myOtherRef.current}</h1>;
    }
    ```
    
    대신 이벤트 핸들러나 Effect에서 ref를 읽거나 쓰면 된다.
    
    ```jsx
    function MyComponent() {
      // ...
      useEffect(() => {
        // ✅ Effect 안에서 읽고 쓰는 건 가능
        myRef.current = 123;
      });
      // ...
      function handleClick() {
        // ✅ 이벤트 핸들러(함수) 안에서 읽고 쓰는 건 가능
        doSomething(myOtherRef.current);
      }
      // ...
    }
    ```
    
    ref로 DOM 조작도 가능하다. 아래 예시와 같이 버튼을 클릭하면 `input` 에 `focus` 된다.
    
    ```jsx
    import { useRef } from 'react';
    
    export default function Form() {
      const inputRef = useRef(null);
    
      function handleClick() {
        inputRef.current.focus();
      }
    
      return (
        <>
          <input ref={inputRef} />
          <button onClick={handleClick}>
            Focus the input
          </button>
        </>
      );
    }
    ```
    

## Effect Hooks

`Effect` 를 통해 컴포넌트 외부 시스템에 연결하고 동기화할 수 있다.

여기에는 네트워크, 브라우저 DOM, 애니메이션, 다른 UI 라이브러리를 사용하여 작성된 위젯, 또는 기타 React가 아닌 코드를 다루는 것이 포함된다.

여기서 외부 시스템이라는 것이 무엇인지 궁금할 수 이싿.

외부 시스템이란 React에 의해 컨트롤되지 않는 모든 코드를 의미한다.

예를 들어 `setInterval()` 에 의해 관리되는 타이머, `window.addEventListener()` 를 이용한 이벤트 등등이 있다.

- `useEffect`: 컴포넌트를 외부 시스템에 연결하고 동기화하는 hook
    
    ```jsx
    useEffect(setup, dependencies?)
    ```
    
    - `setup(설정)` : Effect의 로직이 포함된 함수
        
        설정 함수는 선택적으로 clean up(정리) 함수를 반환할 수 있다.
        
        React는 컴포넌트가 DOM에 추가된 이후에 설정 함수를 실행한다.
        
        의존성의 변화에 따라 컴포넌트가 리렌더링이 되었을 경우(설정 함수에 정리 함수를 추가 했다면) React는 이전 렌더링에 사용된 값으로 정리 함수를 실행한 후 새로운 값으로 설정함수를 실행한다.
        
        컴포넌트가 DOM에서 제거된 경우에도 정리 함수를 실행한다.
        
    - `dependencies(의존성 배열)` (선택 사항) : 설정 함수의 코드 내부에서 참조되는 모든 반응형 값들이 포함된 배열로 구성
        
        `[dep1, dep2, dep3]` 과 같이 작성되어야 한다.
        
        의존성을 생략할 경우, Effect는 컴포넌트가 리렌더링될 때마다 실행된다.
        
    - `useEffect` 를 사용하는 예제
        
        아래 예시에서는 DOM 자체를 외부 시스템으로 사용한다.
        
        일반적으로 JSX와 함께 이벤트 리스너를 명시하지만 이 예시에서 외부 시스템은 브라우저 DOM 자체다.
        
        일반적으로 JSX를 이용해 이벤트 리스너를 지정하지만 이 방식만으로는 전역 window 객체를 감시할 수 없으니 Effect를 이용해 React를 window 객체와 연결해서 이벤트를 감시할 수 있다.
        
        `pointermove` 이벤트를 감시할 경우, 커서의 위치를 추적하고 빨간 점을 해당 위치로 이동시킬 수 있다.
        
        ```jsx
        import { useState, useEffect } from 'react';
        
        export default function App() {
          const [position, setPosition] = useState({ x: 0, y: 0 });
        
          useEffect(() => {
            function handleMove(e) {
              setPosition({ x: e.clientX, y: e.clientY });
            }
            window.addEventListener('pointermove', handleMove);
            return () => {
              window.removeEventListener('pointermove', handleMove);
            };
          }, []);
        
          return (
            <div style={{
              position: 'absolute',
              backgroundColor: 'pink',
              borderRadius: '50%',
              opacity: 0.6,
              transform: `translate(${position.x}px, ${position.y}px)`,
              pointerEvents: 'none',
              left: -20,
              top: -20,
              width: 40,
              height: 40,
            }} />
          );
        }
        ```
        
    
    의존성 배열 `dependencies` 는 없을 수도, 빈 배열일 수도, 값이 있을 수도 있다.
    
    1. 의존성 배열을 전달하는 경우
        
        의존성을 명시하면 Effect는 초기 렌더링 후 그리고 의존성 값 변겨오가 함께 리렌더링이 된 후 동작한다.
        
        ```jsx
        useEffect(() => {
          // ...
        }, [a, b]); // a나 b가 다르면 다시 실행됨
        ```
        
        ```jsx
        // 동작 과정을 이해하기 위한 예시
        import { useEffect, useState } from "react";
        
        export default function App() {
          const [count, setCount] = useState(0);
        
          useEffect(() => {
            if (count !== 0) alert(`count가 ${count}로 변경되었습니다.`);
          }, [count]);
        
          return (
            <div>
              <h3>count : {count}</h3>
              <button onClick={() => setCount(count + 1)}>+</button>
            </div>
          );
        }
        ```
        
    2. 빈 의존성 배열을 전달하는 경우
        
        이 때는 초기 렌더링 이후 한 번만 실행된다.
        
        ```jsx
        useEffect(() => {
          // ...
        }, []); // 다시 실행되지 않음 (개발 환경에서만 엄격모드로 한번 더 실행됨)
        ```
        
        ```jsx
        import { useEffect, useState } from "react";
        
        export default function App() {
          const [count, setCount] = useState(0);
        
          useEffect(() => {
            alert("hi");
          }, []);
        
          return (
            <div>
              <h3>count : {count}</h3>
              <button onClick={() => setCount(count + 1)}>+</button>
            </div>
          );
        }
        ```
        
    3. 의존성 배열을 전달하지 않은 경우
        
        이 때에는 컴포넌트의 모든 렌더링과 리렌더링마다 동작한다.
        
        ```jsx
        useEffect(() => {
          // ...
        }); // 항상 다시 실행됨
        ```
        
        ```jsx
        import { useEffect, useState } from "react";
        
        export default function App() {
          const [count, setCount] = useState(0);
        
          useEffect(() => {
            alert("hi");
          });
        
          return (
            <div>
              <h3>count : {count}</h3>
              <button onClick={() => setCount(count + 1)}>+</button>
            </div>
          );
        }
        ```
        

## Performance Hooks

재렌더링 성능을 최적화하는 일반적인 방법은 불필요한 작업을 건너뛰는 것이다.

예를 들어, 이전 렌더링 이후 데이터가 변경되지 않은 경우 캐시된 계산을 재사용하거나 재렌더링을 건너뛰도록 React에 지시할 수 있다.

계산과 불필요한 재렌더링을 건너뛰려면 `useMemo`나 `useCallback` 를 사용하면 된다.

- `useMemo` : 비용이 많이 드는 계산 결과를 캐시 가능
    
    ```jsx
    const cachedValue = useMemo(calculateValue, dependencies)
    ```
    
    - `calculateValue` : 캐싱하려는 값을 계산하는 함수
        
        순수해야 하며 인자를 받지 않고, 모든 타입의 값을 반환할 수 있어야 한다.
        
        React는 초기 렌더링 중에 함수를 호출한다.
        
        다음 렌더링에서, React는 마지막 렌더링 이후 `dependencies` 가 변경되지 않았을 때 동일한 값을 다시 반환한다.
        
        그렇지 않다면 `calculateValue` 를 호출하고 결과를 반환하며, 나중에 재사용할 수 있도록 저장한다.
        
    - `dependencies` : `calculateValue` 코드 내에서 참조된 모든 반응형 값들의 목록
        
        `[dep1, dep2, dep3]` 와 같이 인라인 형태로 작성해야 한다.
        
    
    - 사용 예시
        
        우선 메모이제이션을 사용하지 않고 `location` 변수를 할당하는 코드를 먼저 살펴보자.
        
        ```jsx
        import { useMemo, useEffect, useState } from "react";
        
        function App() {
          const [number, setNumber] = useState(0);
          const [isKorea, setIsKorea] = useState(true);
        
          const location = { country: isKorea ? "한국" : "일본" };
        
          useEffect(() => {
            console.log("useEffect... 호출");
            // 뭔가 오래 걸리는 작업
          }, [location]);
        
          return (
            <header className="App-header">
              <h2>하루에 몇 끼 먹어요?</h2>
              <input
                type="number"
                value={number}
                onChange={(e) => setNumber(e.target.value)}
              />
              <hr />
        
              <h2>어느 나라에 있어요?</h2>
              <p>나라: {location.country}</p>
              <button onClick={() => setIsKorea(!isKorea)}>Update</button>
            </header>
          );
        }
        
        export default App;
        ```
        
        위 코드를 실행시켜보면 진짜 `location`을 바꾸는 `update` 버튼이 아닌, `input` 을 수정할 때에도 `location` 이 변경됐다고 생각하여 `useEffect` 가 실행되는 것을 볼 수 있다.
        
        이건 자바스크립트에서 객체는 값이 저장될 때 “주소 값”이 저장되는 것을 생각했을 때, 개발자 눈에는 `const location = { country: isKorea ? "한국" : "일본" };` 로 똑같아 보이지만, 실상 `number` 가 바뀔 때마다 `location` 에 저장되는 객체의 메모리 주소가 달라진다.
        
        그렇기에 `useEffect` 는 `location` 이 변경되었다고 생각하는 것이다.
        
        따라서 이 문제를 `useMemo` 로 해결할 수 있다.
        
        `isKorea` 값이 변경되었을 경우에만 `location` 객체를 다시 만들어주도록 해보자.
        
        ```jsx
        import { useMemo, useEffect, useState } from "react";
        
        function App() {
          const [number, setNumber] = useState(0);
          const [isKorea, setIsKorea] = useState(true);
        
          // const location = { country: isKorea ? "한국" : "일본" };
          const location = useMemo(() => {
            return {
              country: isKorea ? "한국" : "일본",
            };
          }, [isKorea]);
        
          useEffect(() => {
            console.log("useEffect... 호출");
            // 뭔가 오래 걸리는 작업
          }, [location]);
        
          return (
            <header className="App-header">
              <h2>하루에 몇 끼 먹어요?</h2>
              <input
                type="number"
                value={number}
                onChange={(e) => setNumber(e.target.value)}
              />
              <hr />
        
              <h2>어느 나라에 있어요?</h2>
              <p>나라: {location.country}</p>
              <button onClick={() => setIsKorea(!isKorea)}>Update</button>
            </header>
          );
        }
        
        export default App;
        ```
        
- `useCallback` : 리렌더링 간에 함수 정의를 캐싱해주는 React Hook
    
    ```jsx
    const cachedFn = useCallback(fn, dependencies)
    ```
    
    - `fn` : 캐싱할 함숫값
        
        이 함수는 어떤 인자나 반환값도 가질 수 있다.
        
        React는 첫 렌더링에서 이 함수를 반환한다. (호출하는 것이 아님)
        
        다음 렌더링에서 `dependencies` 값이 이전과 같다면 React는 같은 함수를 다시 반환한다.
        
        반대로 `dependencies` 값이 변경되었다면 이번 렌더링에서 전달한 함수를 반환하고 나중에 재사용할 수 있도록 이를 저장한다.
        
    - `dependencies` : `fn` 내에서 참조되는 모든 반응형 값의 목록
    
    `useCallback` 의 반환값은 전달한 `fn` 함수를 반환한다.
    
    - 사용 예시
        
        ```jsx
        import { useCallback } from 'react';
        
        function ProductPage({ productId, referrer, theme }) {
        
          const handleSubmit = useCallback((orderDetails) => {
            post('/product/' + productId + '/buy', {
              referrer,
              orderDetails,
            });
          }, [productId, referrer]);
          
          // ...
          
           return (
            <div className={theme}>
              <ShippingForm onSubmit={handleSubmit} />
            </div>
          );
        }
        ```
        
        만약 위 코드에서 `useCallback` 을 사용하지 않았다면, `handleSubmit` 은 `props` 가 바뀔 때마다 새롭게 함수가 정의될 것이다.
        
        그래서 이 때 `[productId, referrer]` 이 의존성 배열인 `useCallback` 으로 함수를 감싸주면, 위 의존성 배열에 들어간 데이터가 변경되지 않는 한 함수는 캐싱된다.
        

`useMemo`와 `useCallback` 은 반드시 성능 최적화 용도로만 사용해야 한다.

만약 이 두 가지 훅 없이 코드가 올바르게 동작하지 않는다면 근본적인 문제를 찾아 해결해야 한다.