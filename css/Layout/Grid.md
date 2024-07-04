## Grid

```css
display: grid;
```

그리드 레이아웃은 2차원 방식으로 레이아웃을 설계할 수 있도록 고안된 속성이다. 이때 2차원 방식이란, 가로와 세로를 같이 사용해 레이아웃을 설계하는 방식이다.

1. 기초

   1. 구성 요소

      그리드 레이아웃에서 사용하는 구성 요소는 다음과 같다.

      <img src="https://github.com/976520/TIL/assets/123460320/7effc5f9-5344-412b-8fb9-9dca4b3bf26a" width="500px"/>

      1. row (행)

         가로줄을 의미한다.

      2. column (열)

         세로줄을 의미한다.

      3. grid line

         row와 column을 구분하는 선을 의미한다.

      4. gird cell

         row와 column이 만나 이루어지는 하나의 공간을 나타낸다.

      5. gap

         각각의 grid cell들 사이의 간격을 의미한다.

      6. container

         display의 속성값으로 grid 혹은 inline-grid가 적용된 요소를 뜻하며, 그리드와 관련한 모든 내용은 이 container 안에 표현된다.

      7. item

         gird cell 안에서 표현되는 콘텐츠 요소를 일컫는다.

   2. 레이아웃 확인 방법

      그리드 레이아웃도 플렉스 박스처럼 레이아웃을 시각적으로 확인하기 위해 크롬 브라우저의 개발자 도구를 이용한다. Elements 탭에서 그리드 컨테이너로 지정된 태그를 보면 grid 아이콘이 보인다.

      <img src="https://github.com/976520/TIL/assets/123460320/a4ee148a-87b7-4759-bc94-b2685eeef69c" width="500"/>

      이를 클릭하면 브라우저에서 그리드 레이아웃의 구성 요소를 확인할 수 있다.
      <img src="https://github.com/976520/TIL/assets/123460320/fdd45a80-83b4-4a58-b550-d9d03577946a" width="600"/>

2. 속성

   1. 기본 속성

      1. `grid-template-columns` `grid-template-rows`

         그리드 레이아웃의 핵심은 column과 row이다. 따라서 이를 지정함으로써 grid cell을 생성해야 한다. 다음과 같이 앞에서부터 1행 또는 1열이며, 속성값을 공백으로 구분하여 작성한다.

         ```css
         .grid-container {
           display: grid;
           grid-templete-columns: 50px 50px 50px;
           grid-templete-rows: 50px 50px;
         }
         ```

         이와 같이 작성하면 50px 크기의 2행\*3열 그리드를 생성할 수 있다. 또한 이 코드를 다음과 같이 repeat() 함수를 이용하여 간편하고 직관성있게 작성할 수 있다.

         ```css
         .grid-container {
           display: grid;
           grid-templete-columns: repeat(3, 50px);
           grid-templete-rows: repeat(2, 50px);
         }
         ```

         또한 속성값으로 auto를 지정하면, 해당하는 행 혹은 열의 크기를 container에 맞춰 자동으로 지정한다.

      2. `column-gap` `row-gap`

         속성의 이름에서 알 수 있듯이, 앞서 설명한 그리드의 요소 중 gap의 크기를 설정할 수 있으며, 그 방법은 다음과 같다.

         ```css
         #container {
           display: grid;
           column-gap: 20px;
           row-gap: 10px;
         }
         ```

         이와 같이 작성하면 그리드의 행과 행 사이의 간격은 10px, 열과 열 사이의 간격은 20px가 된다.

   2. 정렬 속성

      1. `align-items` `aligin-self`

         - `stretch` item이 grid cell을 채우도록 크기를 늘린다.

             <img src="https://github.com/976520/TIL/assets/123460320/8d2753ee-4107-4b96-8bae-787934db1615" width=500/>

         - `start` item이 grid cell의 맨 위에 배치된다. <br/>
           <img src="https://github.com/976520/TIL/assets/123460320/4ffb9047-6ce5-4f39-b67e-ff139d9ddbe3" width="500"/>

         - `end` item이 grid cell의 맨 아래에 배치된다.
         - `center` item이 grid cell의 세로 방향 중간에 배치된다.
           <img src="https://github.com/976520/TIL/assets/123460320/d47c5f0a-fb7e-4f7d-a537-5aad9fe7a898" width="500"/>

      2. `justify-items` `justify-self`

         - `stretch` item이 grid cell을 채우도록 늘린다.

             <img src="https://github.com/976520/TIL/assets/123460320/8d2753ee-4107-4b96-8bae-787934db1615" width=500/>

         - `start` item이 grid cell의 좌측 끝에 배치된다.
         - `end` item이 grid cell의 우측 끝에 배치된다.
         - `center` item이 grid cell의 가로 방향 중간에 배치된다.

           <img src="https://github.com/976520/TIL/assets/123460320/6c1bb612-d540-4d40-9601-d109c3596ed4" width=500/>

      3. `place-items` `place-self`

         각각 `aligin-items`, `justify-items` 혹은 `aligin-self`, `justify-self` 속성을 한 번에 사용할 수 있는 단축 속성으로, 그 사용법은 다음과 같다.

         `place-items: <aligin-items 속성값> <justify-items 속성값>;`

         `place-self: <aligin-self 속성값> <justify-self 속성값>;`

   3. 배치 속성

      1. `grid-template-areas` `grid-area`

         `grid-templete-areas` 을 이용해 그리드 레이아웃의 각 행과 열에 다음과 같이 이름을 지정한 후, `grid-area` 를 통해 이름을 item에 배치할 수 있다.

         ```html
         <div class="container">
           <p id="header">머리</p>
           <p id="nav">왼팔</p>
           <p id="contet">배</p>
           <p id="footer">발</p>
         </div>
         ```

         ```css
         .container {
           display: grid;
           grid-templete-areas: "header header header", "nav content content", "footer footer footer";
         }
         #header {
           grid-area: header;
         }
         #nav {
           grid-area: nav;
         }
         #content {
           grid-area: content;
         }
         #footer {
           grid-area: footer;
         }
         ```

         이러한 코드를 통해 다음과 같은 그리드 레이아웃을 완성할 수 있다.

         <img src="https://github.com/976520/TIL/assets/123460320/eadb66b5-d6b2-47b2-9be1-ffe74fee9d1d" width="500"/>

      2. `grid-column-start` `grid-column-end` `grid-row-start` `grid-row-end`
         `grid-column-start` 과 `grid-column-end` 속성은 grid number를 통해 item의 column 시작 위치와 종료 위치를 지정하며, `grid-row-start` 과 `grid-row-end` 속성은 grid number를 통해 item의 row 시작 위치와 종료 위치를 지정한다.
         이 4가지의 속성을 조합하여 item의 배치를 지정할 수 있다. 만약 다음 그림처럼 item을 배치하고 싶다면,
         <img src="https://github.com/976520/TIL/assets/123460320/75bbfe3d-32e3-4f72-ab75-807a9cf570f8" width="500"/>

         다음과 같이 코드를 작성할 수 있다.

         ```css
         .container {
           display: grid;
           grid-templete-columns: repeat(3, 100px);
           grid-templete-rows: repeat(3, 100px);
         }
         .grid-item:nth-child(1) {
           grid-column-start: 1;
           grid-column-end: 3;
         }
         .grid-item:nth-child(2) {
           grid-column-start: 3;
           grid-column-end: 4;
         }
         .grid-item:nth-child(3) {
           grid-row-start: 2;
           grid-row-end: 4;
         }
         .grid-item:nth-child(4) {
           grid-column-start: 2;
           grid-column-end: 4;
           grid-row-start: 2;
           grid-row-end: 4;
         }
         ```

      3. `grid-column` `grid-row`

         각각 grid-column-start, grid-column-end 혹은 grid-row-start, gird-row-end 를 한 번에 사용할 수 있는 단축 속성으로, 그 사용법은 다음과 같다.

         `grid-column: <grid-column-start 속성값> <grid-column-end 속성값>`

         `grid-row: <grid-row-start 속성값> <grid-row-end 속성값>`

---
