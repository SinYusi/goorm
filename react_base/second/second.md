## 이벤트에 응답하라.

React에서는 JSX에 이벤트 핸들러를 추가할 수 있다.

이벤트 핸들러는 클릭, 마우스 호버, 폼 인풋 포커스 등 사용자 상호작용에 따라 유발되는 사용자 정의 함수다.

`<button>` 과 같은 내장 컴포넌트는 `onClick` 과 같은 내장 브라우저 이벤트만 지원한다.

반면 사용자 정의 컴포넌트를 생성하는 경우, 컴포넌트 이벤트 핸들러 props의 역할에 맞는 원하는 이름을 사용할 수 있다.

아래 코드를 보면 `handleClick` 함수를 정의하였고 이를 `<button>` 에 prop 형태로 전달하였다.

여기서 `handleClick` 은 이벤트 핸들러다.

```jsx
export default function Button() {
  function handleClick() {
    alert("You clicked me!");
  }

  return <button onClick={handleClick}>Click me</button>;
}

// 인라인 이벤트 핸들러도 가능합니다
export default function Button() {

  return <button onClick={() => alert("You clicked me!")}>Click me</button>;
}
```

이벤트 핸들러 함수는 다음 특징을 가진다.

- 주로 컴포넌트 내부에서 정의됨
- `handle` 로 시작하고 그 뒤에 이벤트명을 붙인 함수명을 가짐

관습적으로 `handle` 로 시작하며 이벤트명을 이어 붙인 이벤트 핸들러 명명법이 일반적이다.

ex) `onClick={handleClick}`, `onMouseEnter={handleMouseEnter}`

이벤트 핸들러로 함수를 전달할 때 주의할 점은 호출이 아닌 전달이 되어야 한다는 것이다.

```jsx
// ✅ 함수를 전달한 방식
<button onClick={handleClick}>
<button onClick={() => alert('...')}>	

// ❌ 함수를 호출한 방식
// 이 방식은 우리가 클릭하지 않아도 함수가 호출됩니다.
// 즉, 컴포넌트가 렌더링 된 시점에 그냥 실행이 되어버린다는 뜻
<button onClick={handleClick()}>
<button onClick={alert('...')}>
```

당연히 이벤트 핸들러도 컴포넌트 내부에서 선언되기 때문에 해당 컴포넌트의 prop에 접근 가능하다.

```jsx
function AlertButton({ message, children }) {
  return <button onClick={() => alert(message)}>{children}</button>;
}

export default function App() {
  return (
    <div>
      <AlertButton message="Playing!">Play Movie</AlertButton>
      <AlertButton message="Uploading!">Upload Image</AlertButton>
    </div>
  );
}
```

또한, 이벤트 핸들러 자체를 prop으로 전달할 수도 있다.

```jsx
function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}

function PlayButton({ movieName }) {
  function handlePlayClick() {
    alert(`Playing ${movieName}!`);
  }

  return (
    <Button onClick={handlePlayClick}>
      Play "{movieName}"
    </Button>
  );
}

function UploadButton() {
  return (
    <Button onClick={() => alert('Uploading!')}>
      Upload Image
    </Button>
  );
}

export default function App() {
  return (
    <div>
      <PlayButton movieName="Kiki's Delivery Service" />
      <UploadButton />
    </div>
  );
}
```

위 코드에서

- `PlayButton` 은 `handlePlayClick` 을 `Button` 내 `onClick` prop으로 전달한다.
- `UploadButton` 은 `() => alert(’Uploading!’)` 을 `Button` 내 `onClick` prop으로 전달한다.

그리고 이벤트 핸들러를 원하는대로 명명할 수 있는데, `<button>` 과 `<div>` 같은 빌트인 컴포넌트는 `onClick` 과 같은 브라우저 이벤트 이름만을 지원한다.

하지만 사용자 정의 컴포넌트에서는 이벤트 핸들러 prop의 이름을 원하는대로 명명할 수 있다.

관습적으로 이벤트 핸들러 prop의 이름은 `on` 으로 시작하여 대문자 영문으로 이어진다.

```jsx
function Button({ onSmash, children }) {
  return (
	  // prop 으로 넘거받은 이벤트 핸들러를 받아서 그대로 사용합니다.
    <button onClick={onSmash}>
      {children}
    </button>
  );
}

export default function App() {
  return (
    <div>
	    // Button 컴포넌트의 prop으로 넘겨주는 이벤트 핸들러의 이름은 on 으로 시작합니다.
      <Button onSmash={() => alert('Playing!')}>
        Play Movie
      </Button>
      <Button onSmash={() => alert('Uploading!')}>
        Upload Image
      </Button>
    </div>
  );
}
```

## 당연히 이벤트 전파가 된다.

이전에 배웠던 이벤트 버블링에 대해 기억한다면 어렵지 않은 내용이다.

```jsx
export default function App() {
  return (
    <div
      style={{ backgroundColor: "lightblue", padding: "20px" }}
      onClick={() => {
        alert("You clicked on the toolbar!");
      }}
    >
      <button onClick={() => alert("Playing!")}>Play Movie</button>
      <button onClick={() => alert("Uploading!")}>Upload Image</button>
    </div>
  );
}
```

둘 중의 어느 버튼을 클릭하더라도 해당 버튼의 `onClick` 이 먼저 실행될 것이며 이후 부모인 `<div>` 의 `onClick` 이 뒤이어 실행될 것이다.

만약 툴바 자체를 클릭한다면 오직 부모인 `<div>` 의 `onClick` 만 실행될 것.

이벤트 전파를 막고 싶다면 `e.stopPropagation()` 을 호출해야 한다.

```jsx
export default function App() {
  return (
    <div
      style={{ backgroundColor: "lightblue", padding: "20px" }}
      onClick={() => {
        alert("You clicked on the toolbar!");
      }}
    >
      <button
        onClick={(e) => {
	        // e.stopPropagation()을 호출하여 이벤트가 더 이상 bubbling 되지 않도록 방지
          e.stopPropagation();
          alert("Playing!");
        }}
      >
        Play Movie
      </button>
      <button onClick={() => alert("Uploading!")}>Upload Image</button>
    </div>
  );
}
```

## State로 데이터를 기억하자.

컴포넌트는 상호 작용의 결과로 화면의 내용을 변경해야 하는 경우가 많다.

폼에 입력하면 입력 필드가 업데이트되어야하고, 이미지 캐러셀에서 “다음”을 클릭할 때 표시되는 이미지가 변경되어야 하고, “구매”를 클릭하면 상품이 장바구니에 담겨야 한다.

컴포넌트는 현재 입력값, 현재 이미지, 장바구니와 같은 것들을 “기억”해야 한다.

React는 이런 종류의 컴포넌트별 메모리를 state라고 부른다.

아래 코드를 실행시켜보면 `Next` 버튼을 눌러도 아무런 변화가 일어나지 않는 것을 볼 수 있다.

- data.js
    
    ```jsx
    export const sculptureList = [
      {
        name: "Homenaje a la Neurocirugía",
        artist: "Marta Colvin Andrade",
        description:
          "Although Colvin is predominantly known for abstract themes that allude to pre-Hispanic symbols, this gigantic sculpture, an homage to neurosurgery, is one of her most recognizable public art pieces.",
        url: "https://i.imgur.com/Mx7dA2Y.jpg",
        alt: "A bronze statue of two crossed hands delicately holding a human brain in their fingertips.",
      },
      {
        name: "Floralis Genérica",
        artist: "Eduardo Catalano",
        description:
          "This enormous (75 ft. or 23m) silver flower is located in Buenos Aires. It is designed to move, closing its petals in the evening or when strong winds blow and opening them in the morning.",
        url: "https://i.imgur.com/ZF6s192m.jpg",
        alt: "A gigantic metallic flower sculpture with reflective mirror-like petals and strong stamens.",
      },
      {
        name: "Eternal Presence",
        artist: "John Woodrow Wilson",
        description:
          'Wilson was known for his preoccupation with equality, social justice, as well as the essential and spiritual qualities of humankind. This massive (7ft. or 2,13m) bronze represents what he described as "a symbolic Black presence infused with a sense of universal humanity."',
        url: "https://i.imgur.com/aTtVpES.jpg",
        alt: "The sculpture depicting a human head seems ever-present and solemn. It radiates calm and serenity.",
      },
      {
        name: "Moai",
        artist: "Unknown Artist",
        description:
          "Located on the Easter Island, there are 1,000 moai, or extant monumental statues, created by the early Rapa Nui people, which some believe represented deified ancestors.",
        url: "https://i.imgur.com/RCwLEoQm.jpg",
        alt: "Three monumental stone busts with the heads that are disproportionately large with somber faces.",
      },
      {
        name: "Blue Nana",
        artist: "Niki de Saint Phalle",
        description:
          "The Nanas are triumphant creatures, symbols of femininity and maternity. Initially, Saint Phalle used fabric and found objects for the Nanas, and later on introduced polyester to achieve a more vibrant effect.",
        url: "https://i.imgur.com/Sd1AgUOm.jpg",
        alt: "A large mosaic sculpture of a whimsical dancing female figure in a colorful costume emanating joy.",
      },
      {
        name: "Ultimate Form",
        artist: "Barbara Hepworth",
        description:
          "This abstract bronze sculpture is a part of The Family of Man series located at Yorkshire Sculpture Park. Hepworth chose not to create literal representations of the world but developed abstract forms inspired by people and landscapes.",
        url: "https://i.imgur.com/2heNQDcm.jpg",
        alt: "A tall sculpture made of three elements stacked on each other reminding of a human figure.",
      },
      {
        name: "Cavaliere",
        artist: "Lamidi Olonade Fakeye",
        description:
          "Descended from four generations of woodcarvers, Fakeye's work blended traditional and contemporary Yoruba themes.",
        url: "https://i.imgur.com/wIdGuZwm.png",
        alt: "An intricate wood sculpture of a warrior with a focused face on a horse adorned with patterns.",
      },
      {
        name: "Big Bellies",
        artist: "Alina Szapocznikow",
        description:
          "Szapocznikow is known for her sculptures of the fragmented body as a metaphor for the fragility and impermanence of youth and beauty. This sculpture depicts two very realistic large bellies stacked on top of each other, each around five feet (1,5m) tall.",
        url: "https://i.imgur.com/AlHTAdDm.jpg",
        alt: "The sculpture reminds a cascade of folds, quite different from bellies in classical sculptures.",
      },
      {
        name: "Terracotta Army",
        artist: "Unknown Artist",
        description:
          "The Terracotta Army is a collection of terracotta sculptures depicting the armies of Qin Shi Huang, the first Emperor of China. The army consisted of more than 8,000 soldiers, 130 chariots with 520 horses, and 150 cavalry horses.",
        url: "https://i.imgur.com/HMFmH6m.jpg",
        alt: "12 terracotta sculptures of solemn warriors, each with a unique facial expression and armor.",
      },
      {
        name: "Lunar Landscape",
        artist: "Louise Nevelson",
        description:
          "Nevelson was known for scavenging objects from New York City debris, which she would later assemble into monumental constructions. In this one, she used disparate parts like a bedpost, juggling pin, and seat fragment, nailing and gluing them into boxes that reflect the influence of Cubism’s geometric abstraction of space and form.",
        url: "https://i.imgur.com/rN7hY6om.jpg",
        alt: "A black matte sculpture where the individual elements are initially indistinguishable.",
      },
      {
        name: "Aureole",
        artist: "Ranjani Shettar",
        description:
          'Shettar merges the traditional and the modern, the natural and the industrial. Her art focuses on the relationship between man and nature. Her work was described as compelling both abstractly and figuratively, gravity defying, and a "fine synthesis of unlikely materials."',
        url: "https://i.imgur.com/okTpbHhm.jpg",
        alt: "A pale wire-like sculpture mounted on concrete wall and descending on the floor. It appears light.",
      },
      {
        name: "Hippos",
        artist: "Taipei Zoo",
        description:
          "The Taipei Zoo commissioned a Hippo Square featuring submerged hippos at play.",
        url: "https://i.imgur.com/6o5Vuyu.jpg",
        alt: "A group of bronze hippo sculptures emerging from the sett sidewalk as if they were swimming.",
      },
    ];
    ```
    
- Gallery.jsx
    
    ```jsx
    import { sculptureList } from "./data.js";
    
    export default function Gallery() {
      let index = 0;
    
      function handleClick() {
        index = index + 1;
      }
    
      let sculpture = sculptureList[index];
      return (
        <>
          <button onClick={handleClick}>Next</button>
          <h2>
            <i>{sculpture.name} </i>
            by {sculpture.artist}
          </h2>
          <h3>
            ({index + 1} of {sculptureList.length})
          </h3>
          <img src={sculpture.url} alt={sculpture.alt} />
          <p>{sculpture.description}</p>
        </>
      );
    }
    ```
    

`handleClick` 이벤트 핸들러는 지역 변수 `index` 를 업데이트하고 있다.

하지만 이러한 변화를 보이지 않게 하는 두 가지 이유가 있다.

1. 지역 변수는 렌더링 간에 유지되지 않는다.
    
    React는 이 컴포넌트를 두 번째로 렌더링할 때 지역 변수에 대한 변경 사항은 고려하지 않고 처음부터 렌더링한다.
    
2. 지역 변수는 변경해도 렌더링을 일으키지 않는다.
    
    React는 새로운 데이터로 컴포넌트를 다시 렌더링해야 한다는 것을 인식하지 못한다.
    

React에서 컴포넌트를 새로운 데이터로 업데이트하기 위해선 아래 두 가지가 필요하다.

1. 렌더링 사이에 데이터를 유지한다.
2. React가 새로운 데이터로 컴포넌트를 렌더링하도록 유발한다.

위 2가지 기능을 제공하는 것이 바로 `useState` 이다.

## `useState` Hook

1. 렌더링 간에 데이터를 유지하기 위한 state 변수.
2. 변수를 업데이트하고 React가 컴포넌트를 다시 렌더링하도록 유발하는 state setter 함수
- 기본적인 사용법
    
    ```jsx
    import { useState } from 'react';
    
    const [state, setState] = useState()
    ```
    

위에서 제대로 작동하지 않았던 코드를 `useState` 를 활용해 제대로 동작해보도록 수정해보자.

```jsx
import { useState } from "react";
import { sculptureList } from "./data.js";

export default function Gallery() {
  const [index, setIndex] = useState(0);

  function handleClick() {
    setIndex(index + 1);
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleClick}>Next</button>
      <h2>
        <i>{sculpture.name} </i>
        by {sculpture.artist}
      </h2>
      <h3>
        ({index + 1} of {sculptureList.length})
      </h3>
      <img src={sculpture.url} alt={sculpture.alt} />
      <p>{sculpture.description}</p>
    </>
  );
}
```

`useState` 를 사용할 때 `const [something, setSomething]` 과 같이 지정하는 것이 규칙이다.

`useState` 의 유일한 인수는 `state` 변수의 초기값이다.

위 코드에서 `useState(0)` 에 의해 `index` 의 초기값이 0으로 설정되는 것이다.

```jsx
const [index, setIndex] = useState(0);
```

그렇게 위 코드가 작동하는 방식은

1. 컴포넌트가 처음 렌더링
    
    `index` 의 초기값으로 `useState` 를 사용해 `0` 을 전달했으므로 `[0, setIndex]` 를 반환한다. React는 `0` 을 최신 state값으로 기억한다.
    
2. state를 업데이트
    
    사용자가 버튼을 클릭하면 `setIndex(index + 1)` 를 호출한다.
    
    `index` 는 `0` 이므로 `setIndex(1)` 이다.
    
    이는 React에 `index` 는 `1` 임을 기억하게 하고 또 다른 렌더링을 유발한다.
    
3. 컴포넌트가 두 번째로 렌더링
    
    React는 여전히 `useState(0)` 를 보지만, `index` 를 `1` 로 설정한 것을 기억하고 있기에, 이번에는 `[1, setIndex]` 를 반환한다.
    

위와 같은 방식으로 state가 업데이트된다.

- 한 컴포넌트에 여러 state 변수 저장할 수 있음
    
    ```jsx
    import { useState } from 'react';
    import { sculptureList } from './data.js';
    
    export default function Gallery() {
      const [index, setIndex] = useState(0);
      const [showMore, setShowMore] = useState(false);
    
      function handleNextClick() {
        setIndex(index + 1);
      }
    
      function handleMoreClick() {
        setShowMore(!showMore);
      }
    
      let sculpture = sculptureList[index];
      return (
        <>
          <button onClick={handleNextClick}>
            Next
          </button>
          <h2>
            <i>{sculpture.name} </i>
            by {sculpture.artist}
          </h2>
          <h3>
            ({index + 1} of {sculptureList.length})
          </h3>
          <button onClick={handleMoreClick}>
            {showMore ? 'Hide' : 'Show'} details
          </button>
          {showMore && <p>{sculpture.description}</p>}
          <img
            src={sculpture.url}
            alt={sculpture.alt}
          />
        </>
      );
    }
    ```
    
- 같은 컴포넌트라도 state는 공유되지 않는다.
    
    아래 코드를 같이 실행시켜보면서 동일한 컴포넌트를 호출했을 때 state가 어떻게 동작하는지 보자.
    
    각 컴포넌트의 state가 서로 독립적으로 변경된다는 것을 확인하면 된다.
    
    - App.jsx
        
        ```jsx
        import { useState } from "react";
        import { sculptureList } from "./data.js";
        import "./App.css";
        
        function Gallery() {
          const [index, setIndex] = useState(0);
          const [showMore, setShowMore] = useState(false);
        
          function handleNextClick() {
            setIndex(index + 1);
          }
        
          function handleMoreClick() {
            setShowMore(!showMore);
          }
        
          let sculpture = sculptureList[index];
          return (
            <section>
              <button onClick={handleNextClick}>Next</button>
              <h2>
                <i>{sculpture.name} </i>
                by {sculpture.artist}
              </h2>
              <h3>
                ({index + 1} of {sculptureList.length})
              </h3>
              <button onClick={handleMoreClick}>
                {showMore ? "Hide" : "Show"} details
              </button>
              {showMore && <p>{sculpture.description}</p>}
              <img src={sculpture.url} alt={sculpture.alt} />
            </section>
          );
        }
        
        export default function App() {
          return (
            <div className="page">
              <Gallery />
              <Gallery />
            </div>
          );
        }
        
        ```
        
    - App.css
        
        ```jsx
        .page {
          display: flex;
        }
        
        .page > section {
          width: 50%;
          border: 1px solid black;
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          margin: 10px;
          padding: 10px;
        }
        ```
        
    - data.js
        
        ```jsx
        export const sculptureList = [
          {
            name: "Homenaje a la Neurocirugía",
            artist: "Marta Colvin Andrade",
            description:
              "Although Colvin is predominantly known for abstract themes that allude to pre-Hispanic symbols, this gigantic sculpture, an homage to neurosurgery, is one of her most recognizable public art pieces.",
            url: "https://i.imgur.com/Mx7dA2Y.jpg",
            alt: "A bronze statue of two crossed hands delicately holding a human brain in their fingertips.",
          },
          {
            name: "Floralis Genérica",
            artist: "Eduardo Catalano",
            description:
              "This enormous (75 ft. or 23m) silver flower is located in Buenos Aires. It is designed to move, closing its petals in the evening or when strong winds blow and opening them in the morning.",
            url: "https://i.imgur.com/ZF6s192m.jpg",
            alt: "A gigantic metallic flower sculpture with reflective mirror-like petals and strong stamens.",
          },
          {
            name: "Eternal Presence",
            artist: "John Woodrow Wilson",
            description:
              'Wilson was known for his preoccupation with equality, social justice, as well as the essential and spiritual qualities of humankind. This massive (7ft. or 2,13m) bronze represents what he described as "a symbolic Black presence infused with a sense of universal humanity."',
            url: "https://i.imgur.com/aTtVpES.jpg",
            alt: "The sculpture depicting a human head seems ever-present and solemn. It radiates calm and serenity.",
          },
          {
            name: "Moai",
            artist: "Unknown Artist",
            description:
              "Located on the Easter Island, there are 1,000 moai, or extant monumental statues, created by the early Rapa Nui people, which some believe represented deified ancestors.",
            url: "https://i.imgur.com/RCwLEoQm.jpg",
            alt: "Three monumental stone busts with the heads that are disproportionately large with somber faces.",
          },
          {
            name: "Blue Nana",
            artist: "Niki de Saint Phalle",
            description:
              "The Nanas are triumphant creatures, symbols of femininity and maternity. Initially, Saint Phalle used fabric and found objects for the Nanas, and later on introduced polyester to achieve a more vibrant effect.",
            url: "https://i.imgur.com/Sd1AgUOm.jpg",
            alt: "A large mosaic sculpture of a whimsical dancing female figure in a colorful costume emanating joy.",
          },
          {
            name: "Ultimate Form",
            artist: "Barbara Hepworth",
            description:
              "This abstract bronze sculpture is a part of The Family of Man series located at Yorkshire Sculpture Park. Hepworth chose not to create literal representations of the world but developed abstract forms inspired by people and landscapes.",
            url: "https://i.imgur.com/2heNQDcm.jpg",
            alt: "A tall sculpture made of three elements stacked on each other reminding of a human figure.",
          },
          {
            name: "Cavaliere",
            artist: "Lamidi Olonade Fakeye",
            description:
              "Descended from four generations of woodcarvers, Fakeye's work blended traditional and contemporary Yoruba themes.",
            url: "https://i.imgur.com/wIdGuZwm.png",
            alt: "An intricate wood sculpture of a warrior with a focused face on a horse adorned with patterns.",
          },
          {
            name: "Big Bellies",
            artist: "Alina Szapocznikow",
            description:
              "Szapocznikow is known for her sculptures of the fragmented body as a metaphor for the fragility and impermanence of youth and beauty. This sculpture depicts two very realistic large bellies stacked on top of each other, each around five feet (1,5m) tall.",
            url: "https://i.imgur.com/AlHTAdDm.jpg",
            alt: "The sculpture reminds a cascade of folds, quite different from bellies in classical sculptures.",
          },
          {
            name: "Terracotta Army",
            artist: "Unknown Artist",
            description:
              "The Terracotta Army is a collection of terracotta sculptures depicting the armies of Qin Shi Huang, the first Emperor of China. The army consisted of more than 8,000 soldiers, 130 chariots with 520 horses, and 150 cavalry horses.",
            url: "https://i.imgur.com/HMFmH6m.jpg",
            alt: "12 terracotta sculptures of solemn warriors, each with a unique facial expression and armor.",
          },
          {
            name: "Lunar Landscape",
            artist: "Louise Nevelson",
            description:
              "Nevelson was known for scavenging objects from New York City debris, which she would later assemble into monumental constructions. In this one, she used disparate parts like a bedpost, juggling pin, and seat fragment, nailing and gluing them into boxes that reflect the influence of Cubism’s geometric abstraction of space and form.",
            url: "https://i.imgur.com/rN7hY6om.jpg",
            alt: "A black matte sculpture where the individual elements are initially indistinguishable.",
          },
          {
            name: "Aureole",
            artist: "Ranjani Shettar",
            description:
              'Shettar merges the traditional and the modern, the natural and the industrial. Her art focuses on the relationship between man and nature. Her work was described as compelling both abstractly and figuratively, gravity defying, and a "fine synthesis of unlikely materials."',
            url: "https://i.imgur.com/okTpbHhm.jpg",
            alt: "A pale wire-like sculpture mounted on concrete wall and descending on the floor. It appears light.",
          },
          {
            name: "Hippos",
            artist: "Taipei Zoo",
            description:
              "The Taipei Zoo commissioned a Hippo Square featuring submerged hippos at play.",
            url: "https://i.imgur.com/6o5Vuyu.jpg",
            alt: "A group of bronze hippo sculptures emerging from the sett sidewalk as if they were swimming.",
          },
        ];
        
        ```
        

## state에서 반드시 알아야 할 것

아래 코드를 실행해보자.

```jsx
import { useState } from "react";

export default function App() {
  const [number, setNumber] = useState(0);

  return (
    <main>
      <h1>{number}</h1>
      <button
        onClick={() => {
          setNumber(number + 1);
          setNumber(number + 1);
          setNumber(number + 1);
        }}
      >
        +3
      </button>
    </main>
  );
}
```

위 코드에서 버튼을 클릭하면 +3이 아닌 +1씩 증가하는 것을 볼 수 있다.

분명 `setNumber(number + 1)` 를 3번이나 호출했는데 말이다.

위에서 클릭 이벤트 핸들러가 어떻게 동작하는지 자세히 살펴보자.

1. `setNumber(number + 1)` : `number` 는 `0` 이므로 `setNumber(0 + 1)` 동작, React는 다음 렌더링에서 `number` 을 `1` 로 변경할 준비
2. `setNumber(number + 1)` : `number` 는 `0`이므로 `setNumber(0 + 1)` 동작, React는 다음 렌더링에서 `number`를 `1`로 변경할 준비
3. `setNumber(number + 1)` : `number` 는 `0`이므로 `setNumber(0 + 1)` 동작, React는 다음 렌더링에서 `number`를 `1`로 변경할 준비

위와 같이 동작해서 `setNumber`을 3번 호출했더라도, 이 렌더링에서 이벤트 핸들러의 `number` 는 항상 0이기에 click 이벤트 핸들러가 호출되면 state가 1로 설정되는 것이다.

즉 위 코드는 아래와 같은 코드라는 것이다.

```jsx
<button onClick={() => {
  setNumber(0 + 1);
  setNumber(0 + 1);
  setNumber(0 + 1);
}}>+3</button>
```

다른 예제도 살펴보자. 아래 버턴을 클릭하면 alert 창으로 어떤 `number` 가 뜰까?

```jsx
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 5);
        alert(number);
      }}>+5</button>
    </>
  )
}
```

예상대로 0이 뜰 것이다. 위 버튼 이벤트 핸들러는 아래와 같은 코드니까.

```jsx
setNumber(0 + 5);
alert(0);
```

그럼 이번엔 타이머를 설정해보자. alert 창에 뜨는 number은 무엇일까?

```jsx
import { useState } from 'react';

export default function Counter() {
  const [number, setNumber] = useState(0);

  return (
    <>
      <h1>{number}</h1>
      <button onClick={() => {
        setNumber(number + 5);
        setTimeout(() => {
          alert(number);
        }, 3000);
      }}>+5</button>
    </>
  )
}
```

alert 창에는 0이 뜰 것이다. 다음과 같은 코드라고 생각하면 편할 것이다.

```jsx
setNumber(0 + 5);
setTimeout(() => {
  alert(0);
}, 3000);
```

그래서 alert이 실행되었을 때 실제 화면 상 `number` 값은 변경되었을 수 있지만, 사용자가 alert을 보는 시점에 state는 이미 0으로 예약되어 있던 것이다.

state 변수의 값은 이벤트 핸들러의 코드가 비동기적이더라도 렌더링 내에서 절대 변경되지 않는다.

- 그럼 진짜 +3을 하고 싶으면 어떻게 해야하지?
    
    그럴 때에는 업데이트 함수를 전달해주면 된다.
    
    ```jsx
    import { useState } from 'react';
    
    export default function Counter() {
      const [number, setNumber] = useState(0);
    
      return (
        <>
          <h1>{number}</h1>
          <button onClick={() => {
            setNumber(n => n + 1);
            setNumber(n => n + 1);
            setNumber(n => n + 1);
          }}>+3</button>
        </>
      )
    }
    ```
    
    위 코드는 아래와 같은 순서로 동작한다.
    
    1. `setNumber(n => n + 1)`: `n => n + 1` 함수를 큐에 추가
    2. `setNumber(n => n + 1)`: `n => n + 1` 함수를 큐에 추가
    3. `setNumber(n => n + 1)`: `n => n + 1` 함수를 큐에 추가
    
    | queued update | `n` | returns |
    | --- | --- | --- |
    | `n => n + 1` | `0` | `0 + 1 = 1` |
    | `n => n + 1` | `1` | `1 + 1 = 2` |
    | `n => n + 1` | `2` | `2 + 1 = 3` |
    
    그렇게 최종적으로 3을 state에 저장하고, 반환하는 것이다.
    
    업데이트 함수 인수의 이름은 해당 state 변수의 첫 글자로 지정하는 것이 일반적이다.
    
    좀 더 자세한 코드를 선호하는 경우에는 state 변수 이름 전체를 작성하거나 `setEnabled(prevEnabled => !prevEnabled)` 와 같은 접두사를 사용하면 된다.
    

## 객체 State 업데이트하는 방법

이번엔 state 내에 객체가 들어갔을 때에 어떻게 해야하는지 알아보자.

아래 예시 코드를 살펴보며 객체의 값을 어떻게 바꾸는지 살펴보자.

```jsx
import { useState } from "react";

export default function MovingDot() {
  const [position, setPosition] = useState({
    x: 0,
    y: 0,
  });
  return (
    <div
      onPointerMove={(e) => {
        setPosition({
          x: e.clientX,
          y: e.clientY,
        });
      }}
      style={{
        position: "relative",
        width: "100vw",
        height: "100vh",
      }}
    >
      <div
        style={{
          position: "absolute",
          backgroundColor: "red",
          borderRadius: "50%",
          transform: `translate(${position.x}px, ${position.y}px)`,
          left: -10,
          top: -10,
          width: 20,
          height: 20,
        }}
      />
    </div>
  );
}
```

만약, 객체의 일부 데이터만을 바꾸고 싶다면 어떻게 해야할까?

아래와 같이 코드를 짜면 될까?

```jsx
import { useState } from 'react';

export default function Form() {
  const [person, setPerson] = useState({
    firstName: 'Barbara',
    lastName: 'Hepworth',
    email: 'bhepworth@sculpture.com'
  });

  function handleFirstNameChange(e) {
    person.firstName = e.target.value;
  }

  function handleLastNameChange(e) {
    person.lastName = e.target.value;
  }

  function handleEmailChange(e) {
    person.email = e.target.value;
  }

  return (
    <>
      <label>
        First name:
        <input
          value={person.firstName}
          onChange={handleFirstNameChange}
        />
      </label>
      <label>
        Last name:
        <input
          value={person.lastName}
          onChange={handleLastNameChange}
        />
      </label>
      <label>
        Email:
        <input
          value={person.email}
          onChange={handleEmailChange}
        />
      </label>
      <p>
        {person.firstName}{' '}
        {person.lastName}{' '}
        ({person.email})
      </p>
    </>
  );
}
```

당연히 제대로 동작하지 않는다. 우리는 setter 함수를 사용해 state를 변경해줘야 한다.

이 때에 spread 연산자를 사용할 수 있다.

```jsx
function handleFirstNameChange(e) {
  setPerson({ ...person, firstName: e.target.value });
}

function handleLastNameChange(e) {
  setPerson({ ...person, lastName: e.target.value });
}

function handleEmailChange(e) {
  setPerson({ ...person, email: e.target.value });
}
```