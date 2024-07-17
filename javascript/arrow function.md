# () => {...};

> 화살표 함수(arrow function)란 함수를 변수에 할당하여 사용하는 함수 표현식의 유형 중 하나이다.

---

## 이해

1. 표현

   일반 함수는 function 키워드를 이용하는 반면에 화살표 함수는 => 를 이용하여 함수를 선언한다. 기존 함수보다 간결하다는 장점이 있다.

2. 특징

   화살표 함수는 일반 함수와 달리 inheritance를 생성할 수 없다. 즉, 생성자 함수로 사용할 수 없다. 또한 arguments 객체를 받을 수 없다.

   ~~예쁘다~~

---

## 문법

1. 일반 함수와 비교

   다음은 순서대로 일반 함수의 표현식과 화살표 함수의 표현식을 나타낸다. 두 함수는 표현이 다를 뿐 매개변수를 두 개 받아서 그 합을 반환한다는 기능은 동일하다.

   ```javascript
   const example = function (param1, param2) {
     return param1 + param2;
   };
   ```

   ```javascript
   const example = (param1, param2) => {
     return param1 + param2;
   };
   ```

   이때, 매개변수명은 당연히 중복될 수 없다.

2. 소괄호 생략

   화살표 함수에서 매개변수가 하나인 경우 소괄호의 생략이 가능하다.

   ~~근데 Prettier 이슈로 VScode에서 작성이 안된다. 그냥 쓰지말자.~~

   ```javascript
   const example = (param) => {
     return param;
   };
   ```

3. return 생략

   화살표 함수 내부가 single expression(단일 표현식)인 경우 `return()`을 생략할 수 있다. 이때 반드시 중괄호를 함께 생략하여야 한다.

   두 함수는 표현이 다를 뿐 매개변수를 두 개 받아서 그 합을 반환한다는 기능은 동일하다.

   ```javascript
   const example = (param1, param2) => {
     return param1 + param2;
   };
   ```

   ```javascript
   const example = (param1, param2) => param1 + param2;
   ```

---
