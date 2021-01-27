# 이벤트 처리하기

이벤트란 유저 행동의 결과 혹은 시스템에 의해 발생되는 일을 말합니다.

앞서 배운 HTML에서 사용한 이벤트를 React에서도 동일한 작업을 수행 할 수 있습니다.

HTML에서 사용했던 이벤트를 다시 확인해보세요.

우리가 배운 click 이벤트나 change 이벤트, mouseover 이벤트 등 React는 HTML과 동일한 이벤트를 가지고 있습니다.

## React 이벤트 특징

1. 리액트에서 이벤트의 이름은 **카멜(Camel) 표기법**으로 사용합니다.

여기서 나오는 카멜 표기법에서 카멜은 ‘낙타’ 라는 의미입니다. 말그대로 낙타의 등모습을 닮았습니다. 

카멜표기법은 두 단어로 이루어진 단어에서 **두 번째 단어의 시작을 대문자로 표기**하는 것입니다. 

예를 들어 onclick으로 표기하는 것이 아니라 onClick으로 표기하는 것입니다.
```
<input type = "text"
    name = "message"
    placeholder = "input message"
    onchange={ // 🚨 이렇게 작성하면 안됩니다!!! 🚨→ onChange로 수정해야 합니다.
        (e) =>{
        // console.log(e);
        console.log(e.target.value);
            this.setState({
            message:e.target.value
            })
        }
    }
    value = {this.state.message}
/>
```

2. 이벤트에 실행할 코드 전달 (X) **함수 형태의 객체를 전달 (O)**

이벤트를 실행할 코드를 그대로 전달하는 것이 아니라 아래 onClick처럼 함수의 형태로 객체를 전달합니다.
```
<button onClick={
    ()=>{
        this.setState({
        message : ''
        })
    }
}>
```

3. DOM요소에만 이벤트 설정 가능

직접 만든 리액트 컴포넌트에는 이벤트를 자체적으로 설정할 수 없습니다. 

```<div> <button> <p> <input>``` 등 DOM요소에만 이벤트를 사용할 수 있습니다.

아래와 같이 직접 만든 ```<EventPractice>```에는 이벤트를 사용해도 적용이 되지 않습니다.

```
render() {
    return (
        <EventPractice onLoad={
            ()=>{
            console.log("test");
            }
        }/>
    );
}
```

### 리액트에서의 이벤트 실습

이벤트란 사용자의 행동에 반응하는 기능을 정의하는 것을 의미합니다. 이벤트의 종류는 다음과 같으며, 이 외의 다양한 이벤트가 존재합니다.

- Keyboard Events
- Focus Events
- Mouse Events
- Touch Events
- UI Events

React에서 이벤트를 처리할 때 몇가지 유의사항이 있습니다.

- React의 이벤트는 카멜 케이스로 정의합니다.
```
onClick={buttonclickevent}(X)
onClick={buttonClickEvent}(O)
```

- 문자열이 아닌 JSX 함수명으로 전달합니다.
```
onClick="함수명()" (X)
onClick={함수명} (O)
```

> 이벤트 등록 방법

1. function키워드를 사용해 이벤트 함수를 작성합니다.
2. ```onClick={함수명}```으로 등록한 이벤트를 호출합니다.
```
function ActionLink() {
  function handleClick(e) {
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

> 코드 설명 : ```handleClick(e)```: 클릭 시, console창에 문구를 출력하는 이벤트 함수

#### 지시사항

버튼 클릭 시 경고창을 띄우는 페이지를 작성합니다. 출력문구는 하단의 출력결과와 동일합니다.

1. ActionLink 컴포넌트 내에 이벤트 함수를 정의합니다.
2. ```<a>```태그에 클릭 이벤트를 등록합니다.

> Tips : 경고창을 띄우기 위해 alert("출력 내용");함수를 활용합니다. 이벤트 등록은 onClick 속성을 활용합니다.

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';


function ActionLink() {
  //이벤트를 등록합니다.
    function onClick(e) {
        alert("버튼이 클릭되었습니다.")
    }
  //a 태그에 이벤트를 등록합니다.
    return (
    <a href="#" onClick={onClick}>
        Click me
    </a>
    );
}

ReactDOM.render(<ActionLink />, document.getElementById('root'));

serviceWorker.unregister();
```

## 이벤트 작성하기

function키워드를 사용해 이벤트 함수를 작성합니다.

```onClick={함수명}``` 으로 등록한 이벤트를 호출합니다.

```
function ActionLink() {
  function handleClick(e) { // 클릭 시, console창에 문구를 출력하는 이벤트 함수
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

### 하이퍼링크 Default 설정 실습

React에서 이벤트가 실행될 때, 페이지가 자동으로 새로고침 됩니다. 이를 방지하기 위해서 e.preventDefault()를 명시적으로 호출해야 합니다.

아래 코드를 보시면 클릭 시, href로 이동하라는 동작이 있습니다.
```
<a href="#" onClick={handleClick}>
    Click me
</a>
```

위 코드를 동작하지 않고 onClick에 넘겨준 것만 실행되게 하기 위해선 preventDefault를 사용합니다.

```
function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
}
```

> Tips : ```<a href ="#">```는 링크를 설정하지 않은 상태이기 때문에 현재 페이지로 이동하여 새로고침 됩니다. 이를 방지하는 것이 ```e.preventDefault()```입니다.

> 클래스 컴포넌트에 이벤트 정의

클래스 컴포넌트에 이벤트를 정의하는 방법은 다음과 같습니다.

1. constructor()와 render()사이에 이벤트를 정의합니다.
```
이벤트 명 = () =>{
 //이벤트 기능
}
```

2. constructor()에서 정의한 이벤트를 바인딩합니다.
```
this.이벤트명 = this.이벤트명.bind(this);
```

3. render()내에서 이벤트를 호출합니다.
```<button onClick={this.이벤트명}>```

#### 지시사항

클래스 컴포넌트에서 이벤트를 등록합니다. 버튼 클릭 시, off가 출력되도록 페이지를 작성합니다.

1. 버튼 클릭시 isToggleOn의 값을 false로 변환하는 이벤트를 작성합니다.
  - 이벤트 명은 handleClick으로 정의합니다.
2. 정의한 이벤트를 바인딩합니다.
3. ```<button>```태그에서 이벤트를 호출합니다.

> Tips : state의 값을 변경하기 위해 setState()를 사용합니다. this.setState({isToggleOn: false});
바인딩은 constructor()메소드에서 진행합니다.

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    //정의한 이벤트를 바인딩합니다.
    this.handleClick = this.handleClick.bind(this);
    }

    handleClick = (e) => {
        e.preventDefault();
        this.setState({isToggleOn: false});
    }

    render() {
        return (
        //button 태그에 handleClick이벤트를 등록합니다.
        <button onClick={this.handleClick}>
            {this.state.isToggleOn ? 'ON' : 'OFF'}
        </button>
        );
    }
}

ReactDOM.render(<Toggle />, document.getElementById('root'));

serviceWorker.unregister();
```

## 이벤트 핸들링 하기

1. 함수로 작성하여 핸들링 하기

함수의 형태로 객체를 넘기기 때문에 함수 형태로 작성해야 합니다.

```
//버튼 클릭 시, 실행되는 이벤트 함수
<button onClick={
    ()=>{
        alert(this.state.message);
        this.setState({
            message : ''
        })
    }
}>
</button>
```

2. 함수 미리 작성 후, 핸들링

미리 작성한 함수를 전달하여 핸들링도 가능합니다. 생성자 함수에서 만들어 놓은 함수를 바인딩 해줘야 합니다.

> 바인딩이란? react 컴포넌트에 이벤트를 연결하는 것을 의미합니다.
```
constructor(props){
    super(props);
    this.handleClick = this.handleClick.bind(this);
}

//버튼 클릭 시, 실행되는 이벤트 함수
handleClick(){
    console.log("message == ",this.state.message);
    this.setState({
            message : ''
    })
}
```


## 이벤트 핸들러에 인수 전달하기

보통 반복문 안에서 id값을 추가 인수로 전달해야 하는 경우가 있습니다.
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

위 코드에서 화살표 함수 id값을 부여할 때, event를 e로 전달해주어야 합니다. 하지만 두번째 bind()를 사용하는 경우, event를 따로 전달하지 않아도 자동으로 전달됩니다.
