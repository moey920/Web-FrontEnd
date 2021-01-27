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
