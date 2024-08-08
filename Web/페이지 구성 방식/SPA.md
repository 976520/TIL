## SPA

1. 개념

   > SPA는 Single Page Application의 약자로 한 개의 페이지로 구성된 웹 application이다.

   SPA는 application 속도의 향상을 기대할 수 있다. 이는 User experience와도 직결되며, mobile first 전략에도 부합한다.

   application에 필요한 모든 static(정적) resource를 최초에 단 한번만 다운로드하고 사용자가 새로운 페이지를 요청할 시, 페이지 갱신에 필요한 데이터만 전달받아 기존 페이지의 내부를 동적으로 수정하여 보여준다.

2. 장점

   static resource를 최초 접근 이후 다시 다운받지 않기 때문에 페이지 갱신 시 화면이 새로고침 되어 깜빡이지 않아 UX가 개선된다.

   component 기반 코딩이 가능하기 때문에 component의 특성에 따라 재사용성이 높다.

3. 단점

   사용할 resource를 최초 접근 시 모두 다운받기 때문에 초기 구동 속도가 느릴 수 있다. 또한 독단적인 HTML 페이지가 아닌 JS로 구현된 것이기 때문에 SEO(검색 엔진 최적화)가 어렵다고 한다. JS를 실행시키지 않는 일반 크롤러에서는 페이지의 정보를 제대로 가져가지 않기 때문이다.

   또한 application의 규모가 커지면 JS 파일이 지나치게 커질 수 있다. 유저가 실제로 방문하지 않을 수 있는 페이지에 관련된 스크립트도 불러오기 때문이다.

---
