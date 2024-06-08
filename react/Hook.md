# 원 투 훅

> Hook은 함수형 컴포넌트에서 할 수 없었던 다양한 작업을 할 수 있게 한다.

이 페이지에서는 hook의 몇가지 종류를 설명한다.

---

## useState

1. 정의

   `useState`는 가장 기본적인 Hook으로, 함수형 컴포넌트에서도 **가변적인 상태를 가질 수 있게** 해준다.

2. 문법

   `useState`의 기본형은 다음과 같다.

   ```jsx
   const [state, setState] = useState(initialState);
   ```

   `useState`를 통해 상태 변수 `state`를 선언한 모습이다. 여기서 `useState`의 파라미터 `initialState`가 `state`의 초기값이며, `setState` 함수를 통해 `state`를 다른 값으로 업데이트 할 수 있다.

   보통 업데이트 함수명은 `set+<상태변수명>` 으로 작성한다.

3. 예제

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

## useEffect

1. 정의

   `useEffect`는 컴포넌트가 **mount됐을 때, unmount됐을 때, 그리고 update됐을 때 특정 작업을 처리**시키는 hook이다.

1. 문법

   `useEffect`의 기본형은 다음과 같다.

   ```jsx
   useEffect(function, deps)
   ```

   `function`은 실행하고자 하는 작업이다. `deps`는 배열 형태로, **의존성 배열**이라고 한다.

   의존성 배열을 비워두면 컴포넌트가 mount될 때, 즉 가장 처음 렌더링 될 때만 `function`을 실행하고, 배열 자체를 생략하면 렌더링 될 때마다 실행한다. 또한 배열 안에 어떠한 값을 넣으면 그 값이 바뀔 때 실행한다.

1. 예제

   다음은 useEffect를 이용하여 1초마다 count 값을 증가시키는 함수이다. 의존성 배열이 비어 있으므로, 이 컴포넌트가 처음 mount될 때 실행된다.

   ```jsx
   const [count, setCount] = useState(0);

   useEffect(() => {
     const timer = setInterval(() => {
       setCount((prevCount) => prevCount + 1);
     }, 1000);
     return () => {
       clearInterval(timer);
     };
   }, []);

   return (
     <div>
       <h1>{count}</h1>
     </div>
   );
   ```

   `setInterval()`은 콤마를 기준으로 앞에 있는 함수를 뒤에 있는 시간마다 반복 호출하는 함수이다. 이 코드에서는 `setInterval()`을 이용해 1000ms 마다 타이머를 증가시키고 있다.

   이때 `useEffect`의 반환값이 클린업 함수이다. 이 함수는 컴포넌트가 unmount될 때, 또는 다음 `useEffect` 실행 전에 실행된다. 이 코드에서는 클린업 함수에서 `clearInterval()`를 호출하여 timer를 정리함으로써 메모리 누수를 방지한다.

---
