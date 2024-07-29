## 미디어 쿼리

1. 이해

   > Media query는 사이트에 접속하는 미디어 타입과 특징, 해상도에 따라 다른 스타일 속성을 적용하게 하는 기술이다.

   Media query를 이용해 사이트에 접속하는 디바이스의 타입과 해상도에 따라 다른 스타일 속성을 알맞게 적용하면 그 자체로 반응형 웹이 완성된다.

1. 사용

   Media query의 형식은 다음과 같다.

   ```css
   @media not|only mediatype and (media feature) and|or|not (media feature) {
     /* style */
   }
   ```

   Media query는 `@media` 로 시작하며, 여러 조건과 상태를 정의해 각 media query가 적용되는 기준을 세우면 된다. 이때 조건은 다음과 같다.

   1. `not | only`

      `not`은 뒤에 오는 모든 조건을 부정하며, `only`는 media query를 지원하는 기기만 media query를 해석하라는 의미이다.

   2. `mediatyle`

      Media query가 적용될 미디어 타입을 명시한다. 생략할 수 있으며, 이 경우 `all`로 인식한다. 생략하지 않을 경우 반드시 `and` 가 후행해야 한다. 사용할 수 있는 미디어 타입은 다음과 같다.

      | all    | 모든 장치                                       |
      | ------ | ----------------------------------------------- |
      | print  | 프린터기 등의 인쇄 장치                         |
      | screen | 모니터 등의 컴퓨터 화면 혹은 스마트 기기        |
      | speech | 스크린 리더기 등의 페이지를 소리 내어 읽는 장치 |

   3. `media feature`

      Media query가 적용될 미디어 조건을 명시하며, 종류가 18가지로 많지만 자주 쓰이는 것만 소개한다.

      | min-width   | 화면 너비 | media query가 적용될 최소 너비              |
      | ----------- | --------- | ------------------------------------------- |
      | max-width   | 화면 너비 | media query가 적용될 최대 너비              |
      | orientation | portrait  | 세로 모드, 뷰포트의 높이가 너비보다 큰 경우 |
      | orientation | landscape | 가로 모드, 뷰포트의 너비가 높이보다 큰 경우 |

1. 예시

   1. 연습

      ```css
      @media only screen and (min-width: 360) and (max-width: 720px) {
        /*style*/
      }
      ```

      이와 같은 media query의 실행 조건은 다음과 같다.

      1. `only` media query를 적용할 수 있는 디바이스 이면서
      2. `screen` 컴퓨터 화면 장치 혹은 스마트 기기 일 때
      3. `and` 그리고
      4. `min-width` 뷰포트의 최소 너비가 360px 일 때
      5. `and` 그리고
      6. `max-width` 뷰포트의 최대 너비가 720px 일 때

      또한 `only` 와 미디어 타입은 생략할 수 있으므로 다음과 같이 표현할 수 있다.

      ```css
      @media (min-width: 360) and (max-width: 720px) {
        /*style*/
      }
      ```

   2. 적용

      ```css
      div {
        width: 100px;
        height: 100px;
        background-color: blue;
        @media only all and (min-width: 420px) {
          div {
            background-color: tomato;
          }
        }
      }
      ```

      이 코드와 같은 경우 뷰포트의 너비가 420px 이상일 때는 `<div>`가 상큼한 tomato색, 그렇지 않을 때는 파란색으로 표시된다.

---
