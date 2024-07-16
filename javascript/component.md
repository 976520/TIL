# 리액트의 시작과 끝

> Component는 React Application을 이루는 최소한의 단위이다.

---

## 이해

1. 개념

   component는 react에서 재사용이 가능한 독립된 모듈을 뜻한다. 여러 UI를 구성할 때 같은 기능을 가진 부분을 반복적으로 만드는 대신 만들어진 component를 조합하여 더 예쁜 코드를 만들 수 있다.

---

## 문법

1. component 종류

   component를 정의하는 두 방법이 있다.

   1. 함수형

      일반 javascript 함수와 동일한 형태를 가지므로 구분을 위해 함수명을 항상 대문자로 시작해야 한다. 함수와 비슷하게 `return` 아래의 코드는 무시된다.

      이 방법이 후술할 클래스형보다 더 간단해서 자주 쓰인다.

      ```javascript
      function Example() {
        return <div>Hello, world!</div>;
      }
      ```

   2. 클래스형

      component의 구성 요소에 더불어 react의 생명주기를 모두 포함하고 있다. 이러한 생명주기 메소드가 필요한 구조의 component를 만들 때 사용한다.

      클래스형에서는 `render()` 메서드를 사용하여 JSX를 반환한다.

      ```javascript
      class Example extends Component {
        render() {
          return <div>Hello, world!</div>;
        }
      }
      ```

2. `export`

   component를 정의한 후 `export`를 통해 내보냄으로써 다른 파일에서 `import`하여 component를 사용할 수 있게끔 할 수 있다.

   ```javascript
   export default Example;
   ```

3. `import`

   `export` 한 component를 `import`를 이용하여 재사용할 수 있다.

   다음 코드에서는 앞서 `export` 한 component를 `import`하여 component 함수 안에서 재사용하고, 그 component를 다시 `export` 하여 다른 파일에서 불러올 수 있도록 하였다.

   ```javascript
   import Example from "./example";

   function App() {
     return (
       <div>
         <Example />
         <Example />
       </div>
     );
   }

   export default App;
   ```

---
