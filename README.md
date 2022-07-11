## 7월 9일 토요일

- Redux 연습을 위한 repository

- # intro

store를 이용한 상태관리 라이브러리인 리덕스에 대해서 알아보자

리덕스의 정의

- 리덕스는 자바스크립트 앱에서 예측가능한 상태관리를 해주는 컨테이너
- 그러면 상태라고하는 state는 무엇일까
  - 리액트에서 this.state 이라고 썼던 것 처럼
  - 리액트의 state는 컴포넌트 내에서 관리를 한다 그 state 안에 앱에서 필요한 상태들을 담아두는 공간이었다

그렇다면 각 컴포넌트에서 이 state에 접근해서 사용해야하는 경우가 발생

- 자식컴포넌트 1에서 2에 데이터를 전달해주기 위해서는 부모컴포넌트의 state에 그 데이터를 담아놓고 자식컴포넌트1이 부모컴포넌트에게 데이터를 올려주고
- 부모컴포넌트가 자식컴포넌트2에게 데이터를 내려주는 방식으로 전달을 해줘야한다.
- 자식끼리 다이렉트로 데이터 전달은 불가능

구조가 단순하면 괜찮지만, 만약 자식컴포넌트가 많아진다면, 상태관리가 복잡해진다.

- 거쳐야할 컴포넌트가 많아지기 때문
- 이런 복잡성을 줄이기 위해 상태를 관리해주는 라이브러리인 리덕스를 사용할 수 있다.

### Redux 의 세가지 원칙

### 1. Store

Single source of truth - 동일한 데이터는 항상 같은 곳에서 데이터를 가져온다.

- 데이터를 저장하는 store 라는 하나뿐인 공간이 있다

```jsx
store 는 상태가 관리되는 오직 하나의 공간.
컴포넌트들과 별개로 store라는 공간이 있어서 store안에 앱에서 필요한 state를 두고 컴포넌트들에서 state 정보가 필요할 때 store에 접근을 해서 state 정보를 가져올 수 있다.
```

### 2. Action

State is read-only - React에서도 state를 변경하기 위해서는 반드시 setState 라는 메서드를 활용해야만 변화가 가능했다.

- Redux에서는 Action 이라는 객체를 통해서 state를 변경할 수 있다.

```jsx
Action은 자바스크립트 객체이다. 그 객체 안에 type을 비롯한 다양한 데이터들이 담긴다. 이 Action 객체는 store에게 우리 application 데이터를 운반을 해주는 역할을 한다.

{
	type: "ORDER",
	drink: {
		menu: "icedTea",
		size: "Tall",
		iced: true
	}
}

이런 정보를 객체 안에 담아준다.

```

### 3. Reducer

Changes are made with pure functions - 변경은 순수함수로만 가능하다

- Reducer 와 연결되는 부분이다.
- 현재 상태와 Action 을 이용해 다음 상태를 만들어 냄

Action Dispatch → Reducer → store(New State)

<aside>
💡 Action 객체는 Dispatch 에게 전달되고, Dispatch는 Reducer 를 호출해서 새로운 state 생성

</aside>

# 7월 11일 월요일

### class 컴포넌트와 function 컴포넌트의 차이점

- class 컴포넌트는 this.state로 상태를 가질 수 있다.
- 하지만 function 컴포넌트는 state를 가지지 못했다

  - 그리고 이 state를 가지고 있음으로 인해서 class 컴포넌트에서는 life cycle이라는 것을 가질 수 있었는데,
  - function 컴포넌트엣서는 그렇지 못했다
  - 그래서 function 컴포넌트에서 state, life cycle을 가질 수 있는 방법이 등장
  - 바로 `React Hooks`

- 상태를 가지러면 react hooks에서 useState 라는 hooks를 통해서 상태를 가질 수 있다
- 그리고 useEffect 를 통해서 lifeCycle 도 가질 수 있게 되었다.

### useState

- state 제공

```jsx
const [count, setCount] = useState(0);
```

- count라는 상태를 가지고 있고, count를 변경할 수 있는 메소드가 setCount이다.

### useEffect

- lifeCycle 제공

- useEffect를 통해 life cycle을 흉내낼 수 있다.

  - componentDidMount
  - componentDidUpdate

- 의존성 배열 (dependency Array)

  - 두번째 인자에 [] 빈 배열을 넣어주면 componentDidUpdate처럼 컴포넌트가 mount되면 useEffect안에 정의된 함수가 실행
  - 만약에 인자를 아무것도 넘겨주지 않으면 매 리렌더링마다 실행이된다.

- 특정 컴포넌트가 update 됐을 때 그때에 따라서 상태(함수)를 실행시키고 싶다고하면, [] 의존성 배열 안에
- 내가 지켜볼 상태 (변화를 감지할 상태)를 입력하면 해당 값이 변하면 useEffect 안에 있는 코드가 실행이 되도록 update 가능

## redux method

### useSelector

- 전역에 있는 상태를 component에 가지고와서 사용을 할 때 사용하는 메소드
- useSelector를 이용해서 Redux의 store 상태를 가져오니까 바로 접근 할 수 있다.
  - component ------------ useSelector ------------ state

### useDispatch

- 전역의 상태를 변경하기 위해서 Action 객체를 reducer에게 전달을 할 때 쓰는 메소드
  - Action ------------- useDispatch ---------------- Reducer

## redux 가 왜 필요한가

- useState를 기존에 쓴 방식은 결국 컴포넌트 안에서 그리고 해당 컴포넌트에 딸린 자식 컴포넌트에서만 유효한 상태 였다.
- 그래서 한 컴포넌트에 상태를 가지고 있다가 다른 컴포넌트에게 물려주려면, props로 전달을 해줘야했다.
- 그런데 redux에서는 상태를 컴포넌트가 가지고 있는게 아니라 리덕스 상의 store라는 공간에서 전역으로 state를 관리할 수가 있게 된다.

## 데이터의 흐름

- 데이터가 어떻게 흐르는지가 이해하는데 어려움이 있다.
- Redux에서 구성요소들 ( action, reducer, store, view)의 데이터 흐름이 어떤 순서로 이루어 지는가?
  - `data는 단방향으로 흐른다`

view -> Action -> Reducer -> store
^
ㄴ <--------------------------

- 리액트에서는 view를 통해서 Action이 일어나게되면, 그 Action은 dispatch를 통해서 reducer로 전달이되고, 그 reducer에서는 새로운 상태를 만들어내서
- store를 update 시킨다.
- 그리고 update된 상태는 view를 다시 렌더링 시킨다.
- 이런식으로 데이터가 단방향으로 흐르는 구조이다.
