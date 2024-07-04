# 다시 전화해 주세요

> callback 함수란 매개변수로 함수 객체를 전달해서 호출 함수 내에서 매개변수 함수를 실행하는 것이다.

---

## 개념

1. 정의

   콜백 함수는 파라미터로 일반적인 변수 대신 함수를 전달한다. 쉽게 말해, 어떤 함수 A를 호출하면서
   A에게 "~~조건을 충족할 때 함수 B를 실행해" 라는 요청을 보내는 것이다. 함수 A는 해당 조건이
   갖춰졌는지의 여부를 스스로 판단다고, B를 호출하게 된다.

   콜백 함수는 이처럼 다른 함수에게 인자로 넘겨짐으로써, 후술할 제어권도 함께 위임한 함수이다.

2. 제어권

   1. 호출 시점

      콜백 함수를 받은 함수는 자체적인 로직에 의해 콜백 함수를 적절한 시점에 실행하게 된다.
      이는 다른 말로 콜백 함수는 호출 당하는 시점에 대한 제어권이 위임되었다는 것이다.

   1. 인자의 순서

      콜백 함수의 인자의 순서 역시 호출하는 함수에 의해 정의된다.

      ```js
      function example(callback) {
        const value1 = 9;
        const value2 = 6;
        callback(value1, value2); // 콜백 함수에 두 개의 인자를 순서대로 전달
      }

      example((a, b) => {
        console.log(a); // 출력: 9
        console.log(b); // 출력: 6
      });
      ```

      콜백 함수를 호출할 때 인자의 순서에 대한 정보가 들어 있다. 따라서 콜백 함수의 제어권을
      받은 함수는 이를 호출할 때 어떤 값들을 어떤 순서로 넘길 것인지에 대한 제어권을 가진다.

3. 간결성

   보통 콜백 함수는 일회용으로 사용하기 때문에 보통 **익명 함수**, 다음과 같이 이름이 명시되지
   않은 형태의 함수 를 넣어주게 된다. 이는 코드의 간결성을 위한 것도 있지만,
   **함수 이름으로 인한 충돌 방지**를 위한 이유도 있다.

   ```js
   func(parameter, function (callback) {
     console.log(callback);
   });
   ```

   이처럼 콜백 함수를 익명 함수로 정의함으로써 코드의 간결성을 얻을 수 있다. 하지만 **익명 화살표 함수**
   를 통해 더욱 간결해질 수 있다. 이는 이름에서 알 수 있듯, JS의 화살표 함수와 익명 함수가
   합쳐진 것이다.

   ```js
   func(parameter, (callback) => {
     console.log(callback);
   });
   ```

---

## 사용

1. Fetch

   다음 코드에서 fetchData는 URL에서 데이터를 가져오고, 결과를 콜백 함수에 전달한다. handleData는 에러가 발생했는지 여부에 따라 적절한 메시지를 출력한다.

   ```js
   function fetchData(url, callback) {
     fetch(url)
       .then((response) => response.json())
       .then((data) => callback(null, data))
       .catch((error) => callback(error, null));
   }

   const handleData = (error, data) => {
     error ? console.error("Error:", error) : console.log("Data:", data);
   };

   fetchData("API_URL", handleData);
   ```

2. 콜백 지옥

   콜백 지옥(callback hell)은 함수의 매개변수로 넘겨지는 콜백 함수가 과도하게 반복되어 코드의
   들여쓰기 수준이 심하게 깊어지는 현상이다.

   ```js
   setTimeout(function () {
     console.log("Task 1");
     setTimeout(function () {
       console.log("Task 2");
       setTimeout(function () {
         console.log("Task 3");
         setTimeout(function () {
           console.log("Task 4");
           setTimeout(function () {
             console.log("Task 5");
             setTimeout(function () {
               console.log("Task 6");
               setTimeout(function () {
                 console.log("Task 7");
                 setTimeout(function () {
                   console.log("Task 8");
                   setTimeout(function () {
                     console.log("Task 9");
                     setTimeout(function () {
                       console.log("Task 10");
                     }, 1000);
                   }, 1000);
                 }, 1000);
               }, 1000);
             }, 1000);
           }, 1000);
         }, 1000);
       }, 1000);
     }, 1000);
   }, 1000);
   ```

   이러한 콜백 지옥 현상은 다음 두 방법을 통해 해결할 수 있다.

   1. [Promise](https://github.com/976520/TIL/blob/main/javascript/promise.md)

   2. async/await
