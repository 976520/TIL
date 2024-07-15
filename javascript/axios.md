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
     data: {
       data: "대충 인자로 보낼 데이터",
     },
   });
   ```

   axios를 이용한 요청 중에서 `url`, `data`와 같은 파라미터 옵션을 추가할 수 있으며, 그 종류는 다음과 같다.

2. 옵션

   1. `method`

      사용할 HTTP request 방식을 정한다. 기본값은 `get`이다.

      1. `get`

         `get`은 서버에서 데이터를 받아서 보여줄 때 사용한다.

         ```javascript
         const getData = async () => {
           const response = await axios.get("URL");
           console.log(response.data);
         };
         ```

      2. `post`

         `post`는 리소스를 새롭게 생성할 때 사용한다. 이때 두 번째 인자로 첫 번째의 URL 주소로 보낼 데이터 객체가 들어가게 된다.

         ```javascript
         const postData = async () => {
           const response = await axios.post("URL", { data: "data" });
           console.log(response.data);
         };
         ```

      3. `delete`

         이름에서 알 수 있듯, `delete`는 URL 주소에서의 데이터를 삭제한다. 따라서 두 번째 인자를 전달할 필요가 없다.

         ```javascript
         const deleteData = async () => {
           const response = await axios.delete("URL");
           console.log(response.data);
         };
         ```

      4. `put`

      5. `patch`

   1. `url`

   1. `headers`

   1. `data`

   1. `params`

   1. `responseType`

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
