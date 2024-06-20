## useRef

1. 정의

   `useRef`의 ref는 reference(참조)의 약자로, 렌더링에 필요하지 않은 값을 참조할 수 있는 Hook이다.
   state와 달리 값이 변화해도 렌더링을 발생시키지 않으며, 일반 변수와 달리 이 값을 아무리 렌더링이 되어도 언마운트 전까지 값을 계속 유지한다. 이러한 장점 때문에 useRef를 변수처럼 저장공간으로 쓰기도 한다.
   
   `useRef`를 DOM요소에 접근하기 위한 수단으로 쓰기도 한다.

1. 문법
   
   `useRef`의 선언은 다음과 같다.
   
    ```jsx
    const ref = useRef(initialValue)
    ```
    
    컴포넌트의 최상위 레벨에서 호출하면 `ref` 오브젝트를 반환하며, 이때 `initialValue`는 ref객체의 초기값이다.
   `useRef`의 값에 접근하기 위해서는 `ref.current`를 사용한다.

1. 사용
   
    다음은 `useRef`를 활용하여 버튼을 클릭하면 입력 필드에 포커스가 이동시키는 함수이다.
    ```jsx
    const inputRef = useRef(null);
  
    const focus = () => {
      inputRef.current.focus();
    };
  
    return (
      <div>
        <input ref={inputRef} type="text"/>
        <button onClick={focus}></button>
      </div>
    );
    ```
    input 요소의 ref 속성에 `inputRef`를 할당하여 `input`요소를 참조할 수 있게 하였다. 버튼을 클릭할 시 `inputRef.current.focus()`를 호출하여 input 요소에 포커스가 가도록 한다.
  
---
