## Flex

```css
display: flex;
```

플렉스 박스 레이아웃은 1차원 방식으로 레이아웃을 설계할 수 있도록 고안된 스타일 속성이다. 1차원 방식이란, 가로(row) 혹은 세로(column) 중 한 방향으로 레이아웃을 설계하는 방식을 일컫는다.

1. 기초

   1. 구성 요소

      플렉스 박스 레이아웃에서는 다음과 같은 독자적인 구성 요소가 존재한다.

      <img src="https://github.com/976520/TIL/assets/123460320/3f19f70a-6b8a-44e7-8877-99d1fad01233" width="500"/>

      1. main axis (주축)

         플렉스 박스의 진행 방향과 수평한 축을 뜻한다.

      2. cross axis (교차축)

         플렉스 박스의 진행 방향에 수직한 축을 뜻한다. 즉, 주축에 대해서도 수직하다.

      3. container

         display의 속성값으로 flex 혹은 inline-flex가 적용된 요소를 뜻한다.

      4. item

         container와 자식 관계를 이루는 요소이다.

   2. 레이아웃 확인 방법

      브라우저는 일반적으로 플렉스 박스 레이아웃을 확인하는 기능을 지원한다. 크롬 브라우저의 경우 개발자 도구(F12)를 이용한다.

      개발자 도구의 Elements 탭으로 가면, 플렉스 박스 레이아웃이 적용된 HTML element는 옆에 flex 아이콘이 있는 것을 확인할 수 있다.

      <img src="https://github.com/976520/TIL/assets/123460320/1fcbb8ab-aa97-43f6-8201-ef407cbbecda" height="400px"/>

      이를 클릭하면 해당 요소의 플렉스 박스 레이아웃이 시각적으로 표시된다.

      <img src="https://github.com/976520/TIL/assets/123460320/57ab2d25-28fc-4c6c-9e3a-cd652fbb2a4f" height="150px"/>

2. 속성

   플렉스 박스 레이아웃에 적용할 수 있는 속성은 다음과 같다.

   1. 기본 속성

      1. `flex-direction`

         속성값에 따라 플렉스 박스 레이아웃의 main axis 방향을 결정한다.

         - `row` 방향을 왼쪽→오른쪽으로 지정한다.
         - `row-reverse` 방향을 오른쪽→왼쪽으로 지정한다.
         - `column` 방향을 위쪽→아래쪽으로 지정한다.
         - `column-reverse` 방향을 아래쪽→위쪽으로 지정한다.

      2. `flex-wrap`

         속성값에 따라 item이 container 영역을 벗어날 때 어떻게 처리할지를 결정하며, 기본값은 nowrap이다.

         - `nowrap` item이 container를 벗어나도 무시한다.
         - `wrap` item이 container를 벗어날 시 줄바꿈을 한다.
         - `wrap-reverse` item이 container를 벗어나면 wrap의 역방향으로 줄바꿈을 한다.

      3. `flex-flow`

         `flex-flow: <flex-direction 속성값> <flex-wrap 속성값>;` 와 같이 사용하며, 문법에서 알 수 있듯 flex-direction과 flex-wrap을 한 번에 사용할 수 있는 속성이다.

   2. 정렬 속성

      1. `justify-content`

         item을 속성값에 따라 main axis 방향으로 정렬할 때 사용하는 속성이다.

         - `flex-start` main axis 방향의 시작을 기준으로 정렬한다.
         - `flex-end` main axis 방향의 끝을 기준으로 정렬한다.
         - `center` main axis 방향의 중앙에 정렬한다.
         - `space-between` item 사이의 간격이 균일하도록 정렬한다.
           <img src="https://github.com/976520/TIL/assets/123460320/84174cac-8786-41de-a503-b64d2c650b6a" width="500"/>

         - `space-around` item의 둘레(around)가 균일하도록 정렬한다.

             <img src="https://github.com/976520/TIL/assets/123460320/74bb767e-c4d5-4d69-8a09-bbe170441c5d" width="500"/>

         - `space-evenly` item 사이와 양 끝의 간격이 균일하도록 정렬한다.
           <img src="https://github.com/976520/TIL/assets/123460320/1bd3f7d6-741e-40df-99f1-ad1b405b86d4" width="500"/>

      2. `aligin-items` `aligin-content` `aligin-self`

         item을 속성값에 따라 cross axis 방향으로 정렬할 때 사용하는 속성이다.

         - `stretch` cross axis 방향으로 item의 너비 또는 높이가 늘어난다.
           <img src="https://github.com/976520/TIL/assets/123460320/aa1e93c9-84b1-455a-b177-10bf74e47068" width="500"/>

         - `flex-start` cross axis 방향의 시작을 기준으로 정렬한다.
         - `flex-end` cross axis 방향의 끝을 기준으로 정렬한다
         - `center` cross axis 방향의 중앙을 기준으로 정렬한다.
         - `baseline` item의 baseline을 기준으로 정렬한다.
           <imt src="https://github.com/976520/TIL/assets/123460320/57b0c56e-ceed-48d6-9491-adc83076a509" width="500"/>
