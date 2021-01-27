# 컴포넌트의 재사용

컴포넌트를 가지고 합성 및 추출하는 방법에 대해 알아봅시다. 

React에서는 컴포넌트를 적절히 합성하고 추출하여 재사용하는 것이 좋습니다. 

코드의 재사용이 중요한 이유는 같은 동작을 하는 코드를 여러 번 작성한다면 코드의 가독성이 떨어지고 다른 사람이 보기에 이해하기가 어려워집니다. 

또한 코드를 수정해야 할 때 여러 곳에 작성된 모든 코드를 수정하는 것은 매우 번거로운 일입니다. 

따라서 가능한한 **재사용 가능하도록 컴포넌트를 만들어야** 합니다.

**컴포넌트 합성**을 이용하면 작은 기능을 하는 컴포넌트를 결합하여 더 복잡한 기능을 구축할 수 있습니다. 

또한 **컴포넌트 추출**을 통해서는 여러 기능을 하는 컴포넌트를 작게 나눌 수 있습니다. 

컴포넌트는 **기능이 작을수록 재사용이 쉽기 때문에** 컴포넌트의 합성과 추출이 중요합니다. 

아래 예시와 함께 어떻게 하는 것인지 살펴볼까요?

## 컴포넌트 합성

**컴포넌트 안에서 다른 컴포넌트를 참조**하는 것이 가능합니다. 아래 코드를 살펴볼까요? 

Question 클래스에서 Elice 클래스를 참조하고 있습니다. 참조 방식은 지금까지 사용된 것과 동일하게 DOM 태그를 이용하면 됩니다. 

렌더링 할 때도 마찬가지로 DOM 태그를 이용해 호출하고 있습니다.
```
class Elice extends React.Component { # 클래스 컴포넌트
  render() {
    return <h2>I am a elice!</h2>;
  }
}

class Question extends React.Component { # 클래스 컴포넌트
  render() {
    return (
      <div>
      <h1>Who are you?</h1>
      <Elice /> # 클래스 컴포넌트 안에서 다른 컴포넌트 호출
      </div>
    );
  }
}
```

### 컴포넌트 합성 실습

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//함수 컴포넌트를 사용하여 Subject컴포넌트를 정의합니다. Props와 표현식을 이용해 name 변수를 나타내세요.
function Subject(props) {
    return <h3>React를 이해하기 위해서는 {props.name}을(를) 알아야 합니다.</h3>
}

// Subject을 여러번 호출하는 Curriculum 컴포넌트를 작성합니다.
function Curriculum() {
  return (
    <div>
        <Subject name="HTML" />
        <Subject name="CSS" />
        <Subject name="JavaScript" />
    </div>
  );
}

//Curriculum을 ReactDOM과 렌더링합니다.
ReactDOM.render(<Curriculum />, document.getElementById('root'));


serviceWorker.unregister();
```

ReactDOM.render(<Question />, document.getElementById('root'));

## 컴포넌트 추출

한 컴포넌트가 **복잡하다면 일부를 추출해서 분리**하는 것이 가독성이 좋고 코드 재사용이 용이합니다. 

만약 아래와 같은 댓글에 대한 컴포넌트가 있다고 해봅시다.
```
function Comment(props) {
  return (
    <div className="Comment"> # 댓글의 내용과 날짜를 띄우는 Comment
      <div className="UserInfo"> # 사용자 정보를 띄우는 UserInfo
        <img className="Avatar" # 사용자의 이미지를 띄우는 Avatar
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name"> 
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text"> 
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
댓글에는 사용자의 이미지를 띄우는 Avatar와 사용자 정보를 띄우는 UserInfo, 그리고 댓글의 내용과 날짜를 띄우는 Comment에 대한 요소로 이루어져 있습니다. 이를 3개의 컴포넌트로 아래처럼 나눌 수 있습니다.

1. 먼저 이미지를 띄우는 부분을 Avatar 컴포넌트로 분리합니다.
```
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    /> # 이미지 태그를 닫는 /입니다. 컴포넌트를 호출하는 /가 아닙니다.
  );
}
```

2. 그리고 사용자 정보를 띄우는 부분은 UserInfo 컴포넌트로 분리합니다.
```
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} /> # 컴포넌트 호출
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```

마지막으로 댓글의 내용과 날짜를 띄우는 부분은 Comment 컴포넌트에 남겨둡니다. 

처음 한 컴포넌트에 모든 내용이 있는 것보다, Comment 컴포넌트가 간단해진 것을 볼 수 있습니다.
```
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} /> # 컴포넌트 호출
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

# Props

앞에서 간단히 설명했듯이 Props는 **컴포넌트로 전달되는 매개변수**라고 생각하시면 됩니다. 쉽게 생각하면 함수의 매개변수라고 생각해도 좋습니다. 

**컴포넌트에서 어떤 값을 전달받아 처리하고 싶다면 Props**를 이용해야 합니다. 그리고 **컴포넌트를 호출할 때 Props를 넘겨줘야 합니다.** 

마치 함수 호출 시 매개변수를 전달하는 것처럼요.

아래 예제를 살펴보며 봅시다. Props는 **HTML 속성을 통해 컴포넌트로 전달***됩니다. 

그리고 사용할 때는 **중괄호를 이용해 표현하며 ```this.props.속성```과 같은 형태로 호출**됩니다.
```
const element = <Introduce name="Elice" />;
```
```
class Introduce extends React.Component {
  render() {
    return <h2>I am a {this.props.name}!</h2>;
  }
}
```
> 단, 위의 예제는 클래스형 컴포넌트이고 **함수형 컴포넌트에서 사용할 때는 this를 붙이지 않는 것에 유의하세요.**


## 컴포넌트 추출 실습

컴포넌트를 활용하여 기능을 모듈화 하면 다음과 같은 이점이 있습니다.

- 코드 유지보수성이 향상됩니다.
- 코드 재사용이 용이합니다.
- 가독성 향상됩니다.

아래에 할 일에 대해 반환하는 Comment 컴포넌트가 있습니다.

### 컴포넌트 추출 예시
```
function Comment(props){
    return(
        <div>
            <div className="UserInfo"> {props.name}님의 할일 </div>
            <div className="Todo">
                <div>{props.todo.task1}</div>
                <div>{props.todo.task2}</div>
            </div>
        </div>
    );
}
```

위의 컴포넌트를 3개의 컴포넌트로 분리할 수 있습니다.

1. 값을 출력하는 컴포넌트
```
function Comment(props){
    return(
        <div>
          <UserInfo name={props.name}/>
          <Todo todo={props.todo}/>
        </div>
    );
}
```

2. 할 일을 반환하는 컴포넌트
```
function Todo(props) {
  return (
    <div className="Todo">
      <div>{props.todo.task1}</div>
      <div>{props.todo.task2}</div>
    </div>
  );
}
```

3. 유저의 정보를 반환하는 컴포넌트
```
function UserInfo(props) {
  return (
    <div>{props.name}님의 할일 </div>
  );
}
```

위의 예시를 참고하여 주어진 컴포넌트를 직접 세부적으로 추출하여 코드를 간결하게 변경해봅시다.

#### 지시사항

1. 추출할 컴포넌트와 변수에 대한 정보는 다음과 같습니다.

- UserInfo: user의 이름(name), 나이(age)를 출력하는 컴포넌트
- Comment: 넘겨 받은 text, 즉 한 줄 설명을 출력하는 컴포넌트
- Profile: UserInfo, Comment 컴포넌트를 호출하는 컴포넌트
- comment: user 데이터를 저장하는 변수

아래의 Comment 컴포넌트를 참고하여 추출할 컴포넌트를 완성하세요.
```
function Comment(props) {
    return (
      <div className="Comment">
        <div className="UserInfo">
            <div> 이름: {props.user.name}</div>     
            <div> 나이: {props.user.age}</div>  
        </div>
        <div className="Comment-text">
          <div className="Comment">문구: {props.text}</div>
        </div>
      </div>
    );
}
```

2. 지시사항 1번을 참고하여 아직 완성되지 않은 두 개의 함수형 컴포넌트를 완성하세요.
  
  - UserInfo: 자식 태그 ```<div>```에 Props로 전달받은 user의 name과 age를 각각 출력
  - Profile: UserInfo 호출 후 props.author 전달 및 Comment 호출 후 props.text 전달

> Tips : HTML 태그 내에 주석을 사용하기 위해는 괄호를 이용해 {/* */}처럼 해야 합니다.

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//user의 정보(이름, 프로필사진) 출력 컴포넌트
function UserInfo(props) {
  return (
    <div className="UserInfo">
        <div> 이름: {props.author.name}</div> // 자식 태그 <div>에 Props로 전달받은 user의 name과 age를 각각 출력  
        <div> 나이: {props.author.age}</div>  
    </div>
  );
}

//코멘트 출력 컴포넌트
function Comment(props){
    return(
        <div className="Comment">문구: {props.text}</div>
    );
}

//문구 출력 컴포넌트
function Profile(props) {
  return (
    <div className="Profile">
        <UserInfo author={props.author} /> // UserInfo 호출 후 props.author 전달 
        <Comment text={props.text} /> // Comment 호출 후 props.text 전달
    </div>
  );
}

//데이터 저장 변수
const comment = {
  text: 'I hope you enjoy learning React!',
  author: {
    name: '엘리스 토끼',
    age: '12',
  },
};

const element = (
  <Profile
    text={comment.text}
    author={comment.author}
  />
);

ReactDOM.render(element, document.getElementById('root'));


serviceWorker.unregister();
```


