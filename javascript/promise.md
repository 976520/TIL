# 손모가지 걸고 약속~

> promise 객체는 비동기 작업의 상태 정보를 가진 객체이다.

---

## 개념

1. 정의

   promise 객체는 비동기 작업의 최종 결과를 저장하는 객체이다. 따라서 promise 객체를 보면 작업이 성공했는지, 실패했는지 알 수 있다.

2. 상태

   promise 객체는 다음 세 상태가 존재한다.

   1. **Pending**(대기)

      처리가 완료되지 않은, 진행 중인 상태이다. 이 상태에서 후술할 두 상태로 한 번 변경될 시, 다시 다른 상태를 가질 수 없다.

   2. **Fulfilled**(이행)

      작업이 성공적으로 완료되었음을 나타내며, fulfilled 상태가 될 시 작업의 성공 결과에 관한 정보를 같이 갖게 된다.

   3. **Rejected**(거부)

      작업이 실패했음을 나타내며, rejected 상태가 될 시 작업의 실패 이유에 관한 정보를 함께 가지게 된다.

3. 특징

   비동기 작업을 순차적으로 실행할 수 있다. 그러나 비동기적 처리가 완벽히 가능하게 해주는 것은 아니며, 단지 보기 쉽게 만들어주는 것 뿐이다. [callback 함수](https://github.com/976520/TIL/blob/main/javascript/callback.md)가 많아지면 '콜백 지옥'에 빠져 가독성이 구려지게 된다. 이를 개선하기 위해 promise를 사용한다.

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

      `.then`메서드는 **처리가 이행(fulfilled)되어 promise 객체에서 `resolve()` 를 호출**하게 되면, 콜백 함수를 등록하고, 새로운 promise를 반환한다. 이때 호출한 `resolve()`의 매개변수가 `.then` 매서드의 콜백 함수 인자로 들어가 `.then`내부에서 프로미스 객체 내부에서 처리한 값을 사용할 수 있다.

   2. catch

      ```javascript
      prom().catch((error) => {
        // 실패 시 실행
      });
      ```

      `.then`과 반대로 `.catch`는 **처리가 거부(rejected)되어 promise 객체에서 `reject()`를 호출**하게 되면 이어져, 실패에 대한 추가 처리를 `.then`과 동일한 방식으로 진행한다.

   3. finally

      ```javascript
      prom().finally(() => {
        // 성공과 실패에 관련없이 실행
      });
      ```

      `.finally`는 **결과에 관련 없이** 실행할 콜백 함수를 등록하고, 새로운 promise를 반환한다.

   4. all

      ```javascript
      prom()
        .all([x, y, z])
        .then((result) => {
          // x, y, z가 모두 성공했을 때 실행
        }.catch((error)=>{
          // x, y, z 중 하나라도 실패했을 때 실행
        }));
      ```

      `.all`메서드도 `.then`처럼 새로운 promise 객체를 리턴하며, **인자로 들어온 배열 안에 있는 모든 promise 객체가 fulfilled 상태**가 될 때 까지 기다린다.

      모든 객체들이 fulfilled 상태가 될 시, `.all`이 반환했던 promise 객체는 fulfilled 상태가 된다. 이때 **작업 결과로 각 promise 객체의 작업 결과로 이루어진 배열**을 갖는다.

      단, 하나의 객체라도 rejected 상태가 되는 경우, 전체 작업이 실패한 것으로 간주한다. 이에 따라 `.all`의 promise 객체는 rejected 상태가 되며, 작업 실패 정보를 갖는다.

   5. race

      ```javascript
      prom()
        .all([x, y, z])
        .then((result) => {
          // x, y, z 중 먼저 작업이 완료된 객체가 작업을 성공했다면 실행
        }.catch((error)=>{
          // x, y, z 중 먼저 작업이 완료된 객체가 작업을 실패했다면 실행
        }));
      ```

      `.race`매서드도 `.all`과 같이 인자로 배열을 받으며, 이때 `.race`는 배열에서 가장 먼저 pending 상태를 벗어난 promise 객체와 동일한 상태, 결과를 가진다. 다른 말로 **가장 먼저 fulfilled 혹은 rejected 로 상태가 결정된 객체를 선택**한다.

   이렇게 chaining이 가능한 이유는 handler에서 값을 return하면 그 반환값은 자동으로 promise 객체로 감싸져 다음 handler가 그것을 받게 되기 때문이다.

   만약 `.catch` handler 다음으로 `.then`이 이어져 있으면, 가까운 `.then`으로 제어 흐름이 넘어가 처리가 이어진다.

   이러한 promise의 구조는 callback과 비슷한 문제를 일으킬 수 있다. 단적인 예시로, `.then` chain을 길게 이어나가면 코드의 가독성이 저해되고, 에러의 위치를 찾기 힘들다는 단점이 있을 수 있다. 이를 보완한 것이 바로...

   [async, await](https://github.com/976520/TIL/blob/main/javascript/async%2C%20await.md)

---

## 사용

1. api 통신

   [async, await](https://github.com/976520/TIL/blob/main/javascript/async%2C%20await.md)를 쓸 때와, [axios](https://github.com/976520/TIL/blob/main/javascript/axios.md)를 쓸 때와 비교하는 것이 중요하다.

   ```javascript
   function example() {
     fetch(url)
       .then((response) => {
         return response.json();
       })
       .then((data) => console.log(data));
   }
   ```
