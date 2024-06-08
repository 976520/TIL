# React

태그: React

# 반응하다.

> React는 메타에서 개발한 프론트엔드 프레임워크이며, 오픈 소스 Javascirpt 라이브러리이다.
> 

---

## React 특징

1. Virtual DOM
    
    [DOM](https://www.notion.so/DOM-8a3c4aea8db44552a9cd9b1ce88b6ab1?pvs=21) 
    
2. 컴포넌트(Component) 구조
    
    React 개발의 가장 큰 특징은 페이지가 아닌, 특정 기능을 수항하는 독립적인 단위인 컴포넌트로 시작한다는 것이다. 기획자나 디자이너로부터 앱을 전달받으면, 먼저 컴포넌트로 나누어 각각의 컴포넌트를 개발하고 조립하여 복잡한 UI를 구성한다.
    
    이로 인한 장점은 당연히 앱이 컴포넌트 더 세세히 분할되어 있기 때문에, 전체 코드를 파악하기 쉽고 유지보수에 용이하다는 것이다.
    
3. 단방향 바인딩
    
    각 컴포넌트는 state를 가진 부모 컴포넌트에서 props를 이용해 데이터를 마치 arguments(인자) 혹은 attributes(속성)처럼 전달받을 수 있다. 즉, 데이터 전달의 주체는 부모 컴포넌트이며, 데이터가 부모에서 자식으로 전달됨을 의미한다. 자식 컴포넌트는 props를 변경할 수 없으며 오직 부모 컴포넌트만이 그의 상태를 변경할 수 있다.
    
    Vue와 Angular는 양방향 바인딩을 한다. 양방향 바인딩은 데이터의 변경과 UI의 상태 변경이 서로 영향을 주며 동시에 업데이트 하는 것이다. 때문에 UI가 복잡해지면 성능이 저하된다는 단점이 있다.
    
    하지만 React는 데이터의 흐름이 한 방향으로 유지되는 단방향 바인딩을 한다. 이러한 단방향 바인딩의 경우 앱의 상태가 어디서 관리되고 있는지를 명확하게 해 주어 데이터의 흐름을 예측하여 디버깅하기 쉽다는 장점이 있다.
    

---

## React 문법

> Javascript Syntax eXtension은 이름과 같이 Javascript를 확장한 것이다.
> 

React는 기본적으로 JSX 문법을 사용한다. 이는 JS 코드 안에 HTML과 유사한 문법을 통해 UI구조를 작성할 수 있다는 특징이 있다.

```jsx
const App = () => {
	const name = 'React';
  return (
    <div className="container">
      <h1>Hello, {name}!</h1>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

render()는 데이터를 입력받아 화면에 표시할 내용을 반환하는 역할을 한다. 위와 같은 코드에서는 App 함수의 내용을 HTML 안의 ‘root’라는 ID를 가진 element에 반환한다.

JSX 내부에서 코드를 중괄호로 감싸므로써 JS 표현식을 작성할 수 있다.

또한 class를 className 이라고 해야한다.

---