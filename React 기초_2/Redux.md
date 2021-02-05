# Redux 등장배경

React를 비롯한 JavaScript 어플리케이션을 활용하여 개발을 할 때 필수적으로 따라 올 수 밖에 없는 것이 바로 눈에 보이지 않는 **복잡성**입니다. 

React 뿐만 아니라 프로그램의 복잡성은 개발자와 코드를 관리하는 보안관리자의 사이를 멀어지게 하며 개발자들이 개발을 할 때 코드가 장황해지거나 애플리케이션 시스템을 제어하기가 매우 까다로워집니다.

> Redux는 애플리케이션의 복잡성을 획기적으로 낮춰서 코드가 어떤 결과를 가져올지 예측가능하게 만들어주는 환상적인 도구입니다. 

여러분이 만들게 될 컴포넌트들의 상태관련 로깅들을 다른 파일들로 분리시켜서 효율적으로 관리를 함으로서 코드를 예측가능하게 구현해주는 것입니다. 이 컴포넌트를 분리시키는 것에 대한 설명은 다음 장에서 더 이해하기 쉽게 설명해 드리겠습니다.

## Redux 정의

Redux는 **application 전체의 상태(state)를 편리하게 관리**하기 위해 사용하는 **라이브러리** 중 하나입니다.

여기서 상태(state)란 무슨 뜻일까요?

예를들어 SNS앱에서 현재 사용자가 로그인을 했는지, 어떤 포스트를 읽었는지, 어떤 메시지가 펼쳐져 있는지에 대한 정보를 포함한 것이 사용자의 상태이고 게시글이 어떤 레코드를 가지고 있는지, 언제 수정됐는지 등의 정보를 포함하는 것이 포스팅의 상태입니다. 

리액트는 이 상태를 여러 다른 컴포넌트에 골고루 퍼져있었습니다. Redux는 이 **모든 상태 데이터를 한 객체에 모으게 함으로써 상태를 중앙 집중적으로 관리하고 프로그램 크기가 커져도 애플리케이션 상태를 보는 관점을 단순하게 유지**해 주는것입니다.

## Redux 개념정리

**Redux는 사용률이 높은 상태 관리 라이브러리** 입니다.

앱의 컴포넌트들의 상태 관련 로직은 각각 다른 파일로 분리해서 효율적으로 관리가 가능해집니다

- Redux는 React, Vue, Anguler에서 사용가능
- Vue와 Anguler는 각자의 상태관리 도구가 존재

### Redux는 단방향

양방향으로 데이터가 수정되면 화면도 같이 수정되고 화면을 수정하면 데이터도 같이 수정될 수 있지만 **버그**가 많이 생깁니다. 

이 문제를 해결하기 위해 페이스북에서 flux pattern 개발, flux pattern이 점점 업그레이드 되다가 페이스북 리액트팀의 댄 아브라모프와 앤드류 클락이 Redux를 개발했습니다.

Redux는 앱 전체상태를 단일 스토어로 관리하여 앱 전체를 쉽게 관리할수 있고 디버깅이나 개발자도구를 쉽게 사용할 수 있게 합니다.

### Redux의 리듀서는 순수 함수

Redux의 리듀서는 순수 함수여야 합니다.
여기서 순수함수란 어떤 함수에 **동일한 파라미터를 주었을 때 항상 같은 값을 리턴하고 외부 상태를 변경하지 않는 함수**를 말합니다. 

> 리듀서는 이전의 상태와 액션을 받아서 다음 상태를 반환하는 순수한 함수입니다.

## Redux 의 필요성

React로 application을 만들 때 필수적으로 상태를 관리하는 상황을 마주치는데 기본적으로 state에 기본 값을 지정하고 setState를 사용하여 data를 추가, 제거 그리고 수정합니다. 

독립적인 component내에서 뿐만 아니라 부모-자식, 부모-자식-자식의 자식- 자식의 자식의 자식, 혹은 그 역순과 사돈/팔촌 관계끼리도 state를 공유하고 수정하고 다시 공유할 수 있습니다.

**state를 props로 서로 넘겨주며 data를 공유**하고 **setState를 통해 data를 수정**하는 등 간단한 방법으로 React에서 상태 관리를 할 수 있지만 application의 규모가 복잡해지고 커질수록 상태 관리는 더욱 더 힘들어집니다.

Redux는 **글로벌 상태 관리**를 할 때 굉장히 효과적입니다. 컴포넌트 구조와 관계가 복잡해지면 호출되지않는 컴포넌트를 거쳐가야한다는 것은 렌더링을 다시할 때 비효율적이며 매우 귀찮은 작업이기도 합니다. **상위 컴포넌트에서 props이름을 바꿔 준다면 아래에도 모두 바꿔줘야 하니까요.**

원 하나가 프로그램의 컴포넌트라면 하나의 컴포넌트가 다른 컴포넌트들과 기능을 수행하기 위해서는 보내는 로직 2개과 (→,↓)받는 로직 2개(←,↑) 다 합해서 4개의 로직이 필요합니다. 즉 4개의 컴포넌트일 때는 16개의 로직을, 5개의 컴포넌트일 때는 25개의 로직을, 6개의 컴포넌트일 때는 36의 로직을 작성해야 합니다. Redux가 없는 상태에서 컴포넌트가 하나가 추가될 때마다 우리가 작업해야되는 양은 이렇게 기하급수적으로 늘어납니다. 만약에 프로그램안에 있는 컴포넌트가 200개라면 40000개의 코드를 작성해야 한다는 것입니다.

하지만 Redux가 있다면 중앙 집중적인 스토어를 이용할 수 있습니다.

이제 이렇게 Redux를 도입하면 컴포넌트에 필요한 로직의 개수가 1:2로 획기적으로 줄었습니다.
4개의 컴포넌트일 때 8개의 로직을, 5개의 컴포넌트일 때 10개의 로직을 , 6개의 컴포넌트일 때 12개의 로직으로 구현이 가능합니다.

훨씬 단순한 코드로 아주 복잡한 일을 할 수 있도록 해줍니다.

다음 장에서는 실습으로 Redux를 도입하면 코드가 어떻게 달라지는지 비교해봅시다.

## Redux 및 Redux 확장 프로그램 설치하기

Redux를 직접 설치하고 적용해봅시다.

### 설치
```
npm install --save redux react-redux
```

yarn add redux react-redux
redux를 프로젝트에 추가한다면

$ npm i redux
리액트 프로젝트에 Redux를 추가한다면

$ npm i redux
$ npm i react-redux
기본적으로 자바스크립트로 작성된 라이브러리에서 모두 사용 가능한 redux와
리액트와 Redux의 공식 바인딩 패키지인 react-redux를 함께 설치해줍니다.

그 다음은 store를 생성하기전에 프로젝트를 진행하는 도움이 되는 몇가지 library을 설치해주세요.

- yarn add redux-thunk
- yarn add redux-logger --dev
- yarn add react-router-dom react-router-redux history
- yarn add redux-devtools-extension --dev
Redux 확장프로그램 설치하기
Redux의 개발자 도구(redux-devtools 확장 프로그램)를 사용하면 현재 스토어의 상태를 개발자 도구에서 조회 할 수 있고 지금까지 어떤 액션들이 디스패치 되었는지, 그리고 액션에 따라 상태가 어떻게 변화했는지 확인할 수 있습니다. 추가적으로 액션을 직접 디스패치 할 수도 있습니다.

1) 먼저 크롬 웹스토어로 가면 Redux DevTools 이란 크롬 확장 프로그램을 받을 수 있습니다. 여기서 확장 프로그램을 설치해줍니다.
설치 후 아래와 같이 스토어(Store) 생성 시 + window.REDUX_DEVTOOLS_EXTENSION && window.REDUX_DEVTOOLS_EXTENSION() 를 추가해주면 크롬 개발자 모드에서 Redux의 상태 변화를 볼 수 있습니다.

const store = createStore(
   reducer, /* preloadedState, */
+  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
 );
2) 다음은 프로젝트에 redux-devtools-extension라이브러리를 설치해줍니다.

//yarn으로 설치하는 경우
yarn add redux-devtools-extension
또는

//npm으로 설치하는 경우
npm add redux-devtools-extension
3) 다음에는 index.js를 수정해주면 됩니다.

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import rootReducer from './modules';
import { composeWithDevTools } from 'redux-devtools-extension'; // Redux 개발자 도구

const store = createStore(rootReducer, composeWithDevTools()); // 스토어 생성
// composeWithDevTools 함수로 Redux 개발자 도구 활성화

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

serviceWorker.unregister();
이렇게 하시면 크롬의 개발자도구에서 redux를 확인하실 수 있습니다.
