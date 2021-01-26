# React란?

React(리액트)란 **사용자 인터페이스(UI)를 구축하기 위한 자바스크립트 라이브러리**입니다. 

React는 선언적이고 효율적이며, 유연합니다. 

또한 React의 컴포넌트(component)라고 하는 요소를 이용하면 복잡한 UI를 독립적인 단위로 쪼개어 구현할 수 있습니다.

### 등장 배경

React를 개발하기 전에는 페이스북은 성능이 좋은 동적 UI를 구축하는 과제에 직면했습니다. 

예를 들어, 사용자가 채팅하는 동시에 뉴스 피드 업데이트가 이루어지길 원했습니다. 

이를 위해 페이스북은 개발 프로세스 최적화를 해야 했고 그에 따라 자바스크립트를 사용하기로 했습니다. 

그리고 페이스북 마크업 구문인 XHP를 자바스크립트에 넣을 것을 제안했습니다. 

이것은 불가능해 보였지만 2011년에 페이스북은 자바스크립트와 XHP 공생을 기반으로 React 라이브러리를 출시했습니다. 

React는 2013년 오픈 소스화되었으며 다른 어떤 도구보다 빠르게 동작합니다.

## 그렇다면, React를 왜 사용해야 할까요?

프론트엔드(Front-end)를 만드는 라이브러리는 상당히 많습니다. HTML과 CSS, Javascript, Jquery 등 다양한 방법으로 얼마든지 제작이 가능합니다. 하지만, 요즘 같은 복잡한 동적인 웹페이지를 만드는 시대에는 다릅니다.

웹 페이지는 각 페이지마다 페이지를 관리해줘야 하고, 사용자의 응답에 따라 인터페이스가 지속적으로 변해야 합니다. 

하지만, 그렇게 하기 위해선 기존 방식으로 관리하기는 어렵습니다. React는 이런 어려움을 해결해줍니다!! 

이미, 위에 등장 배경에서처럼 페이스북에서 적용해 증명했으니 해결은 충분히 가능하겠죠? 

요즘은 React를 Airbnb와 Netflix에서도 React를 사용하면서 점점 생태계가 커지고 있습니다.

**한 마디로! React를 사용하는 이유들을 정리하면 “사용자와의 소통을 UI로 쉽게 구현하고 대규모의 웹페이지를 관리하기 위해 사용한다”라고 말할 수 있습니다.**

## 장점

- React의 Virtual DOM은 사용자 경험을 향상하고 개발자의 작업 속도를 높입니다. Virtual DOM이란 가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화하는 프로그래밍 개념입니다.
- React 컴포넌트의 재사용은 개발 시간을 크게 절약합니다.
- 단방향 데이터 흐름을 통해 안정적인 코드를 제공합니다. 단방향 데이터 흐름은 데이터는 항상 일정한 장소에 있고, 그 장소에서만 변경이 가능한 것을 의미합니다.
- 오픈 소스이며 페이스북 라이브러리이기 때문에 지속해서 개발되고 커뮤니티에 공개됩니다.
- Hooks를 이용해 컴포넌트의 상태를 쉽게 관리할 수 있습니다.
- 여러 개발 도구를 지원합니다. 예를 들어 크롬에서는 React Developer Tools라는 확장 프로그램을 제공합니다.

### 파일 구조

- public : 이미지나 html 같은 정적 파일이 담기는 디렉토리
    - .html
    - .img
- src : 개발에 대한 코드를 작성하는 디렉토리
    - App.css : 컴포넌트의 스타일 설정
    - App.js : 컴포넌트 코드 작성
    - App.test.js : 컴포넌트 테스트를 위한 코드
    - index.css : 메인 페이지의 스타일 작성
    - index.js : 주로 코드를 작성할 메인 페이지
    - serviceWorker.js : 브라우저에서 실행되는 스크립트 파일
    - setupTest.js : 컴포넌트 테스트 설정을 위한 파일
- .env
- next.config.js : 프로젝트 설정을 위한 파일
- package.json : 패키지에 관한 정보와 의존중인 버전에 관한 정보를 담음
- yarn.lock : 자바스크립트의 새로운 패키지 매니저인 yarn을 다양한 디바이스에서 일관성있게 적용


지금 등장하는 모든 용어들에 대해 암기하실 필요는 없습니다. 우선 React의 전체적인 구조와 흐름에 집중해서 학습을 진행하세요.
상기 모든 내용은 React 공식 문서 를 기반으로 작성되었습니다.

## HTML로 리액트 구동

HTML로 리액트 구동
React의 세계로 오신 여러분 환영합니다! 간단한 React 앱을 CDN과 함께 구동해보겠습니다. React와 ReactDOM은 모두 CDN을 통해 사용할 수 있습니다.

**DOM(Document Object Model)**이란 HTML 요소들을 노드로 포함하는 트리와 같은 구조를 말합니다.

**CDN(Contents Delivery Network)**은 지리적 물리적으로 떨어져 있는 사용자에게 컨텐츠 제공자의 컨텐츠를 더 빠르게 제공할 수 있는 기술을 말합니다. CDN을 사용하면 다음과 같은 이점이 있습니다.

- 온라인 콘텐츠를 빠르게 전송 가능합니다.
- 시스템을 정상적으로 사용가능한 정도(가용성)가 높습니다.
- 외부의 다양한 공격을 방지합니다.

React에서 CDN을 활용하기 위해서는 index.html 파일의 <head>태그 내에 ```crossorigin``` 속성을 이용하면 됩니다. 해당 속성을 통해 실행 중인 React 앱이 해당 출처의 리소스에 접근할 수 있는 권한을 부여할 수 있도록 알려줄 수 있습니다.

<script crossorigin src="..."></script>

### 지시사항

1. index.html 파일 내 head 태그 내에 아래 React와 ReactDom에 대한 CDN을 연결하는 코드를 아래처럼 추가하세요.
```
<script crossorigin src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
```

> Tips : CDN 연결이 없더라도 보이는 실행 결과는 차이가 없습니다.

### 해답 코드
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    
    <!-- CDN 연결을 위한 코드를 추가합니다. -->
    <script crossorigin src="https://unpkg.com/react@17/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js"></script>
    
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

# React와 자바스크립트의 차이점

앞서 페이스북 사례를 통해 웹 앱 변화에 대응하여 프로세스 속도를 높이기 위해 React가 등장한 배경에 대해 확인했습니다. 

그렇다면 React와 자바스크립트의 차이점이 무엇인지, 왜 굳이 React를 사용하는지에 대해 알아보겠습니다.

React는 **앱 작성 방식을 정의하는 라이브러리**입니다. 

이는 데이터가 앱에 사용되는 방식과 그 데이터가 변화하는 결과에 따른 UI 변경 방법에 대해 명확한 규칙을 설정하여 수행합니다. 

반면 **자바스크립트는 규칙을 설정하지 않는 스크립트 언어**라고 할 수 있습니다. 

따라서 이러한 라이브러리 없이 작성된 앱은 더 자유로울수는 있지만, 정해진 것이 없기 때문에 코드를 작성하다가 길을 잃어버리기 쉽습니다.

먼저 React와 자바스크립트의 차이점 4가지를 간단한 코드와 함께살펴보겠습니다. 

만약 자바스크립트의 문법이 익숙하지 않다면, 어떠한 문법들이 있었는지 튜토리얼을 다시 확인해 보시기 바랍니다.

## 사용자 인터페이스를 처음 만드는 방법

### 자바스크립트

자바스크립트에서 사용자 인터페이스는 보통 아래처럼 HTML을 통해 구현합니다. 이 때 자바스크립트는 따로 추가적인 코드가 필요하지 않습니다.
```
<div>
    <h1>Grocery List</h1>
    <ul>
        <li>Milk</li>
        <li>Bread</li>
        <li>Eggs</li>
    </ul>
</div>
```

### React

반면 React는 **JSX로 반환되는 컴포넌트를 통해 UI를 정의**합니다. JSX는 HTML처럼 보이지만 실제로는 자바스크립트입니다. 

아래에서 생성된 ```GroceryList``` 컴포넌트는 이후 **ReactDOM 라이브러리에 의해 렌더링되어 화면에 출력**될 수 있습니다.
```
function GroceryList(props) {
    return (
        <div>
            <h1>Grocery List</h1>
            <ul>
                <li>Milk</li>
                <li>Bread</li>
                <li>Eggs</li>
            </ul>
        </div>
    )
};
```

## 앱에서 기능이 분할되는 방식

### 자바스크립트

자바스크립트 앱에서는 앱의 기능 또는 UI의 요소를 분할하는 방법에 대한 특별한 요구사항이 없습니다. 

기본적인 출력은 아래처럼 기본 **HTML 파일**에 정의합니다.
```
<div>
    <h1>Grocery List</h1>
    <ul id="grocery-list">
        <li>Milk</li>
        <li>Bread</li>
        <li>Eggs</li>
    </ul>
</div>
```
그리고 목록을 업데이트하는 코드를 **자바스크립트 파일**에 넣어야 합니다.
```
function addItemToList() {

  // Add item

}
```

코드가 이렇게 작성되어야 하는 이유는 관심사 분리 원칙에 따라 화면에 출력을 하는 HTML과 기능을 구현하는 자바스크립트가 분리되도록 설계하였기 때문입니다. 하지만 이러한 방식은 앱이 복잡해짐에 따라 큰 골칫거리가 되었습니다. 왜냐하면 하나의 HTML을 구성하는 코드가 서로 다른 자바스크립트 파일에 있을 수 있기 때문에 HTML의 기능이 구현된 코드가 위치한 곳을 기억하기 어렵기 때문입니다.

React
반면 React를 이용하면 위의 기능을 구현하는데 필요한 코드를 하나의 파일로 유지할 수 있습니다.

function GroceryList(props) {
    function addItem() {
        // Add Item
    }

    return (
        <div>
            <h1>Grocery List</h1>
            <ul>
                <li>Milk</li>
                <li>Bread</li>
                <li>Eggs</li>
            </ul>
        </div>
    )
};
이렇게 하면 앱이 복잡해 지더라도 쉽게 이해할 수 있고 만들어 놓은 컴포넌트를 앱 전체가 공유할 수 있으므로 코드의 재사용이 가능해집니다.
