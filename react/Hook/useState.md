## useState

1. 정의

   `useState`는 가장 기본적인 Hook으로, 함수형 컴포넌트에서도 가변적인 상태를 가질 수 있게 해준다.

2. 문법

   `useState`의 기본형은 다음과 같다.

   ```jsx
   const [state, setState] = useState(initialState);
   ```

   `useState`를 통해 상태 변수 `state`를 선언한 모습이다. 여기서 `useState`의 파라미터 `initialState`가 `state`의 초기값이며, `setState` 함수를 통해 `state`를 다른 값으로 업데이트 할 수 있다.

   보통 업데이트 함수명은 `set+<상태변수명>` 으로 작성한다.

3. 사용

   다음은 count라는 상태 변수를 선언하고 그 초기값을 0으로 설정하였으며, 버튼을 클릭할 때 마다 count 변수를 증가시키는 코드이다.

   ```jsx
   const [count, setCount] = React.useState(0);

   const increment = () => {
     setCount(count + 1);
   };

   return (
     <div>
       <h1>{count}</h1>
       <button onClick={increment}>click!</button>
     </div>
   );
   ```

   이처럼 `useState` Hook의 파라미터의 값이 상태의 기본값이다. 앞선 예제에서는 파라미터에 0을 넣었는데, 결국 count의 기본값을 0으로 설정하겠다는 의미이다.

---
