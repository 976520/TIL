# Router

> react router는 react의 routing 관련 라이브러리 중 하나이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install react-router-dom
```

---

## routing

routing이란 사용자가 요청한 URL에 따라 알맞은 페이지를 보여주는 것이다. 여러 페이지로 구성된 웹 애플리케이션을 만들 때 페이지 별로 component를 분할하여 프로젝트를 관리하기 위해 필요하다.

react는 SPA 방식이기에 하나의 페이지 안에서 필요한 데이터만 가져와서 보여준다. 이 때 routing은 신규 페이지를 불러오지 않는 상황에서 url에 따라 선택된 데이터를 하나의 페이지 안에서 렌더링 해주는 작업이라고 할 수 있다.

---
