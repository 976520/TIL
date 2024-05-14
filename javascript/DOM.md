# DOM?

> DOM은 XML, HTML 문서의 각 항목을 계층으로 표현하여 생성, 변형, 삭제 할 수 있도록 돕는 인터페이스이다.
> 

DOM은 Document Object Model(문서 객체 모델)의 약자로  JS에서 HTML의 문서에 접근할 수 있는 API이다. 여기서 접근이란, 정의에서 알 수 있듯 HTML의 요소를 JS의 Object처럼 조작할 수 있다는 뜻이다! 

---

## DOM 개념

다음과 같은 HTML 문서가 있다고 가정해보자.

```html
<!DOCTYPE html>
<html>
	<head>
		<title>sexy title</title>
	</head>
	<body>
		<p>sexy text</p>
		<a>sexy href</a>
	</body>
</html>
```

이렇게 텍스트 파일로 만들어진 문서를 브라우저에 렌더링하려면 이를 브라우저가 이해할 수 있는 구조로 메모리에 올려야 한다. 브라우저에 내장된 화면을 그리는 엔진(rendering engine)이 이 문서를 로드한 후, 다음과 같이 파싱하여 브라우저가 이해할 수 있는 구조로 표현하고 메모리에 로드하는데, 이를 DOM이라고 부르는 것이다. 

![Untitled](DOM%208a3c4aea8db44552a9cd9b1ce88b6ab1/Untitled.png)

즉, 모든 요소와 속성을 객체로 만들고, 이 객체를 부모-자식 관계를 표현하는 트리 구조로 구성한 것이 DOM이다. DOM의 의의는 DOM이 제공하는 API를 이용해 개발자가 JS로 이것을 조작할 수 있는 데에 있다. JS는 이것을 이용해 HTML 요소나 style을 생성/변경/삭제하거나 event를 추가하고 그에 반응할 수 있다.

---

## DOM 조회

DOM구조를 조회할 때는 `console.dir` 을 사용한다. 이는 `console.log` 와 다르게 DOM을 Object 형태로 출력한다. 

1. <body>의 자식요소
    
    `console.dir(document.body)` 를 입력하여 body 아래의 모든 속성을 객체의 형태로 확인할 수 있다. 이중 chileren이 body의 자식요소를 뜻한다.
    
    ![Untitled](DOM%208a3c4aea8db44552a9cd9b1ce88b6ab1/Untitled%201.png)
    
    정신없으니까 `console.dir(document.body.children)` 을 통해 자식 요소만 골라내보자.
    
    ![Untitled](DOM%208a3c4aea8db44552a9cd9b1ce88b6ab1/Untitled%202.png)
    
    여기서 `console.dir(document.body.children[n])` 으로 n번째 자식만을 조회할 수 있다.
    
2. 특정 id를 가진 엘리먼트의 자식요소
    
    매번 자식요소를 조회할 때 마다 `console.dir(document.body.children[3])` 이런걸 쓰고 있으면 귀찮기 마련이다. 이럴 때 따로 변수 선언을 하고 id를 할당하면 번거롭지 않을 수 있다.
    
    ```jsx
    const exampleId = document.body.children[3]
    console.dir(exampleId)
    ```
    
3. 특정 id를 가진 엘리먼트의 부모요소 ~~느그 아부지 뭐하시노~~
    
    `console.dir(document.body.children[n].parentElement)` 는 n번째 자식 요소의 부모요소를 조회하는 코드이다. 정말 읽기 불편하기 때문에 아까와 같이변수 선언을 해서 가독성을 높여보겠다. 
    
    ```jsx
    const exampleId = document.body.children[3]
    console.dir(exampleId.parentElement)
    ```
    

---

## **Virtual DOM**

만약 페이지의 특정 요소의 style을 변경하려고 한다면, 브라우저가 해당 요소를 찾아서 색상을 변경한 후 그를 적용하기 위해 해당 요소부터 그 하위 요소까지 모두 다시 그리게 된다. 이러한 일련의 과정을 DOM구조나 레이아웃의 변경의 경우 Reflow, 요소의 외양적 변경의 경우 Repaint라고 칭한다. Reflow와 Repaint의 과정에서 많은 비용이 발생하는데, Virtual(가상의) DOM은 이를 완화하기 위해 등장했다. 

React는 렌더링이 발생할 때 마다 이러한 VDOM을 생성한다. 이 VDOM은 진짜 DOM의 가벼운 복사본 정도로 이해하면 되며, JS 객체 형태로 존재한다. 또한 React는 항상 VDOM을 렌더링 전, 후 버전으로 2개 가지고 있으며, 이를 비교하여 실질적으로 state의 변경이 일어난 부분만 DOM에 반영한다. Virturl DOM은 실제 DOM을 직접 조작하는 대신 간접적으로 조작하면서 렌더링 성능을 향상시키는 데에 목적을 둔다.

---
