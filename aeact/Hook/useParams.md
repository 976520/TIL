## useParams

1. 이해

   `useParams`는 react router 사용 시 파라미터 정보를 사용해야 할 때 사용한다.

2. 문법

   `useParams`의 기본형은 다음과 같다.

   ```jsx
   const params = useParams();
   ```

   다음과 같은 URL에서,

   > https://url/pathname/parameter

   parameter 부분을 파라미터라고 한다.

   `useParams`를 이용하면 현재 페이지의 파라미터를 알 수 있다.

3. 사용

   ```jsx
   let { params } = useParams();

   return (
     <div className="test">
       <p>parameter is {params}</p>
     </div>
   );
   ```
