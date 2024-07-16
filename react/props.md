# props

> props는 부모 component가 자식 component에게 전달하는 객체이다.

즉, props를 이용하여 부모에서 자식으로 값을 전달할 수 있다.

---

## 이해

1. 개념

   props는 properties(속성)를 줄인 말이다.

   props는 객체 형태로 전달된다. props는 함수형 component에서는 함수의 매개변수로, 클래스형 component에서는 `this.props`로 접근할 수 있다. 이러한 props는 component간 데이터의 공유를 더 쉽게 하여 component의 효용성을 더 높인다.

2. 데이터의 방향성

   react는 데이터의 흐름이 단방향이므로 무조건 부모 component에서 자식 component로 props가 전달되며, 자식 component는 전달받은 props 데이터를 직접 수정할 수 없다.

   이 때 자식 component에서 부모 component의 상태를 변경하고 싶다면, callback 함수를 props로 전달하여 사용할 수 있다.

---

## 문법

```javascript
import React from "react";

function Example(props) {
  return (
    <div>
      <p>data: {props.data}</p>
    </div>
  );
}

export default Example;
```

```javascript
import React from "react";
import Example from "./Example.jsx";

function App() {
  return (
    <div>
      <Example data="im properties" />
    </div>
  );
}

export default App;
```
