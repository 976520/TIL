## useEffect

1. 이해

   `useEffect`는 컴포넌트가 mount됐을 때, unmount됐을 때, 그리고 update됐을 때 특정 작업을 처리시키는 hook이다.

1. 문법

   `useEffect`의 기본형은 다음과 같다.

   ```jsx
   useEffect(function, deps)
   ```

   `function`은 실행하고자 하는 작업이다. `deps`는 배열 형태로, 의존성 배열이라고 한다.

   의존성 배열을 비워두면 컴포넌트가 mount될 때, 즉 가장 처음 렌더링 될 때만 `function`을 실행하고, 배열 자체를 생략하면 렌더링 될 때마다 실행한다. 또한 배열 안에 어떠한 값을 넣으면 그 값이 바뀔 때 실행한다.

1. 사용

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
