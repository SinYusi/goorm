## OOP의 핵심, 상속

OOP에서 가장 중요한 개념 중 하나인 `“상속”`을 알아보자.

상속은 코드의 중복을 줄이고, 코드를 재사용 가능한 조각으로 나눌 수 있다.

코드에서의 상속 개념은 `“자녀 클래스가 부모 클래스의 속성을 갖게 되는 것”`이다.

예를 들어, 인간 키우기 RPG 게임이 있다고 생각해보자.

아기 때 캐릭터 → 청소년 캐릭터 → 어른 캐릭터 순으로 캐릭터가 필요할 것이다.

클래스를 사용한다면 다음과 같이 만들 수 있을 것이다.

```jsx
class Baby {
	constructor(name) {
		this.name = name;
		this.arms = 2;
		this.legs = 2;
		this.cute = true;
	}
	cry() {
		return "응애"
	}
}

class Teenager {
	constructor(name) {
		this.name = name;
		this.arms = 2;
		this.legs = 2;
		this.emotional = true;
	}
	study() {
		return "열공중"
	}
}

class Human {
	constructor(name) {
		this.name = name;
		this.arms = 2;
		this.legs = 2;
	}
}
```

이렇게 클래스를 만들어 봤는데, 여기서 중복되는 코드가 보인다.

바로, `Baby`, `Teenager` 클래스는 `Human`에 속해있다는 것이다.

`Human` 의 속성을 전부 가지고 있으며 각각 다른 속성들을 가지고 있으니까.

이 때 필요한 개념이 `“상속”` 이다. 상속을 적용한 코드를 보자.

```jsx
// ⚠️ 아직 아래 코드가 정상 작동하지 않음
class Human {
	constructor(name) {
		this.name = name;
		this.arms = 2;
		this.legs = 2;
	}
}

// extends 키워드를 통해 Human의 속성을 전부 가지면서 그들만의 데이터를 넣어 확장하는 것
class Baby extends Human {
	constructor(name) {
		this.cute = true;
	}
	cry() {
		return "응애"
	}
}

class Teenager extends Human {
	constructor(name) {
		this.emotional = true;
	}
	study() {
		return "열공중"
	}
}

const mandooBaby = new Baby("mandoo")
console.log(mandooBaby)
```

위 코드가 작동하지 않는 이유는 Human constructor는 인수에 따라 인간의 이름을 정하기 때문이다.

상속 받은 부모 클래스가 정상적으로 작동하려면 `super` 라는 키워드를 호출해야 한다.

```jsx
class Human {
	constructor(name) {
		this.name = name;
		this.arms = 2;
		this.legs = 2;
	}
}

// extends 키워드를 통해 Human의 속성을 전부 가지면서 그들만의 데이터를 넣어 확장하는 것
class Baby extends Human {
	constructor(name) {
		super(name)
		this.cute = true;
	}
	cry() {
		return "응애"
	}
}

class Teenager extends Human {
	constructor(name) {
		super(name)
		this.emotional = true;
	}
	study() {
		return "열공중"
	}
}

const mandooBaby = new Baby("mandoo")
console.log(mandooBaby) // Baby {name: 'mandoo', arms: 2, legs: 2, cute: true}
```

4가지 핵심 용어와 개념을 살펴보자.

- 캡슐화 (Encapsulation)
    
    데이터, 그리고 데이터를 활용하는 함수를 캡슐 혹은 컨테이너 안에 두는 것을 의미한다.
    
    이 경우 캡슐은 `class`를 의미한다.
    
    캢ㄹ화는 어떻게 클래스 정보에 접근 혹은 수정하는지를 결정하는 권한을 제공한다.
    
    따라서 데이터와 class 안에 있는 해당 데이터를 이용하는 함수를 장 정리하는 방법론이다.
    
- 상속 (Inheritance)
    
    상속 덕분에 코드를 더 작게 쪼개고, 재사용할 수 있게 되었다.
    
    자세한 내용은 위 내용과 같다.
    
- 추상화 (Abstraction)
    
    구현 세부 정보를 숨기는 일반 인터페이스를 지정하는 행위라고 정의할 수 있다.
    
    예를 들자면, 운전으로 예를 들 수 있다.
    
    엑셀, 브레이크, 각종 버튼들을 인터페이스라고 할 수 있는데, 이 인터페이스는 차량 제조사가 우리에게 운전을 위해 노출시켜 만들어둔 것이다.
    
    우리는 액셀을 밟으면 어떤 원리로 차가 움직이는지 내부 로직은 알지 못해도 운전할 수 있다.
    
    이렇게 세부 로직, 내부 정보들은 전부 숨겨져 있는 것이다.
    
    즉, 차가 앞으로 나갈 수 있도록 만든 내부의 세부 로직들을 엑셀이란 인터페이스로 추상화한 것이다.
    
    ```jsx
    class ArrayAbstracition {
    	#items;
    	
    	constructor() {
    		this.#items = []
    	}
    	
    	// 이 메서드들이 items라는 private변수를 편하게 조종할 수 있는 노출된 인터페이스임
    	// 즉, 이 메서드가 밖에서 접근하여 내부 items를 조종할 수 있다
    	getItems() {
    		return [...this.#items]
    	}
    	
    	addItems(item) {
    		return this.#items.push(item)
    	}
    }
    
    const result = new ArrayAbstracition()
    
    // 배열에 어떻게 값을 추가하는지 즉, push()를 몰라도 addItems()만 사용하면 배열에 추가할 수 있다
    // 즉, ArrayAbstracition의 인터페이스를 만든 것이다
    result.addItems("HI")
    result.addItems("BYE")
    
    console.log(result.getItems())
    
    ```
    
    이렇게 코드를 추상화해두면 뭐가 좋을까?
    
    바로, 내부 로직이 수정되어야할 때 아무도 모르게 해당 메서드 내부의 코드만 변경하면 된다는 것이다.
    
    즉, 인터페이스 함수를 사용하는 사람은 내부 로직이 바뀐지도 모를 것이다.
    
- 다형성 (Polymorphism)
    
    poly(여러개) + morphos(형태, 모양) = 여러 개의 형태 = 다형성
    
    ```jsx
    class Person {
    	sayHi() {
    		console.log("HIIII")
    	}
    	sayBye() {
    		console.log("BYEEEE")
    	}
    }
    
    // Korean, American 두 인스턴스는 Person 클래스를 상속 받았음.
    // 즉, 두 인스턴스 모두 sayHi(), sayBye() 메서드를 갖는다는 뜻
    class Korean extends Person {}
    class American extends Person {}
    ```
    
    여기서 만약 `Korean` 클래스에서 `sayHi` 가 다른 콘솔을 출력하길 원하면 `Korean` 에만 메서드를 재정의해줄 필요가 있다.
    
    ```jsx
    class Korean extends Person {
    	sayHi() {
    		console.log("안녕, 나는 한국인이야.")
    	}
    }
    ```
    
    이런 식으로 이미 부모 클래스에 같은 메서드가 있는데 자식 클래스에서 같은 이름의 메서드를 다시 정의한 것을 method overriding(메서드 오버라이딩)이라고 한다.
    
    `sayHi` 라는 같은 함수의 이름이 쓰였지만, 다른 구현 방식인 상황을 말하는 것이다.
    
    다형성을 위해 지켜줘야 할 것이 있는데,
    
    ```jsx
    class Person {
    	sayHi() {
    		console.log("HIIII")
    		return "HIIII" // 부모가 string을 return 하기 때문에
    	}
    	sayBye() {
    		console.log("BYEEEE")
    	}
    }
    
    class Korean extends Person {
    	sayHi() {
    		console.log("안녕, 나는 한국인이야.")
    		// 만약 여기 숫자를 썼다면 타입스크립트는 에러를 뿜을 것입니다.
    		return "안녕, 나는 한국인이야." // 상속받은 자식도 string을 return 해야 합니다
    	}
    }
    
    class American extends Person {}
    
    const 한국인 = new Korean()
    const 미국인 = new American()
    
    한국인.sayHi() // "안녕, 나는 한국인이야."
    미국인.sayHi() // "HIIII"
    ```
    
    이렇게 부모와 자식에서 메서드 오버라이딩이 필요할 때 같은 자료형을 `return` 해주는 것이 OOP에서의 다형성이다. 
    

## 함수형 프로그래밍이란?

현 트렌드까지 OOP를 사용한 이유는 인간의 사고방식과 유사했기 때문이고, 보편화되어 많은 언어들이 지원했기 때문이다.

하지만 요즘 AI, 빅데이터, 비트코인이 뜨기 시작하며 방대한 데이터를 빠르게 계산하여 병렬적으로, 그리고 안정적으로 처리하는 것의 중요성이 부각되며 함수형 프로그래밍이 주목받기 시작했다.

함수형 프로그래밍은 수학과 관련이 있다.

수학에서는 주어진 데이터를 통해서 결과값을 도출한다.

즉, 인풋이 들어오면 내부 로직을 통해 아웃풋을 도출한다. << 외부에서는 내부 로직을 볼 수 없음

정리하자면, 함수형 프로그래밍을 진행한다는 것은 이런 함수들을 적용하고 묶어서 프로그램을 구성해나가는 것을 의미한다.

- 함수형 프로그래밍의 특징
    1. 순수 함수(Pure Function)
        
        ```jsx
        // ❌ 
        let num = 1
        function add(a) {
        	return a + num; // 외부 값 참조하고 있으니 순수 함수가 아님
        }
        // ✅
        function add(a,b) {
        	return a + b; // 늘 받아온 인자를 더한 결과값을 반환하기 때문에 순수 함수임
        }
        const result = add(2,3)
        ```
        
        1. 함수에서 외부의 상태값을 참조하거나 또는 외부의 상태를 변경하는 것은 순수 함수가 아님
        (만약 함수에서 외부 상태를 변경한다면 OOP에 가까움)
        2. 동일한 인자를 넣었을 때 항상 동일한 결과값을 반환하고, 언제 선언됐든지 외부에 전혀 영향을 받지 않도록 작성한 것이 순수 함수
    2. Stateless(비상태), Immutability(불변성) 유지
        
        다음과 같이 함수에 인자로 전달된 데이터를 변경하는 것은 함수형 프로그래밍이 아니다.
        
        ```jsx
        // X
        let person = {name: 'mandoo', age: 2}
        function increaseAge(person) {
        	person.age = person.age + 1
        	return person
        }
        ```
        
        함수형 프로그래밍에서는 전달된 데이터를 변경하는 것이 아닌, 새로운 버전의 새로운 오브젝트를 만들어서 결과값으로 전달해야 한다.
        
        ```jsx
        let person = {name: 'mandoo', age: 2}
        function increaseAge(person) {
        	return {...person, age: person.age + 1}
        }
        ```
        
        JavaScript에서 객체를 불변성으로 만들어주기 위해 `Object.freeze()` 를 사용할 수 있다.
        
        ```jsx
        let person = Object.freeze({name: 'mandoo', age: 2})
        function increaseAge(person) {
        	return Object.freeze({...person, age: person.age + 1})
        }
        ```
        
        `Object.freeze()` 란 객체를 동결하는 메서드이다. 동결된 객체는 더 이상 변경될 수 없다.
        
        즉, 객체에 새로운 속성을 추가하거나 제거하거나 변경하는 것을 방지한다.
        
        위와 같이 함수형 프로그래밍은 외부의 상태나 데이터를 변경하지 않음으로써 side effect를 만들지 않아 불변성을 유지할 수 있게 된다.(side effect: 함수를 호출하면 외부의 상태가 변경되거나 예상치 못한 에러가 발생하는 것)
        
    3. Expressions only (expressions를 사용)
        
        `if`, `switch`, `for` 문과 같은 여러가지 문장을 사용하는 것은 함수형 프로그래밍이 아니다.
        
        ```jsx
        // ❌  statements(not if, switch, for...)
        let numbers = [1, 2, 3]
        function multiply(numbers, multiplier) {
        	for(let i = 0; i < numbers.length; i++) {
        		numbers[i] = numbers[i] * multiplier
        	}
        }
        
        // ✅ expressions
        function multiply(numbers, multiplier) {
        	return numbers.map(num => num * multiply)
        }
        
        ```
        
    4. First-class & height-order functions
        
        함수를 변수에 할당하거나, 함수에 인자로 전달하거나 리턴하는 등의 일들을 할 수 있는 First Class의 특징과 함수 자체를 인자로 전달하거나 함수에서 또 다른 함수를 리턴하는 고차함수, 이 두 가지의 속성을 가지고 있어야 한다.
        
        - First-class
            
            ```jsx
            let numArr = [1, 2, 3, 4]
            const addTwo = a => a + 2
            const multiplyTwo = a => a * 2
            const transform = numbers => numbers.map(addTwo).map(multiplyTwo)
            console.log(transform(numArr))
            ```
            
        - higher-order functions(고차함수)
            
            ```jsx
            const addToppings = topping => food => food + topping
            const egg = addToppings("계란") // 여기서 새로운 함수를 반환
            const becon = addToppings("베이컨")
            
            console.log(egg) // food => food + topping
            console.log(becon) // food => food + topping
            
            const saladWithEgg = egg("샐러드")
            const toastWithBecon = becon("토스트")
            
            console.log(saladWithEgg) // 샐러드계란
            console.log(toastWithBecon) // 토스트베이컨
            ```
            

## 객체/배열에서 왜 `spread` 문법이 필요할까?

spread 문법을 단순히 객체나 배열을 개별 요소로 분해하기 위해 사용할 수 있지만, 원본을 지키면서 배열이나 객체를 복사할 때 아주 유용하게 쓰일 수 있다.

- 기존 객체를 복사하면..
    
    ```jsx
    let objectA = {a: 1, b: 2}
    let objectB = objectA // 한 집에 a와 b가 같이 살게 됨
    
    objectA.a = 100 // 그러니까 얘만 바뀌어도 b도 같이 바뀌게 됨
    
    console.log(objectA) // {a: 100, b: 2}
    console.log(objectB) // {a: 100, b: 2}
    
    // 배열도 마찬가지
    let a = [1, 2, 3]
    let b = a 
    
    a[0] = 100 
    
    console.log(a) // [100, 2, 3]
    console.log(b) // [100, 2, 3]
    ```
    
- spread 문법을 사용한다면?
    
    ```jsx
    let objectA = {a: 1, b: 2}
    let objectB = {...objectA} // objectA를 개별 요소로 분해해서 새로운 객체로 만듦
    
    objectA.a = 100 // 그래서 얘가 바뀌어도 objectB 랑은 상관 없음
    
    console.log(objectA) // {a: 100, b: 2}
    console.log(objectB) // {a: 1, b: 2}
    ```
    

## 객체는 `getter` & `setter` 메서드가 있다.

우리가 일반적으로 사용하던 객체의 프로퍼티는 데이터 프로퍼티였다.

이번엔 객체의 접근자 프로퍼티라고 불리는 새로운 종류의 프로퍼티를 배워보자.

접근자 프로퍼티의 본질은 함수다. 이 함수는 값을 획득(Get) & 설정(Set)하는 역할을 담당하는데, 외부에서는 함수가 아닌 일반 프로퍼티처럼 보인다.

접근자 프로퍼티로 사용하는 메서드를 `getter`, `setter` 라고 표현하고, 실제 사용법은 아래와 같다.

```jsx
let obj = {
  get propName() {
    // getter -> obj.propName을 실행할 때 실행되는 코드
  },

  set propName(value) {
    // setter -> obj.propName = value를 실행할 때 실행되는 코드
  }
};
```

- `getter` 예제
    
    ```jsx
    let user = {
      name: "John",
      surname: "Smith",
      get fullName() {
        return `${this.name} ${this.surname}`;
      }
    };
    console.log(user.fullName); // John Smith
    
    // 만약, getter를 통해 수정하려고 해도 바뀌지 않을 것이다.
    user.fullName = 'lisa'
    
    console.log(user.fullName); // John Smith
    ```
    
- `setter` 예제
    
    ```jsx
    let user = {
      name: "John",
      surname: "Smith",
    
      get fullName() {
        return `${this.name} ${this.surname}`;
      },
    
      set fullName(value) {
        [this.name, this.surname] = value.split(" ");
      }
    };
    
    // 주어진 값을 사용해 set fullName이 실행됨
    user.fullName = "mandoo lisa";
    
    console.log(user.name); // Alice
    console.log(user.surname); // Cooper
    ```
    
- `getter`, `setter` 활용하기
    
    ```jsx
    // _ 로 시작하는 프로퍼티는 객체 내부에서만 활용하고, 외부에서 건드리지 않는 것이 관습
    let user = {
      get name() {
        return this._name;
      },
    
      set name(value) {
    	  // 객체에 저장되는 프로퍼티의 값을 원하는대로 통제할 수 있게 됨
        if (value.length < 4) {
          console.log("입력하신 값이 너무 짧습니다. 네 글자 이상으로 구성된 이름을 입력하세요.");
          return;
        }
        this._name = value;
      }
    };
    
    // 이걸 통해 name은 실제로 user안에 _name에 저장될 것
    user.name = "Pete";
    console.log(user.name); // Pete
    
    user.name = ""; 
    console.log(user.name)
    ```
    

## 객체에는 메서드도 만들 수 있다.

객체의 프로퍼티에 함수를 할당해 객체에게 행동할 수 있는 능력을 부여할 수 있다.

```jsx
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```

이렇게 메서드 추가하면서 객체가 단순히 데이터 저장만 하지 않게된다.

위 메서드를 단축 구문으로 작성하려면 2가지 방법이 있다.

- 방법 1
    
    ```jsx
    user = {
      sayHi: function() {
        console.log("Hello");
      }
    };
    
    user.sayHi();
    ```
    
- 방법 2
    
    ```jsx
    user = {
      sayHi() { // "sayHi: function()"과 동일합니다.
        console.log("Hello");
      }
    };
    ```
    

현업에서의 객체 메서드는 상태 관리, 데이터 조작, API 호출, 이벤트 핸들링 등 다양한 용도로 활용된다.

예를 들어, 쇼핑몰 장바구니 시스템을 구현해야 한다고 해보자.

```jsx
const cart = {
  items: [],
  
  addItem(item) {
    this.items.push(item);
    console.log(`${item}이(가) 장바구니에 추가되었습니다.`);
  },

  removeItem(item) {
    this.items = this.items.filter(i => i !== item);
    console.log(`${item}이(가) 장바구니에서 제거되었습니다.`);
  },

  showCart() {
    console.log("장바구니 목록:", this.items.join(", "));
  }
};

cart.addItem("노트북");
cart.addItem("마우스");
cart.showCart(); // 장바구니 목록: 노트북, 마우스
cart.removeItem("마우스");
cart.showCart(); // 장바구니 목록: 노트북
```

그리고 메서드에서 객체 내부의 값을 변경하고 싶을 때에는 `this`를 사용한다.

```jsx
// 위 예제로 보여준 객체 메서드에서 객체 자신에게 접근할 수 있다.
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타낸다.
    console.log(this.name);
  }

};

user.sayHi(); // John
```

## `this`

`this` 는 런타임에 결정된다. 즉, 대부분의 경우 `this` 의 값은 함수를 호출한 방법에 의해 결정된다.

기본적으로 `this` 는 `window` (전역 객체)이다.

일반 함수 내에서도 혼자 `this`를 선언하면, `window` 객체를 가르킨다.

```jsx
function foo() {
  console.log("foo's this: ",  this);  // window
  function bar() {
    console.log("bar's this: ", this); // window
  }
  bar();
}
foo();
```

하지만 다른 객체에서 호출했다면 `this`가 참조하는 값이 달라진다.

쉽게 말해 `this` 를 사용하는 함수 앞에 점이 있거나, 대과호를 사용한다면 점/대괄호 앞에 있는 것이 `this`가 된다.

```jsx
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  console.log( this.name , this);
}

// 별개의 객체에서 동일한 함수를 사용
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```

## 화살표 함수는 일반 함수와 다르다.

- 가변 인자(arguments)를 받아오는 방법이 다르다.
    
    실제로 인자를 얼만큼 받아올지 모를 때 가변 인자를 사용할 수 있다. 이 때, 가변 인자를 가져오는 방법이 다르다.
    
    - 일반 함수
        
        ```jsx
        function main() {
        	console.log(arguments)
        }
        main(1, 2, 3) // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
        
        main(1, 2, 3, 4, 5) // Arguments(5) [1, 2, 3, 4, 5, callee: ƒ, Symbol(Symbol.iterator): ƒ]
        ```
        
    - 화살표 함수
        
        ```jsx
        const main = (...arguments) => {
        	console.log(arguments)
        }
        main(1, 2, 3) // ✅ [1, 2, 3]
        ```
        
- `this` 의 동작 방식이 다르다.
    - 일반 함수
        
        ```jsx
        const object = {
        	name: 'mandoo',
        	sayHi: function() {
        		console.log("HI : ", this)
        	}
        }
        
        // 여기서 sayHi 함수안의 this는 object가 된다. 점 왼쪽에 object가 있으니까
        object.sayHi(); // HI :  {name: 'mandoo', sayHi: ƒ}
        
        const object2 = {
        	name: '만두',
        	sayHi: object.sayHi, // 여기에 위 object.sayHi를 복사해서 같은 함수를 넣는다.
        }
        
        // 여기서 sayHi의 this는 점 왼쪽의 object2가 된다.
        object2.sayHi();  // HI :  {name: '만두', sayHi: ƒ}
        ```
        
    - 화살표 함수
        
        ```jsx
        const object = {
        	name: 'mandoo',
        	sayHi: function() {
        		console.log("HI : ", this)
        	},
        	sayBye: () => {
        		console.log("Bye : ", this)
        	}
        }
        
        object.sayHi() // HI :  {name: 'mandoo', sayHi: ƒ, sayBye: ƒ}
        object.sayBye() // Bye :  Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
        ```
        
    
    위 코드에서 볼 수 있듯 화살표 함수의 `this` 는 일반 함수와 다르다.
    
    화살표 함수는 일반 함수와는 다르게 자신만의 `this` 를 가지지 않는다.
    
    화살표 함수의 `this` 는 자신을 감싸는 상위 요소를 찾아간다.
    
    위 에제에서는 왜 전역 객체를 가르킬까? 화살표 함수의 상위 요소 `this` 를 확인해보자.
    
    ```jsx
    const object = {
    	name: 'mandoo',
    	sayHi: function() {
    		console.log("HI : ", this)
    	},
    	sayBye: this // this를 값으로 넣어보면 알 수 있다
    }
    
    console.log(object.sayBye) // Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
    ```
    
    여기서 볼 수 있듯 화살표 함수에서의 `this` 는 함수가 선언된 위치에서 `this` 가 결정된다.
    
    이유는 화살표 함수를 감싸는 스코프의 `this` 를 가져와야 하기 때문이다.
    
    즉, 화살표 함수는 자기 자신을 감싸는 스코프의 `this` 를 가져온다.
    
    그렇기에 화살표 함수가 어떻게 호출 되었는지는 중요하지 않다. << 일반 함수와 다름
    
    함수가 선언된 위치에서 `this` 가 결정되고 변하지 않는다.
    
    → 때문에 화살표 함수를 객체의 메서드로 사용하는 것은 좋지 않은 방법
    

조금 더 심화된 내용을 살펴보자.

아래 코드의 `innerFunction` 의 `this` 는 왜 전역 객체를 가르킬까?

함수가 호출될 때 앞에 아무것도 없이 함수 혼자 호출되었다.

일반 함수에서의 `this`는 함수가 호출될 때 결정된다. 즉, 진짜 `this` 가 쓰이는 함수가 호출될 때 결정된다는 것이다.

```jsx
const object = {
	name: 'mandoo',
	sayHi: function() {
		console.log(this) // {name: 'mandoo', sayHi: ƒ} -> 여기는 object가 앞에 붙었기 때문
		const innerFunction = function(){
			console.log(this) // Window
		}
		innerFunction(); // 여기서 함수가 호출될때 앞에 아무것도 없이 혼자 호출되었기 때문!
	}
}
object.sayHi()
```

그럼 화살표 함수로 코드를 짜면 어떻게 될까?

화살표 함수가 선언된 위치를 감싸고 있는 스코프가 가르키는 `this` 를 따라갈 것이다.

```jsx
const object = {
	name: 'mandoo',
	sayHi: function() {
		console.log(this) // {name: 'mandoo', sayHi: ƒ} -> 여기는 object가 앞에 붙었기 때문
		const innerFunction = () => {
			console.log(this) // {name: 'mandoo', sayHi: ƒ} 
		}
		innerFunction(); // 이 함수를 감싸고 있는 스코프는 sayHi 함수, 그리고 이 함수의 this는 객체
	}
}
object.sayHi()
```

## `bind()`

다른 객체로 `this` 를 정하고 싶을 때 사용할 수 있다.

```jsx
const object = {
	name: 'mandoo',
	sayHi: function() {
		console.log(this) // {name: 'mandoo', sayHi: ƒ}
		
		// bind를 사용하여 함수를 어떻게 호출했던지 상관없이 this를 개발자가 바꿔줄 수 있음
		const innerFunction = function(){
			console.log(this) // {newKey: 'newValue'}
		}.bind({newKey: 'newValue'})
		
		innerFunction(); 
	}
}
object.sayHi()
```

하지만 화살표 함수를 사용하면 불가능하다.

화살표 함수는 `bind` 를 해줄 자신만의 `this` 를 갖고 있지 않기 때문이다.

```jsx
const object = {
	name: 'mandoo',
	sayHi: function() {
		console.log(this) // {name: 'mandoo', sayHi: ƒ}
		
		// bind를 써도 여전히 바뀌지 않음
		// 화살표 함수가 정의된 위치를 감싸는 스코프를 따라 this가 결정되면 변하지 않기 때문!
		const innerFunction = (() => {
			console.log(this) // {name: 'mandoo', sayHi: ƒ}
		}).bind({newKey: 'newValue'})
		
		innerFunction(); 
	}
}
object.sayHi()
```

## 고차 함수 (Higher-Order FUnctions)

함수를 인자로 받거나, 함수를 반환하는 함수이다.

함수형 프로그래밍을 있게 해준 녀석이라고 볼 수 있다.

기본적으로 고차 함수는 이렇게 만들 수 있다.

1. 함수를 인자로 받을 때
    
    ```jsx
    // 기본 사용법
    function 함수명(인자로넘겨받는함수) {
    	인자로넘겨받는함수()
    }
    
    // 예시
    const fruits = ['사과', '바나나', '딸기'];
    
    function customForEach(array, func) {
    	for(let i = 0; i < array.length; i++) {
    		func(array[i])
    	}
    }
    
    customForEach(fruits, (fruit) => console.log(`${fruit}는 맛있어요!`));
    
    // result:
    // 사과는 맛있어요!
    // 바나나는 맛있어요!
    // 딸기는 맛있어요!
    ```
    
2. 함수를 반환할 때
    
    ```jsx
    // 기본 사용법
    function 함수() {
    	return function 반환하는함수() {
    		// 코드
    	};
    }
    
    // 예시
    function addToppings(topping) {
    	return function (food) {
    		return `${topping} 토핑이 올라간 ${food}`
    	}
    }
    
    const addStrawberry = addToppings("딸기")
    const addCookies = addToppings("쿠키")
    
    const finalFood1 = addStrawberry("생크림 케이크")
    const finalFood2 = addCookies("요거트 아이스크림")
    
    console.log(finalFood1) // 딸기 토핑이 올라간 생크림 케이크
    console.log(finalFood2) // 쿠키 토핑이 올라간 요거트 아이스크림
    ```
    

## Module, 모듈 시스템

코드를 여러 파일로 나누어 관리할 수 있다.

```jsx
// math.js - 수학 관련 함수들
export const 더하기 = (a, b) => a + b
export const 빼기 = (a, b) => a - b
export const PI = 3.14159;

// utils.js - 유틸리티 함수들
export default function 포맷날짜(date) {
    return date.toLocaleDateString();
}

// main.js - 메인 파일
import { 더하기, 빼기, PI } from './math.js';
import 포맷날짜 from './utils.js';

// 모든 것을 한번에 가져오기
import * as MathUtils from './math.js';

// 실제 사용
console.log(더하기(5, 3));  // 8
console.log(MathUtils.PI);   // 3.14159
```

혹은 `export`를 한 번에 해도 된다.

```jsx
// 혹은 export를 한번에 해도 됩니다.

// say.js (모듈 만드는 곳)
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}; // 두 함수를 내보냄

// main.js (사용하는 곳)
import {sayHi, sayBye} from './say.js';

sayHi('John'); // Hello, John!
sayBye('John'); // Bye, John!
```