# 조건부 렌더링(Conditional rendering) 알아보기

조건이라고 생각하면 가장 먼저, if문이 떠오릅니다. 

자바스크립트에서 사용한 if문처럼 컴포넌트 안에서 사용하는 방법과 JSX를 사용하여 인라인으로 조건문을 처리하는 방법을 학습해보겠습니다. 

덧붙여, 컴포넌트가 렌더링되는 것을 막는 방법에 대해서도 학습해보도록 하겟습니다.

## 조건문으로 구현하기

아래 코드를 확인하면, UserGreeting과 GuestGreeting이라는 컴포넌트가 만들어진 것을 볼 수 있습니다. 

우리가 알아보고자하는 것은 조건부 렌더링입니다. 즉, 조건에 따라서 렌더링이 되어야 하는 것입니다.

예를 들어서 가장 쉽게 접할 수 있는 로그인 기능을 생각해봅시다. 로그인의 여부에 따라서 사용자에게 보여지는 화면이나 메세지는 달라야 합니다. 

이미 가입된 사용자라면 “어서오세요!” 라는 문구가 나와야 하고, 가입되지 않은 사용자라면 “처음오셨군요! 회원 가입 부탁드려요.” 라는 문구가 나와야 합니다. 

바로 그 컴포넌트가 아래 코드입니다.
```
function UserGreeting(props) { //유저일 때 보여주는 컴포넌트
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) { //게스트일 때 보여주는 컴포넌트
  return <h1>Please sign up.</h1>;
}
```

따라서, 유저일 때는 UserGreeting컴포넌트를 렌더링 해야하고, 유저가 아닐 때는 GuestGreeting컴포넌트를 렌더링해야 합니다. 

이렇게 조건에 따라서 컴포넌트를 다르게 렌더링하는 컴포넌트를 만드는 방법을 알아보겠습니다.

### 1. 조건문 사용하기

조건문 if를 사용하여 렌더링하는 방법을 알아보겠습니다.
```
function Greeting(props) { //인사하는 컴포넌트 선언
  const isLoggedIn = props.isLoggedIn; //props에서 받아온 isLoggedIn값을 inLoggedIn 변수에 할당
  if (isLoggedIn) { //할당한 변수의 값을 if문으로 확인 (= 조건별로 구분하기)
    return <UserGreeting /> //true일 때 실행되는 컴포넌트
  }
  return <GuestGreeting /> //false일 때 실행되는 컴포넌트

  ReactDOM.render(
    //isLoggedIn={true}; 로 하면 어떤 컴포넌트가 실행될지 생각해보세요!
    <Greeting isLoggedIn={false} />, //Greeting이라는 컴포넌트를 불러올 때, isLoggedIn이라는 props를 주고, props의 false 값을 할당합니다.
    document.getElementById('root')
  );
}
```
### 엘리먼트 변수에 따른 조건부 렌더링 실습

if나 조건부 연산자를 활용하여 조건부 렌더링을 제공합니다. 인자값에 따라 다른 컴포넌트를 렌더링할 수 있습니다.

이를 통해 사용자의 동작에 대해 유연한 페이지를 작성합니다.
```
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}
```

```
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);
```

Greeting 컴포넌트의 반환값이 ReactDOM에 렌더링됩니다. 

Greeting 컴포넌트는 props값인 isLoggedIn에 따라 반환하는 컴포넌트가 변경됩니다.

##### 지시사항

if문을 활용하여 사용자의 동작에 따라 출력문구가 바뀌는 페이지를 작성합니다.

1. isToggleOn의 값을 변경하는 handleClick이벤트를 정의합니다.
  - true -> false
  - false -> true
2. 정의한 이벤트를 바인딩합니다.
3. ```<button>```태그에서 이벤트 핸들러를 추가합니다.
4. State 컴포넌트를 정의합니다.
  - isToggleOn을 props로 받습니다.
  - isToggleOn이 참이면 LoginState컴포넌트를 반환합니다.
  - isToggleOn이 거짓이면 LogoutState컴포넌트를 반환합니다.

> Tips : ````this.setState({isToggleOn: !this.state.isToggleOn})``` 을 통해 state를 변경합니다.
바인딩은 constructor()메소드에서 진행합니다.

### 2. element variables

react element를 변수에 저장할 수 있습니다.

아래 코드를 확인하면 LoginButton과 LogoutButton 총 2가지 버튼이 있는 것을 확인할 수 있습니다. 확인하면, 내용만 다릅니다. 

버튼의 내용이 Login이고, Logout이죠. 또 로그인 기능을 생각하며 코드를 살펴봅시다. 만약, 

내가 로그인을 했다면 LogoutButton이 보여야 하고, 로그인을 해야 한다면 LoginButton이 보여야 합니다.
```
function LoginButton(props) { //로그인 버튼
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) { //로그아웃 버튼
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}
```


간편하게 **다른 컴포넌트를 보여주고 싶은 경우에는 변수에 저장**을 하여 보여주는 방법이 있습니다. 

LoginControl이라는 클래스 컴포넌트를 만들다고 가정을 한다면 이 컴포넌트는 로그인 여부에 따라서 판단을 합니다. 

유저가 로그인을 하면 “어서오세요!” 라는 메세지가 보이면서 동시에 로그아웃 버튼이 보여야하고, 로그아웃을 하면 “처음오셨군요! 회원 가입 부탁드려요.” 라는 메세지가 보이면서 동시에 로그인 버튼이 보여야 합니다. 

이러한 로직을 구현한 코드가 아래 코드입니다. 주석과 함께 확인해보세요.
```
class LoginControl extends React.component {
  constructor(props) {
    super(props)
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true})
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false})
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button; //버튼 변수 선언 (바로, 이 변수가 element variables 입니다.) 컴포넌트를 이 변수에 할당할 수 있다는 의미입니다. (어려운 개념이 아니니, 겁 먹지 마세요!)

    if(isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />; //로그인 상태일 경우, button변수에 LogoutButton 엘리먼트를 할당
    } else {
      button = <LoginButton onCLickc={this.handleLoginClick} />; //로그 아웃 상태일 경우, button변수에 LoginButton 엘리먼트를 할당
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} /> //Greeting 컴포넌트를 보여주고 있다.
        {button} //button 엘리먼트를 렌더링하고 있다.
      </div>
    )
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

### 3. JSX로 구현하기

앞서 설명드린 방법은 자바스크립트에 더 가까운 코드라고 생각이 드실 것 입니다. 

이번에는 react의 특징인 JSX를 사용하여 조건부 렌더링하는 방법을 알아보겠습니다.

#### && 연산자 사용하기

&& 연산자는 자바스크립트의 연산자이기 때문에 { }을 사용해야 합니다. 

&&연산자는 리액트 엘리먼트를 렌더링 여부를 결정할 때 사용할 수 있는 간단한 연산자입니다. 

아래 컴포넌트 코드를 보고 어떻게 구현을 하였는지 살펴보겠습니다.

```
function Mailbox(props) { //Mailbox라는 function component 선언
  const unreadMessages = props.unreadMessages; //읽지 않은 메세지 값을 받아 unreadMessages 변수에 할당
/* 조건부 렌더링 부분! */
  return (
    <div>
      <h1>Hello!</h1>
            /*이 부분이 true이면 렌더링, false면 렌더링 하지 않는다.*/
      {unreadMessages.length > 0 && /* unreadMessages 의 길이가 0보다 크면 아래 <h2> 태그를 렌더링 */
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React']; //messages 배열에 3가지 값을 담았습니다.
ReactDOM.render(
  <Mailbox unreadMessages={messages} />, // props 값을 받는다.
  document.getElementById('root')
);
```

#### 조건부 연산자 (?) 활용 실습

조건부 연산자 (?)를 사용하여 if-else문을 한줄로 표현할 수 있습니다. 조건부 연산자는 다음과 같은 결과를 반환하는 연산자입니다.
```
(조건) ? expr1 : expr2
```

- 조건의 결과값이 true인 경우: expr1을 실행합니다.
- 조건의 결과값이 false인 경우: expr2를 실행합니다.

예시
```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```
isLoggedIn의 값이 true라면, ‘currently’문자열을 출력합니다.

isLoggedIn의 값이 false라면, ‘not’문자열을 출력합니다.

##### 지시사항

조건부 연산자를 활용하여 숫자가 양수인지 판단하는 페이지를 작성합니다. 조건에 따라 아래와 같은 결과값을 출력합니다.

- 입력된 숫자 > 0: “양수입니다.”
- 입력된 숫자 <= 0: “양수가 아닙니다.”

1. Check의 props를 변수에 저장합니다.
2. 조건에 따라 적절한 결과값을 출력합니다.
  - 출력 태그는 ```<h2>```태그를 이용합니다.

> Tips : parseInt(숫자로 변경할 문자열, 진법)을 사용해 문자를 숫자로 변환할 수 있습니다.

##### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

function Check(props){

//Check의 props를 변수에 저장합니다.
  const data = parseInt(props.num);
  return(
    <div>
        <h2>{data>0 ? '양수입니다.' : '양수가 아닙니다.'}</h2>
    </div>
  )
}

class InputData extends React.Component {
  state = {
    num: ''
  }
  handleChange = (e) => {
    this.setState({
      num: e.target.value
    })
  }
  render() {
    return (
      <form>
        숫자를 입력하세요: <input
          value={this.state.num}
          onChange={this.handleChange}
        />
        
        {<Check num={this.state.num}/>}
      </form>
      
    );
  }
}

ReactDOM.render(<InputData />,document.getElementById('root'));

serviceWorker.unregister();
```

#### 3항 연산자로 조건부 렌더링 구현하기

3항 연산자로 간단하게 구현할 수 있습니다.
```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
            {/* 중괄호 안에서 isLoggedIn이 true이며 LogoutButton 컴포넌트를 렌더링, false면 LoginButton 컴포넌트를 렌더링 */}
      {isLoggedIn ? ( 
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```
