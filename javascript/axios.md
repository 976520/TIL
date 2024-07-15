# 액시오스

> Axios는 Promise API를 활용하는 HTTP 비동기 통신 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install axios
```

---

## 개념

1. 정의

---

## 문법

1. 구조

   대략적인 구조는 다음과 같다.

   ```javascript
   axios({
     url: "대충 통신할 URL",
     method: "대충 HTTP 메소드",
     data: {
       data: "대충 인자로 보낼 데이터",
     },
   });
   ```

   axios를 이용한 요청 중에서 `url`, `method`와 같은 파라미터 옵션을 추가할 수 있으며, 그 종류는 다음과 같다.

2. 옵션

   1. `method`

   2. `url`

   3. `headers`

   4. `data`

   5. `params`

   6. `responseType`

---

## 사용

1. api 통신

   [promise](https://github.com/976520/TIL/blob/main/javascript/promise.md)를 쓸 때와, [async, await](https://github.com/976520/TIL/blob/main/javascript/async%2C%20await.md)를 쓸 때와 비교하는 것이 중요하다.

   ```javascript
   function example() {
     return axios
       .get(url)
       .then((response) => {
         return response.data;
       })
       .catch((error) => {
         throw error;
       });
   }
   ```
