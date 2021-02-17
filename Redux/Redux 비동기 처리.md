# Redux 미들웨어

여러분은 [Redux 기초 I] 에서 리액트 생태계에서 가장 사용률이 높은 상태관리 라이브러리인 Redux의 필요성을 알게 되었고 redux로 웹의 상태관리를 해보았습니다.

이번 과목에서는 Redux가 지니고 있는 핵심 기술인 Redux 미들웨어의 개념을 배워봅시다.
Redux는 굉장히 코드가 짧고 가벼운 아키텍처를 가지고 있습니다. Redux는 미들웨어라고 부르는 확장 기능을 지원합니다. 

기본적으로 제공되는 미들웨어 외에 추가로 설치하여 사용해야하는 미들웨어들이 많이 공개되어있는데 이번 장에서는 이 미들웨어 중에서 대표적인 Redux-thunk를 적용하는 기본적인 방법부터 만드는 방법까지 알아봅니다.

Redux 미들웨어를 사용하면 액션이 디스패치 된 다음, 리듀서에서 해당 액션을 받아와서 업데이트하기 전에 추가적인 작업을 할 수 있습니다.

> 액션 - 미들웨어 - 리듀서 - 스토어

## Redux 미들웨어란?

Redux 미들웨어는 리덕스의 기능을 확장할 때 사용하는 기능입니다. 구체적인 예를 몇 가지 들어보겠습니다.

- 액션 로그를 출력하는 미들웨어
- 비동기 처리를 하게 해주는 미들웨어 (redux-thunk 적용)
- 크래시 리포트를 전송하는 미들웨어
- 라우팅을 위해 사용하는 미들웨어

### 이러한 미들웨어가 하는 일

- 특정 조건에 따라 액션이 무시되게 만들 수 있습니다.
- 액션을 콘솔에 출력하거나, 서버 쪽에 로깅을 할 수 있습니다.
- 액션이 디스패치 됐을 때 이를 수정해서 리듀서에게 전달되도록 할 수 있습니다.
- 특정 액션이 발생했을 때 이에 기반하여 다른 액션이 발생되도록 할 수 있습니다.
- 특정 액션이 발생했을 때 특정 자바스크립트 함수를 실행시킬 수 있습니다.

이 미들웨어들은 여러 가지를 조합해서도 사용할 수 있습니다. 리덕스만으로는 조금 불편한 기능을 수많은 개발자들이 미들웨어로 조합해서 만들어 공개하고 있습니다.

미들웨어는 독립적이므로 여러 미들웨어를 사용해도 서로에게 영향을 미치지 않습니다. 그래서 필요한 만큼 여러 개를 조합해서 사용 가능합니다.

## Redux 미들웨어의 구조

미들웨어는 Redux 흐름에서 **액션이 디스패치되는 시점부터 reducer로 처리가 이동할 때까지의 처리를 확장**합니다.
간단하게 미들웨어가 어떠한 형태를 가지는지 살펴봅시다.
```
const middleware = store => next => action {
    console.log('이곳은 "액션이 디스패치 되고 리듀서로 처리가 이동하는 시점의 부분"입니다.');
    const result = next(action);
    return result;
};
```

여기 화살표가 많아서 당황하셨을 수도 있습니다. 이는 “화살표 함수로 result를 리턴하는 함수를 리턴하는 함수를 리턴하는 함수” 를 나타냅니다. 각 함수의 스토어, next, 액션 에서 리턴하는 리턴 값입니다.

위의 리덕스 미들웨어를 일반적인 함수 리터럴로 나타낸다면 이런 형태를 갖게됩니다.
```
const middleware = function(store) {
    return function(next) {
        return function(action) {
            console.log('이곳은 "액션이 디스패치되고 리듀서로 처리가 이동하는 시점의 부분" 입니다.' );
            const result = next(action);
            return result;
        }
    }
};
```
여기서 result는 각 함수의 스토어, next, action에서 리턴하는 리턴 값입니다.

# 동기와 비동기

## 비동기 처리란?

비동기 처리는 말 그대로 동기적이지 않은 처리를 나타냅니다. 동기적인 처리란 작성된 순서대로 실행되는 처리라고 할 수 있습니다. 따라서 비동기 처리란 작성된 순서대로 실행되지 않는 처리라고 할 수 있습니다.

현실세계에서 적용해서 생각해봅시다. 만약 여러분이 음식점에서 피자를 배달하는 배달부라고 가정해봅시다.
시킨 사람이 피자를 다 먹을 때까지 기다렸다가 식사가 끝난 후에야 그 그릇을 가지고 다음 장소로 이동할 수 있다면 어떨까요? 동기코드에서는 시킨 사람이 피자를 먹는 동안 배달부는 아무 일도 할 수 없고 시간당 배달할 수 있는 피자수는 급격하게 줍니다. 비동기 코드에서는 주문했던 배달이 끝나고 그 식사가 끝나기 전에 수행될 일을 미리 알려주고 배달부는 다음 장소로 이동합니다.

동기(Sync) - 작업을 하나의 Thread에서 하도록 시킨 후 그 작업이 끝나길 “기다리고“ 다음 일을 진행한다.

비동기(Async) - 작업을 다른 Thread에서 하도록 시킨 후, 그 작업이 끝나길 “안 기다리고“ 다음 일을 진행한다.

비동기라는 개념이 일반적으로 필요한 경우는 대부분 서버와의 통신(네트워크 작업)이나 외부 API에 접근하는 경우를 들 수 있습니다.
비동기 처리를 실행한 이후에 원하는 코드를 실행하고 싶다면 콜백, Promise, Async/Await 등의 방법을 사용합니다.
```
//동기적인 예
console.log('start');
const a = 100;
const b = 200;
const sum = a + b;
console.log('합계 = ${sum}');
console.log('finish');

/*
실행결과
start
합계 = 300
finish
*/
```

```
//비동기 처리 예
console.log('start');
setTimeout(() => {
const a = 100;
const b = 200;
const sum = a + b;
console.log('합계 = ${sum}');
}, 1000);
console.log('finish');

/*
실행결과
start
finish
합계 = 300
*/
```

이렇게 비동기 처리를 했더니 finish 가 먼저 출력됐습니다. setTimeout 함수 내부의 처리는 비동기적으로 실행되므로 처리가 완료되기를 기다리지 않고 finish를 출력하는 줄이 먼저 실행되는 것입니다. 이 처럼 처리가 완료되기를 기다리지 않고 실행되는 방식을 비동기 처리라고 합니다. setTimeout 외의 비동기 처리의 예로는 API요청, 데이터베이스 접속 등이 있습니다.

# redux-thunk

비동기 작업에 관련된 미들웨어 라이브러리는 redux-thunk, redux-saga, redux-observable, redux-promise-middleware 등이 있습니다. 리덕스를 사용하는 애플리케이션에서 비동기 작업을 처리할 때 가장 기본적인 방법은 redux-thunk라는 미들웨어를 사용하는 것입니다. 

redux-thunk는 리덕스를 개발한 Dan Abramov 가 만든 것이며, redux 공식 매뉴얼에서도 이 미들웨어를 사용하여 비동기 작업을 다룹니다. redux-thunk를 사용하면 액션 객체가 아닌 함수를 디스패치 할 수 있습니다.

## thunk란?

thunk라는 단어가 굉장히 낯선 분들도 있을 것입니다.
thunk는 “생각한다”라는 의미를 가진 “think”의 비표준 과거형 단어입니다. 프로그래밍 세계에서는 “필요할 때 처리한다”라는 의미로 많이 사용됩니다. thunk 미들웨어는 redux-thunk라는 이름으로 npm에 올라가 있습니다.

간단히 말해 thunk란 특정 작업을 나중에 하도록 미루기 위해서 함수 형태로 감싼 것을 칭합니다.

예를 들어서 여러분들이 1 + 1을 지금 당장 하고 싶다면 이렇게 하겠죠?
```
const x = 1+1;
```
하지만 다음과 같이 할 수도 있습니다.
```
const foo = () => 1+1;
```
이렇게 하면, 1 + 1의 연산이 코드가 실행될 때 바로 이뤄지지 않고 나중에 foo()가 호출되어야만 이뤄집니다.

redux-thunk는 뭘 하는 미들웨어(액션과 리듀서 사이의 중간자) 일까요?

## redux-thunk가 하는일

- pure javascript object 형태로 action을 반환하던 actionCreator에서 함수로 래핑한 형태로 반환 가능하게 함
- actionCreator가 함수를 반환하는데, 이 함수는 dispatch와 getState를 파라미터로 갖고 내부에서 비동기적으로 action을 dispatch 가능
```
const INCREMENT_COUNTER = 'INCREMENT_COUNTER'

function increment() {
    return {
        type: INCREMENT_COUNTER,
    }
}

function incrementAsync() {
    return dispatch => {
        setTimeout(() => {
            // Yay! Can invoke sync or async actions with `dispatch`
            dispatch(increment())
        }, 1000)
    }
}
```

가장 간단히 설명하자면, 이 redux-thunk는 객체 대신 함수를 생성하는 액션 생성 함수를 작성할 수 있게 해 줍니다.

일반적인 dispatch 예시
```
store dispatch({type: 'DO_SOMETHING' });
```

Redux-Thunk dispatch 예시
```
store.dispatch((dispatch,getState) => {
   dispatch ({type: DO_SOMETHING });
     });
```
store.dispatch에 함수가 전달되면 next 함수를 실행하지 않고, 매개변수로 전달된 함수를 실행합니다. 이때 매개변수에 store.dispatch와 store.getState를 전달합니다. 액션으로 전달된 함수 내부에서 dispatch를 사용하면 원하는 시점에 디스패치할 수 있습니다. 비동기적으로 실행되는 API 요청의 콜백 또는 setTimeout 내부에서도 디스패치할 수 있게 되는 것입니다.

## redux-thunk 설치
```
npm install redux-thunk
```
또는
```
$ yarn add redux-thunk
```

redux-thunk은 미들웨어이기 때문에 storeFactory와 함께 사용해야 합니다. 먼저 index.js 파일의 앞부분에 redux-thunk를 임포트 하세요.
```
import thunk from 'redux-thunk' 

Redux Thunk, use applyMiddleware():

import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers/index';

// Note: this API requires redux@>=3.1.0
const store = createStore(rootReducer, applyMiddleware(thunk));
```

# redux-thunk를 이용한 비동기 처리

## redux-thunk 적용(1) - 콜백으로 비동기처리하기

thunk 미들웨어 적용 (store.js)
```
import { createStore, applyMiddleware } from 'redux';
import logger from 'redux-logger';
import thunk from 'redux-thunk';
import reducers from './reducers';


const middlewares = { logger, thunk];

const store = createStore (
reducers,
applyMiddleware(...middlewares)
);

export default store;
```

이렇게 thunk 미들웨어를 적용해서 비동기적으로 실행되는 액션을 작성해봤습니다. 그럼 실제로 코드를 실행해보고 비동기 액션클리에이터와 동기 액션크레이터가 어떻게 작동하는지 살펴보겠습니다. 동기적인 엑션크레이터는 매개변수로 Todo의 타이틀을 받고 자동으로 유니크ID를 생성하고 액션 객체를 리턴합니다.
비동기 액션크레이터를 사용하면 함수를 리턴합니다. 이때 리턴하는 함수는 dispatch 함수와 getState함수를 매개변수로 갖습니다.
```
import * as types from '../types/todo';
//동기 액션크리에이터
export function addTodo(title) {
return { 
type: types.ADD_TODO,

payload: {
id: shortid.generate(),
title,
},
};
}

//비동기 액션크리에이터
export function asyncAddTodo(title) {
return (dispatch, getState) => {
setTimeout(() => {
 setTimeout(() => {
 dispatch(addTodo(title));
 }, 1000);
 };
 }
 ```

## redux-thunk 적용(2) - 카운터 딜레이하기

thunk 함수를 만들고, setTimeout를 사용하여 액션이 디스패치되는 것을 1초씩 딜레이 시켜봅시다.

increaseAsync와 decreaseAsync라는 thunk 함수를 만들겠습니다.
```
// 액션 타입
const INCREASE = 'INCREASE';
const DECREASE = 'DECREASE';

// 액션 생성 함수
export const increase = () => ({ type: INCREASE });
export const decrease = () => ({ type: DECREASE });

// getState를 쓰지 않는다면 굳이 파라미터로 받아올 필요 없습니다.
export const increaseAsync = () => dispatch => {
  setTimeout(() => dispatch(increase()), 1000);
};
export const decreaseAsync = () => dispatch => {
  setTimeout(() => dispatch(decrease()), 1000);
};

// 초깃값 (상태가 객체가 아니라 그냥 숫자여도 상관 없습니다.)
const initialState = 0;

export default function counter(state = initialState, action) {
  switch (action.type) {
    case INCREASE:
      return state + 1;
    case DECREASE:
      return state - 1;
    default:
      return state;
  }
}
```
이제 컨테이너 컴포넌트를 다음과 같이 수정해보세요.
```
import React from 'react';
import Counter from '../components/Counter';
import { useSelector, useDispatch } from 'react-redux';
import { increaseAsync, decreaseAsync } from '../modules/counter';

function CounterContainer() {
  const number = useSelector(state => state.counter);
  const dispatch = useDispatch();

  const onIncrease = () => {
    dispatch(increaseAsync());
  };
  const onDecrease = () => {
    dispatch(decreaseAsync());
  };

  return (
    <Counter number={number} onIncrease={onIncrease} onDecrease={onDecrease} />
  );
}

export default CounterContainer;
```
카운터의 버튼들을 클릭할 때 액션 디스플레이가 디스패치된 걸 (버튼을 클릭한 다음 1초 후에 결과가 나오는 것)을 확인할 수 있습니다.

- 동기적인 액션크리에이터는 일반적인 액션을 리턴합니다.
- thunk 미들웨어를 사용하면 일반적인 액션 객체가 아닌 함수를 리턴할 수 있습니다.
- 비동기적인 처리를 하는 가장 기본적인 방법은 setTImeout()을 사용하는건데 setTimeout은 비동기적으로 실행되므로 처리가 완료되기를 기다리지않고 finish를 출력하는 줄이 먼저 실행됩니다.
- 비동기적인 액션크리에이터는 함수를 리턴한다.

# Promise 란?

Promise는 자바스크립트 비동기 처리에 사용되는 객체입니다.
Promise 객체는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타냅니다.

Promise는 프로미스가 생성될 때 꼭 알 수 있지는 않은 값을 위한 대리자로, 비동기 연산이 종료된 이후의 결과값이나 실패 이유를 처리하기 위한 처리기를 연결할 수 있도록 합니다. 

Promise를 사용하면 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있습니다. 다만 최종 결과를 반환하지는 않고, 대신 Promise를 반환해서 미래의 어떤 시점에 결과를 제공합니다.

프로미스는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용합니다. 일반적으로 웹 애플리케이션을 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 아래와 같은 API를 사용합니다.
```
$.get('url 주소/products/1', function(response) {
  // ...
});
```
위 API가 실행되면 서버에다가 ‘데이터 하나 보내주세요’ 라는 요청을 보내죠. 그런데 여기서 데이터를 받아오기도 전에 마치 데이터를 다 받아온 것 마냥 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 뜹니다. 이와 같은 문제점을 해결하기 위한 방법 중 하나가 프로미스입니다.

## 프로미스의 3가지 상태(states)

프로미스를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 프로미스의 상태(states)입니다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미합니다. new Promise()로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖습니다.

- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

### Pending(대기)

먼저 아래와 같이 new Promise() 메서드를 호출하면 대기(Pending) 상태가 됩니다.
```
new Promise();
```

new Promise() 메서드를 호출할 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자는 resolve, reject입니다.
```
new Promise(function(resolve, reject) {
  // ...
});
```

### Fulfilled(이행 또는 완료)

여기서 콜백 함수의 인자 resolve를 아래와 같이 실행하면 이행(Fulfilled) 상태가 됩니다.
```
new Promise(function(resolve, reject) {
  resolve();
});
```
그리고 이행 상태가 되면 아래와 같이 then()을 이용하여 처리 결과 값을 받을 수 있습니다.
```
function getData() {
  return new Promise(function(resolve, reject) {
    var data = 100;
    resolve(data);
  });
}
// resolve()의 결과 값 data를 resolvedData로 받음
getData().then(function(resolvedData) {
  console.log(resolvedData); // 100
});
```
Promise의 개념과 redux-thunk 적용 방법에 대한 더 자세한 설명이 필요하시다면 다음 링크들을 참조하세요.

- Promise 개념<https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Using_promises>
- Promise 적용 방법<https://react.vlpt.us/redux-middleware/05-redux-thunk-with-promise.html>

Redux-thunk를 사용할 경우의 Promise를 사용하는 예를 살펴봅시다.

#### Promise의 예 (1)
```
const sleep1000ms = () => {
    return new Promise(resolve => {
            setTimeout(() => {
                resolve();
                } , 1000);
            });
};

export function addTodo(title) {
return {
    type: types.ADD.TODO,
        payload: {
            id: short.id.generate(),
            title,
        },
    };
}

//Promise 버전
export function asyncAddTodo(title) {
 return (dispatch) => {
         sleep1000ms().then((=> {
                 dispatch(addTodo(title));
                 });
            };
}
```

#### Promise의 예 (2)

다음은 promise를 카운터에 적용했을 때 해당 숫자가 number가 아니면 reject(실패), 5 이상일 경우에는 true를 반환하고 그 외의 경우에는 false를 반환합니다.
```
export const checkNumber = async number => { //넘버를 체크해서 Promise를 리턴
  await sleep(500) 
  return new Promise((resolve, reject) => { 
    if(isNaN(number)) reject(`${number} is NaN`)
    if(number >= 5) resolve(true)
    else resolve(false)
  })
}
```

Promise를 다루는 Redux 모듈을 다룰 땐 다음과 같은 사항을 고려해야합니다.

- Promise가 시작, 성공, 실패했을때 다른 액션을 디스패치해야합니다.
- 각 Promise마다 thunk 함수를 만들어주어야 합니다.
- 리듀서에서 액션에 따라 로딩중, 결과, 에러 상태를 변경해주어야 합니다.
