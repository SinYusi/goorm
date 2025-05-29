## 배열 State 업데이트하는 방법

이번엔 객체가 아닌 배열을 업데이트해보자.

마찬가지로 배열을 직접 변경하는 것이 아닌 새 배열을 반환하는 방식으로 업데이트해야 한다.

|  | 비선호 (배열을 변경) | **선호 (새 배열을 반환)** |
| --- | --- | --- |
| 추가 | `push`, `unshift` | `concat`, `[...arr]` 전개 연산자 |
| 제거 | `pop`, `shift`, `splice` | `filter`, `slice` |
| 교체 | `splice`, `arr[i] = ...` 할당 | `map` |
| 정렬 | `reverse`, `sort` | 배열을 복사한 이후 처리 |

배열에 항목을 추가한다고 했을 때 `push()` 를 사용해보면 원하는대로 동작하지 않을 것이다.

```jsx
import { useState } from 'react';

let nextId = 0;

export default function List() {
  const [name, setName] = useState('');
  const [artists, setArtists] = useState([]);

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <input
        value={name}
        onChange={e => setName(e.target.value)}
      />
      <button onClick={() => {
        artists.push({
          id: nextId++,
          name: name,
        });
      }}>Add</button>
      <ul>
        {artists.map(artist => (
          <li key={artist.id}>{artist.name}</li>
        ))}
      </ul>
    </>
  );
}
```

이렇게 기존 배열을 변경하는 것이 아닌 spread 연산자를 통해 새로운 배열을 만들어야 한다.

```jsx
import { useState } from "react";

let nextId = 0;

export default function List() {
  const [name, setName] = useState("");
  const [artists, setArtists] = useState([]);

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button
        onClick={() => {
          setArtists([...artists, { id: nextId++, name: name }]);
        }}
      >
        Add
      </button>
      <ul>
        {artists.map((artist) => (
          <li key={artist.id}>{artist.name}</li>
        ))}
      </ul>
    </>
  );
}
```

이번엔 배열에서 특정 항목을 제거해보자. 이 때 `filter()` 을 사용해볼 것이다.

```jsx
import { useState } from "react";

let nextId = 0;

export default function List() {
  const [name, setName] = useState("");
  const [artists, setArtists] = useState([]);

  const handleDeleteClicked = (id) => {
    const filterArtists = artists.filter((a) => a.id !== id);
    setArtists(filterArtists);
  };

  return (
    <>
      <h1>Inspiring sculptors:</h1>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button
        onClick={() => {
          setArtists([...artists, { id: nextId++, name: name }]);
        }}
      >
        Add
      </button>
      <ul>
        {artists.map((artist) => (
          <>
            <li key={artist.id}>{artist.name}</li>
            <button onClick={() => handleDeleteClicked(artist.id)}>
              Delete
            </button>
          </>
        ))}
      </ul>
    </>
  );
}
```

이번엔 독립적으로 동작하는 카운터를 구현해보자.

아래 배열을 사용해서 각 요소별로 카운터가 + 1 증가하도록 구현해보자.

```jsx
let initialCounters = [0, 0, 0];
```

완성해보면 아래와 같은 코드가 될 것이다.

```jsx
import { useState } from "react";

let initialCounters = [0, 0, 0];

export default function CounterList() {
  const [counters, setCounters] = useState(initialCounters);

  function handleIncrementClick(index) {
    const nextCounters = counters.map((c, i) => {
      if (i === index) return c + 1;
      else return c;
    });
    setCounters(nextCounters);
  }

  return (
    <ul>
      {counters.map((counter, index) => (
        <li key={index}>
          {counter}
          <button
            onClick={() => {
              handleIncrementClick(index);
            }}
          >
            +1
          </button>
        </li>
      ))}
    </ul>
  );
}
```

이번엔 배열을 뒤집어보자. `reverse()` 를 사용할 때에는 배열을 복사해서 사용해야 한다.

```jsx
import { useState } from 'react';

const initialList = [
  { id: 0, title: 'Big Bellies' },
  { id: 1, title: 'Lunar Landscape' },
  { id: 2, title: 'Terracotta Army' },
];

export default function List() {
  const [list, setList] = useState(initialList);

  function handleClick() {
    const nextList = [...list];
    nextList.reverse();
    setList(nextList);
  }

  return (
    <>
      <button onClick={handleClick}>
        Reverse
      </button>
      <ul>
        {list.map(artwork => (
          <li key={artwork.id}>{artwork.title}</li>
        ))}
      </ul>
    </>
  );
}
```

## State로 Input 다루기

Form을 선언적인 방식으로 구현하기 위해 첫 번째로, 컴포넌트의 다양한 시각적 state를 확인해야 한다.

Form이 가지고 있는 여러가지 state

- **Empty**: 폼은 비활성화된 “제출” 버튼을 가지고 있다.
- **Typing**: 폼은 활성화된 “제출” 버튼을 가지고 있다.
- **Submitting**: 폼은 완전히 비활성화되고 스피너가 보인다.
- **Success**: 폼 대신에 “감사합니다” 메시지가 보인다.
- **Error**: “Typing” state와 동일하지만 오류 메시지가 보인다.

```jsx
import { useState } from "react";

export default function Form() {
  const [status, setStatus] = useState("success");
  // status: empty, submitting, error, success

  if (status === "success") {
    return <h1>That's right!</h1>;
  }
  return (
    <>
      <h2>City quiz</h2>
      <p>
        In which city is there a billboard that turns air into drinkable water?
      </p>
      <form>
        <textarea disabled={status === "submitting"} />
        <br />
        <button disabled={status === "empty" || status === "submitting"}>
          Submit
        </button>
        {status === "error" && (
          <p className="Error">Good guess but a wrong answer. Try again!</p>
        )}
      </form>
    </>
  );
}
```

그리고 컴포넌트의 시각적 state를 표현하기 위해 `useState`를 사용할 것이다.

```jsx
import { useState } from "react";

export default function Form() {
  const [answer, setAnswer] = useState("");
  const [error, setError] = useState(null);
  const [status, setStatus] = useState("typing");

  if (status === "success") {
    return <h1>That's right!</h1>;
  }

  async function handleSubmit(e) {
    e.preventDefault();
    setStatus("submitting");
    try {
      await submitForm(answer);
      setStatus("success");
    } catch (err) {
      setStatus("typing");
      setError(err);
    }
  }

  function handleTextareaChange(e) {
    setAnswer(e.target.value);
  }

  return (
    <>
      <h2>City quiz</h2>
      <p>
        In which city is there a billboard that turns air into drinkable water?
      </p>
      <form onSubmit={handleSubmit}>
        <textarea
          value={answer}
          onChange={handleTextareaChange}
          disabled={status === "submitting"}
        />
        <br />
        <button disabled={answer.length === 0 || status === "submitting"}>
          Submit
        </button>
        {error !== null && <p style={{ color: "red" }}>{error.message}</p>}
      </form>
    </>
  );
}

function submitForm(answer) {
  // 네트워크에 접속한다고 가정해봅시다.
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      let shouldError = answer.toLowerCase() !== "lima";
      if (shouldError) {
        reject(new Error("Good guess but a wrong answer. Try again!"));
      } else {
        resolve();
      }
    }, 1500);
  });
}
```

## State Hooks

앞서 배운 `useState` 가 바로 내장 hook이었다.

state를 통해 컴포넌트는 사용자 입력과 같은 정보를 기억할 수 있다고 했다.

컴포넌트에 state를 추가하려면 `useState` 말고도, `useReducer` 라는 훅이 있다.

- `useState` : 직접 업데이트할 수 있는 state 변수 선언
    
    앞서 `useState` 사용법을 배웠기에 기본적인 문법은 생략한다.
    
    그 외의 내용에 대해 얘기하자면, 리스트를 렌더링할 때 `key` 속성을 전달해줘야 함을 배웠었다.
    
    리액트가 요소들을 구분할 수 있도록 도와주기 위함인데, 이 `key` 속성은 다른 용도로도 사용된다.
    
    바로, 컴포넌트에 다른 `key` 를 전달하여 컴포넌트의 state를 초기화할 수 있다.
    
    코드로 알아보자.
    
    ```jsx
    import { useState } from 'react';
    
    export default function App() {
      const [version, setVersion] = useState(0);
    
      function handleReset() {
        setVersion(version + 1);
      }
    
      return (
        <>
          <button onClick={handleReset}>Reset</button>
          <Form key={version} />
        </>
      );
    }
    
    function Form() {
      const [name, setName] = useState('Taylor');
    
      return (
        <>
          <input
            value={name}
            onChange={e => setName(e.target.value)}
          />
          <p>Hello, {name}.</p>
        </>
      );
    }
    ```
    
    위 코드를 실행시켜보면 Form 컴포넌트의 `name state` 를 변경한 것도 아닌데, `reset` 버튼을 누르면 초기화되는 것을 볼 수 있다.
    
    그 이유는 `reset` 버튼이 `version state` 변수를 변경하고, 이를 `Form` 컴포넌트의 `key` 로 전달하고 있는데, 이 때 `key` 가 변경되면 React는 `Form` 컴포넌트와 그 모든 자식을 처음부터 다시 생성한다.
    
    그래서 컴포넌트의 state가 초기화된 것이다.
    
- `useReducer` : reducer 함수 내부의 업데이트 로직을 사용하여 `state` 변수 선언
    
    말 그대로 컴포넌트에 `reducer` 를 추가하는 리액트 내장 hook이다.
    
    당연히 hook이기 때문에 컴포넌트 최상위에 호출해야 하고, reducer를 사용해 state를 관리하면 된다.
    
    기본 사용 문법은 아래와 같다.
    
    ```jsx
    useReducer(reducer, initalArg, init?)
    ```
    
    - `reducer` : state가 어떻게 업데이트 되는지 지정하는 리듀서 함수
        
        리듀서 함수는 반드시 순수 함수여야 하며, `state`와 `action`을 인수로 받아야 하고, 다음 `state`를 반환해야 한다.
        
        `state` 와 `action` 에는 모든 데이터 타입이 할당될 수 있다.
        
    - `initialArg` : 초기 `state`가 계산되는 값
        
        모든 데이터 타입이 할당될 수 있다.
        
        초기 `state` 가 어떻게 계산되는지는 다음 `init` 인수에 따라 달라진다.
        
    - 선택사항 `init` : 초기 `state` 를 반환하는 초기화 함수
        
        이 함수가 인수에 할당되지 않으면 초기 `state`는 `initialArg` 로 설정된다.
        
        할당되었다면 초기 `state` 는 `init(initialArg)` 를 호출한 결과가 할당된다.
        
    
    그럼 `useReducer` 는 어떤 것을 반환할까?
    
    `useReducer` 는 2개의 엘리먼트로 구성된 배열을 반환한다.
    
    1. 현재 `state` : 첫 번째 렌더링에서의 `state` → `init(initialArg)` 또는 `initialArg` 로 설정
    2. `dispatch` 함수 : `dispatch` 는 `state` 를 새로운 값으로 업데이트하고 리렌더링을 일으킴
    
    - 실제 사용 예시
        
        ```jsx
        import { useReducer } from 'react';
        
        function reducer(state, action) {
          // ...
        }
        
        function MyComponent() {
          const [state, dispatch] = useReducer(reducer, { age: 42 });
          // ...
        ```
        
    
    내장 훅이기에 컴포넌트 최상위 또는 커스텀 훅에서만 호출할 수 있다는 것을 알아두자.
    
    그리고 반복문이나 조건문에서는 사용할 수 없다.
    
    `dispatch` 함수에 대해서 조금 더 알아보자.
    
    `dispatch` 함수는 위에서 봤듯 `state` 를 새로운 값으로 업데이트하고 리렌더링을 일으킨다.
    
    이 함수의 유일한 인수는 `action` 인데, 이는 리듀서 함수의 매개변수로 넘겨지는 사용자에 의해 수행된 활동이다.
    
    `convention` 에 의해 일반적으로 `action` 을 정의하는 `type` 프로퍼티와 추가 정보를 표현하는 기타 프로퍼티를 포함한 객체로 구성된다.
    
    ```jsx
    const [state, dispatch] = useReducer(reducer, { age: 42 });
    
    function handleClick() {
    	// dispatch 함수는 오직 다음 렌더링에 사용할 state 변수만 업데이트
      dispatch({ type: 'incremented_age' });
      // ...
    ```
    
    그럼 직접 사용해 볼겸 카운터를 `useReducer` 로 구현해보자.
    
    ```jsx
    import { useReducer } from "react";
    
    function reducer(state, action) {
      if (action.type === "increment") {
        return { age: state.age + 1 };
      }
      throw new Error("Unknown action type");
    }
    
    export default function App() {
      const [state, dispatch] = useReducer(reducer, { age: 0 });
    
      return (
        <>
          <button onClick={() => dispatch({ type: "increment" })}>
            Increment age
          </button>
          <p>Hello! You are {state.age}.</p>
        </>
      );
    }
    ```
    
    그런데 `reducer` 함수도 일반적으로 사용되는 컨벤션이 있다. 
    
    바로 `switch` 문을 사용하는 것이다.
    
    ```jsx
    function reducer(state, action) {
      switch (action.type) {
        case "increment":
          return { age: state.age + 1 };
        default:
          throw new Error("unknown action" + action.type);
      }
    }
    ```
    
    당연히 `type` 말고도 다른 프로퍼티로 사용이 가능하다.
    
    ```jsx
    import { useReducer } from "react";
    
    function reducer(state, action) {
      switch (action.type) {
        case "increment":
          return { age: state.age + 1 };
        case "changeName":
          return { ...state, name: action.newName };
        default:
          throw new Error("unknown action" + action.type);
      }
    }
    
    export default function App() {
      const [state, dispatch] = useReducer(reducer, { name: "mandoo", age: 0 });
    
      return (
        <>
          <button onClick={() => dispatch({ type: "increment" })}>
            Increment age
          </button>
          <input
            type="text"
            value={state.name}
            onChange={(e) =>
              dispatch({ type: "changeName", newName: e.target.value })
            }
          />
          <p>
            Hello {state.name}! You are {state.age}.
          </p>
        </>
      );
    }
    ```
    
    `useReducer` 의 `state` 도 마찬가지로 직접적인 변경을 하지 말아야 한다.
    
    ```jsx
    function reducer(state, action) {
      switch (action.type) {
        case 'incremented_age': {
          // ❌ 이렇게 state를 변경하면 안됨
          state.age = state.age + 1;
          return state;
          
          // ✅ 이렇게 새로운 객체로 반환
          return {
            ...state,
            age: state.age + 1
          };
        }
    ```