# 액시오스

> Axios는 Promise API를 활용하는 HTTP 비동기 통신 라이브러리이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install axios
```

---

# 사용

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
