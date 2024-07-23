# Router

> react router는 react의 routing 관련 라이브러리 중 하나이다.

외부 라이브러리이기 때문에 별도의 설치가 필요하다.

```shell
npm install react-router-dom
```

---

## 개념

1. routing

   routing이란 사용자가 요청한 URL에 따라 알맞은 페이지를 보여주는 것이다. 여러 페이지로 구성된 웹 애플리케이션을 만들 때 페이지 별로 component를 분할하여 프로젝트를 관리하기 위해 필요하다.

2. react router

   react는 [SPA](https://github.com/976520/TIL/blob/main/Web/%ED%8E%98%EC%9D%B4%EC%A7%80%20%EA%B5%AC%EC%84%B1%20%EB%B0%A9%EC%8B%9D/SPA.md) 방식이기에 하나의 페이지 안에서 필요한 데이터만 가져와서 보여준다. 이 때 routing은 신규 페이지를 불러오지 않는 상황에서 url에 따라 선택된 데이터를 하나의 페이지 안에서 렌더링 해주는 작업이라고 할 수 있다.

   이러한 react 안에서 routing 작업을 해 주는 것이 react router이다.

3. 종류

   1. HashRouter

      주소에 #이 붙게 된다. 또한 별도의 서버 설정이 없어도 새로고침 시 오류가 발생하지 않는다. 이는 hashRouter가 # 뒤의 문자열을 브라우저에서만 관리하게끔 하고 서버는 # 이전의 기본 URL로 데이터를 요청하기 때문이다. 이 # 뒤의 문자열을 브라우저에서는 fragment 식별자로 간주한다.

      hash값이 변경되면 hashchange 이벤트가 발생하는데, 이를 JS에서 감지하고 동작을 수행한다.

      그러나 URL의 hash값을 사용하여 history API를 사용하지 않기 때문에 SEO에는 매우 취약하다.

   2. BrowserRouter

      HTML5의 history API를 이용하여 URL과 UI를 동기화해 주는 router이다.

---

## 사용

react router를 파일에 다음과 같이 router를 `import` 하여 사용한다.

```javascript
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Layout from "./layout/Layout.tsx";
import HomeMain from "./page/HomePage.tsx";
import Login from "./page/Login.tsx";
import ProjectPage from "./page/ProjectPage.tsx";
import ProfilePage from "./page/ProfilePage.tsx";
import ProjectListPage from "./page/ProjectListPage.tsx";
import Signup from "./page/Signup.tsx";
import CreateProjectPage from "./page/CreateProjectPage.tsx";
import PostsPage from "./page/PostListPage.tsx";

function App() {
  return (
    <>
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Layout />}>
            <Route path="/" element={<HomeMain />} />
            <Route path="/projects" element={<ProjectListPage />} />
            <Route path="/profile" element={<ProfilePage />} />
            <Route path="/project/:id/" element={<ProjectPage />} />
            <Route path="/createProject" element={<CreateProjectPage />} />
            <Route path="/posts" element={<PostsPage />} />
          </Route>
          <Route path="/login" element={<Login />} />
          <Route path="/signup" element={<Signup />} />
        </Routes>
      </BrowserRouter>
    </>
  );
}

export default App;
```

~~실제 아이디어 페스티벌 코드를 훔쳐왔다~~

1. 페이지 분할

   `BrowserRouter`는 react router dom을 적용시키고 싶은 최상위 component를 감싸는 wrapper component이다. `Routes` component 하위에 `Route`들을 배치하여 각 페이지를 나눈다. `Route` 안에 다시 `Route`를 배치하여 다시 서브 페이지들을 나눌 수 있다.

2. 동적 경로

   :으로 시작하는 문자열을 사용하면 경로에 파라미터를 지정할 수 있다. 예를 들어 예제 코드의 `/:id` 라는 경로에 `/517`이라는 주소로 접속하면, 실제 `517` 값을 `id` 파라미터로 받는 식이다.

   이 파라미터를 사용하기 위해서는 `useParams`를 이용하면 된다.

3. Navigate component

   Navigate component가 return될 경우, to 의 prop에 있는 경로로 이동한다.

   ```javascript
   import { Navigate } from "react-router-dom";

   function Example() {
     const onClick = () => {
       return <Navigate to="/슝" />;
     };

     return (
       <div>
         <button onClick={onClick}>click me</button>
       </div>
     );
   }
   ```

---
