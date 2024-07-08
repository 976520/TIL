# async, await

> async와 await는 자바스크립트의 비동기 처리 방식 중 하나이다.

---

## 개념

1. 정의

   `async`가 붙은 함수는 promise를 반환하며 그 안에서~~만~~ `await` 키워드를 사용할 수 있다.

   promise 앞에 `await`를 붙이면 그 promise가 처리될 때 까지 코드 실행을 일시적으로 정지한다. 처리가 완료될 시, 오류가 발생하지 않았다면 promise 객체의 결과값을 return한다.

   `async`와 `await`를 사용하면 비동기 코드를 동기 코드처럼 작성할 수 있으므로 가독성이 좋아지고 에러 처리가 간단해진다.

2. 오류

   만약 처리가 완료된 시점에서 오류가 발생하였다면, 예외가 생성된다. 이 예외는 `throw error`를 호출한 것과 동일하며, `try-catch`를 통해 감지할 수 있다. `try-catch`가 없다면 `async` 함수를 호출하여 생긴 promise가 rejected 상태가 된다.

   `async` 함수에 `.catch`를 추가하여 rejected 상태인 promise를 처리할 수 있다.

---

## 사용

1. api 통신

   [promise](https://github.com/976520/TIL/blob/main/javascript/promise.md)를 쓸 때와, [axios](https://github.com/976520/TIL/blob/main/javascript/axios.md)를 쓸 때와 비교하는 것이 중요하다.

   ```javascript
   async function example() {
     try {
       const data = await fetch(url);
       return await data.json();
     } catch (error) {
       throw error;
     }
   }
   ```
