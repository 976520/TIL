## API

1. 개념

   API는 Application Programming Interface의 약자로, application이 서로 통신하여 데이터를 교환할 수 있도록 하는 일련의 규칙이다. ~~프로토콜~~ 하나의 예시로 Java 시스템을 쉽게 이해할 수 있도록 그 명령어를 정의해 놓은 Java API가 있다.

   웹에서는 데이터가 클라이언트로부터 분리되어 서버에 저장된다. 그러므로 클라이언트는 서버에 저장된 정보에 접근하기 위해 지속적으로 서버에게 요청을 보내야 한다. 이때 요청을 보내는 방법이 지멋대로면 개발자들이 힘들기 때문에, 이를 통일하여 약속해둔 것이 API이다.

2. REST API

   REST란 Representational State Transfer의 약자로, resource를 이름으로 구분하여 해당 resource의 상태를 주고받는 것을 뜻한다. 더 명확하게 설명하자면,

   **HTTP URL을 통해 resource를 명시하고, HTTP method를 통해 URL로 명시된 해당 자원에 대한 CRUD operation을 적용하는 것을 뜻한다.**

   CRUD는 대부분의 소프트웨어가 가지는 기본적인 처리 작업인 Create, Read, Update, Delete를 묶어서 부르는 것으로, REST에서는 이를 HTTP method로 다음과 같이 표현할 수 있다.

   1. Create `POST`

   2. Read `GET`

   3. Update `PUT` `PATCH`

   4. Delete `DELETE`

   거의 모든 서비스는 이러한 API를 자체 개발하여 클라이언트가 서버의 데이터를 이용할 수 있도록 한다. 이러한 API를 serve(제공)해주는 것이 API server이다.
