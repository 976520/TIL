# 손모가지 걸고 약속~

> Promise 객체는 비동기 작업의 상태 정보를 가진 객체이다.

따라서 Promise 객체를 보면 작업이 성공했는지, 실패했는지 알 수 있다.

---

## 개념

1. 정의

   Promise 객체는 비동기 작업의 최종

2. 상태

   Promise 객체는 다음 세 상태가 존재한다.

   1. **Pending**(대기)

      처리가 완료되지 않은, 진행 중인 상태이다.

   2. **Fulfilled**(이행)

      작업이 성공적으로 완료되었음을 나타내며, fulfilled 상태가 될 시 작업의 성공 결과에 관한 정보를 같이 갖게 된다.

   3. **Rejected**(거부)

      작업이 실패했음을 나타내며, rejected 상태가 될 시 작업의 실패 이유에 관한 정보를 함께 가지게 된다.

3. 장점

---

## 문법

1. 생성

   ```javascript
   function prom() {
     return new Promise((resolve, reject) => {
       if (/* 성공 조건 */) {
         resolve(/* 결과 값 */);
       } else {
         reject(/* 에러 값 */);
       }
     });
   }
   ```

   promise 객체의 생성은 `new`와 promise 생성자 함수를 이용한다. 이때 생성자 함수는 두 개의 매개 변수를 가진 콜백 함수를 넣게 되는데, 첫 번째 인수는 작업이 성공했을 때 성공(resolve)임을 알려주는 객체이며, 두 번째 인수는 작업이 실패했을 때 실패(reject)임을 알려주는 오류 객체이다.
   또한 이 콜백 함수를 executor라고 한다.

2. 처리

   만들어진 promise 객체는 비동기 작업이 완료된 후의 다음 작업을 연결시켜 진행할 수 있다.

   메서드 chaining을 통해 작업 결과에 따라 후속 처리를 진행한다. chaining이란, 다음과 같은 handler를 연달아 연결하는 것이다.

   1. then

      ```javascript
      prom().then((result) => {
        // 성공 시 실행
      });
      ```

      `.then` 메서드는 처리가 이행(fulfilled)되어 promise 객체에서 `resolve()` 를 호출하게 되면, 콜백 함수를 등록하고, 새로운 promise를 반환한다. 이때 호출한 `resolve()`의 매개변수가 `.then` 매서드의 콜백 함수 인자로 들어가 `.then`내부에서 프로미스 객체 내부에서 처리한 값을 사용할 수 있다.

   2. catch

      ```javascript
      prom().catch((error) => {
        // 실패 시 실행
      });
      ```

      `.then`과 반대로 `.catch`는 처리가 거부(rejected)되어 promise 객체에서 `reject()`를 호출하게 되면 이어져, 실패에 대한 추가 처리를 `.then`과 동일한 방식으로 진행한다.

   3. finally

      ```javascript
      prom().finally(() => {
        // 성공과 실패에 관련없이 실행
      });
      ```

      `.finally`는 결과에 관련 없이 실행할 콜백 함수를 등록하고, 새로운 promise를 반환한다.
