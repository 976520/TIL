# Layout

태그: FrontEnd

# 레이아웃 설계

> 레이아웃(layout)이란, HTML 태그로 작성한 구성 요소를 제한된 공간 안에 효과적으로 배열하는 일을 의미한다.
> 

---

## Flex

```css
display: flex;
```

플렉스 박스 레이아웃은 1차원 방식으로 레이아웃을 설계할 수 있도록 고안된 스타일 속성이다. 1차원 방식이란, 가로(row) 혹은 세로(column) 중 한 방향으로 레이아웃을 설계하는 방식을 일컫는다. 

1. 기초
    1. 구성 요소
        
        플렉스 박스 레이아웃에서는 다음과 같은 독자적인 구성 요소가 존재한다.
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled.png)
        
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
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%201.png)
        
        이를 클릭하면 해당 요소의 플렉스 박스 레이아웃이 시각적으로 표시된다.
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%202.png)
        
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
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%203.png)
                
            - `space-around` item의 둘레(around)가 균일하도록 정렬한다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%204.png)
                
            - `space-evenly` item 사이와 양 끝의 간격이 균일하도록 정렬한다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%205.png)
                
            
        2. `aligin-items` `aligin-content` `aligin-self`
            
            item을 속성값에 따라 cross axis 방향으로 정렬할 때 사용하는 속성이다.
            
            - `stretch` cross axis 방향으로 item의 너비 또는 높이가 늘어난다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%206.png)
                
            - `flex-start` cross axis 방향의 시작을 기준으로 정렬한다.
            - `flex-end` cross axis 방향의 끝을 기준으로 정렬한다
            - `center` cross axis 방향의 중앙을 기준으로 정렬한다.
            - `baseline` item의 baseline을 기준으로 정렬한다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%207.png)
                
            

---

## Grid

```css
display: grid;
```

그리드 레이아웃은 2차원 방식으로 레이아웃을 설계할 수 있도록 고안된 속성이다. 이때 2차원 방식이란, 가로와 세로를 같이 사용해 레이아웃을 설계하는 방식이다. 

1. 기초
    1. 구성 요소
        
        그리드 레이아웃에서 사용하는 구성 요소는 다음과 같다.
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%208.png)
        
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
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%209.png)
        
        이를 클릭하면 브라우저에서 그리드 레이아웃의 구성 요소를 확인할 수 있다.
        
        ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2010.png)
        
2. 속성
    1. 기본 속성
        1. `grid-template-columns`  `grid-template-rows`
            
            그리드 레이아웃의 핵심은 column과 row이다. 따라서 이를 지정함으로써 grid cell을 생성해야 한다. 다음과 같이 앞에서부터 1행 또는 1열이며, 속성값을 공백으로 구분하여 작성한다.
            
            ```css
            .grid-container{
            	display: grid;
            	grid-templete-columns: 50px 50px 50px;
            	grid-templete-rows: 50px 50px;
            }
            ```
            
            이와 같이 작성하면 50px 크기의 2행*3열 그리드를 생성할 수 있다. 또한 이 코드를 다음과 같이 repeat() 함수를 이용하여 간편하고 직관성있게 작성할 수 있다.
            
            ```css
            .grid-container{
            	display: grid;
            	grid-templete-columns: repeat(3, 50px);
            	grid-templete-rows: repeat(2, 50px);
            }
            ```
            
            또한 속성값으로 auto를 지정하면, 해당하는 행 혹은 열의 크기를 container에 맞춰 자동으로 지정한다. 
            
        2. `column-gap` `row-gap`
            
            속성의 이름에서 알 수 있듯이, 앞서 설명한 그리드의 요소 중 gap의 크기를 설정할 수 있으며, 그 방법은 다음과 같다.
            
            ```css
            #container{
            	display: grid;
            	column-gap: 20px;
            	row-gap: 10px;
            }
            ```
            
            이와 같이 작성하면 그리드의 행과 행 사이의 간격은 10px, 열과 열 사이의 간격은 20px가 된다.
            
    2. 정렬 속성
        1. `align-items` `aligin-self`
            - `stretch` item이 grid cell을 채우도록 크기를 늘린다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2011.png)
                
            - `start` item이 grid cell의 맨 위에 배치된다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2012.png)
                
            - `end` item이 grid cell의 맨 아래에 배치된다.
            - `center` item이 grid cell의 세로 방향 중간에 배치된다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2013.png)
                
            
        2. `justify-items` `justify-self`
            - `stretch`  item이 grid cell을 채우도록 늘린다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2011.png)
                
            - `start` item이 grid cell의 좌측 끝에 배치된다.
            - `end` item이 grid cell의 우측 끝에 배치된다.
            - `center` item이 grid cell의 가로 방향 중간에 배치된다.
                
                ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2014.png)
                
            
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
            .container{
            	display: grid;
            	grid-templete-areas:
            	"header header header",
            	"nav content content",
            	"footer footer footer"
            }
            #header{
            	grid-area: header;
            }
            #nav{
            	grid-area: nav;
            }
            #content{
            	grid-area: content;
            }
            #footer{
            	grid-area: footer;
            }
            
            ```
            
            이러한 코드를 통해 다음과 같은 그리드 레이아웃을 완성할 수 있다.
            
            ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2015.png)
            
        2. `grid-column-start` `grid-column-end` `grid-row-start` `grid-row-end`
            
            `grid-column-start` 과 `grid-column-end` 속성은 grid number를 통해 item의 column 시작 위치와 종료 위치를 지정하며,  `grid-row-start` 과 `grid-row-end` 속성은 grid number를 통해 item의 row 시작 위치와 종료 위치를 지정한다.
            
            이 4가지의 속성을 조합하여 item의 배치를 지정할 수 있다. 만약 다음 그림처럼 item을 배치하고 싶다면,
            
            ![Untitled](Layout%209cd8abbb4bb3403f9b2bd22a4fbc0f5d/Untitled%2016.png)
            
            다음과 같이 코드를 작성할 수 있다.
            
            ```css
            .container{
            	display: grid;
            	grid-templete-columns: repeat(3, 100px);
            	grid-templete-rows: repeat(3, 100px);
            }
            .grid-item:nth-child(1){
            	grid-column-start: 1;
            	grid-column-end: 3;
            }
            .grid-item:nth-child(2){
            	grid-column-start: 3;
            	grid-column-end: 4;
            }
            .grid-item:nth-child(3){
            	grid-row-start: 2;
            	grid-row-end: 4;
            }
            .grid-item:nth-child(4){
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

## 반응형

[반응형 Layout](https://www.notion.so/Layout-ea029a9b998a438cac91cc3b267ca81c?pvs=21) 

---