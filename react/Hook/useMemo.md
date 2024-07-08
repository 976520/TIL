## useMemo

1. 정의

   `useMemo`는 컴포넌트의 성능을 최적화 시키기 위한 hook이다. 이때 Memo는 memoization의 약자이며, 이의 의미는 다음과 같다.

   > 계산의 결과를 메모리에 저장했다가 꺼내 씀으로써 중복 계산을 방지하는 기법이다.

   즉, 동일한 값을 반환하는 함수를 반복적으로 호출해야 할 때, **처음 계산 시 해당 값을 메모리에 저장해서 필요할 때마다 재사용**하는 것이다.

2. 문법

   `useMemo` 의 기본형은 다음과 같다.

   ```jsx
   const cachedValue = useMemo(calculateValue, deps);
   ```

   `useMemo`는 `useEffect`처럼 첫 번째 인자로 콜백 함수, 두 번째 인자로 의존성 배열을 받는다. 의존성 배열의 사용은 `useEffect`와 동일하며, 마운트 될 때에만 값을 계산하고 그 이후론 계속 memoization 된 값을 꺼내와 사용한다는 차이가 있다.

3. 사용

   아래 코드에서는 `useMemo`를 사용하여 num이 변경될 때만 계산을 진행한다. 당연히 이전 값은 memoization되어 불필요한 재계산을 방지한다.

   ```jsx
   function FibonacciComponent() {
     const [num, setNum] = useState(0);

     const fibValue = useMemo(() => {
       const fibonacci = (n) => {
         if (n <= 1) return n;
         return fibonacci(n - 1) + fibonacci(n - 2);
       };
       return fibonacci(num);
     }, [num]);

     return (
       <div>
         <p>
           fibonacci of {num}: {fibValue}
         </p>
         <button onClick={() => setNum(num + 1)}>next</button>
       </div>
     );
   }
   ```

---
