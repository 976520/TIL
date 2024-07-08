## useCallback

1. 정의

   `useCallback`은 `useMemo`와 유사하게 최적화가 필요한 상황에서 쓰인다. 그러나 useMemo는 특정 결과값을 재사용 할 때 사용했던 반면, `useCallback`은 특정 함수를 재사용하고 싶을 때 사용한다.

2. 문법

   `useCallback`의 기본형은 다음과 같다.

   ```jsx
   const cachedFn = useCallback(function, deps)
   ```

   이 역시 `useEffect`와 동일하게 첫번째 인자로 콜백 함수, 두번째 인자로 의존성 배열을 받는다. `useMemo`에서는 콜백 함수의 리턴값을 memoization 했다면, `useCallback`은 콜백 함수 자체를 memoization 한다.

3. 사용

   아래 코드는 `useCallback`을 통해 전달되는 콜백 함수가 동일한 참조를 유지한다. 함수가 변경되지 않으면 props를 전달받는 하위 컴포넌트도 재렌더링을 하지 않기 때문에 함수의 memoization을 통해 최적화하였다고 볼 수 있다.

   ```jsx
   function ChildComponent({ onClick }) {
     return <button onClick={onClick}>Increment</button>;
   }

   function ParentComponent() {
     const [count, setCount] = useState(0);
     const [text, setText] = useState("");

     const handleClick = useCallback(() => {
       setCount((prevCount) => prevCount + 1);
     }, []);

     const handleTextChange = (event) => {
       setText(event.target.value);
     };

     return (
       <div>
         <p>Count: {count}</p>
         <ChildComponent onClick={handleClick} />
         <input type="text" value={text} onChange={handleTextChange} />
       </div>
     );
   }
   ```

---
