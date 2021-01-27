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


이벤트에 실행할 코드 전달 (X) 함수 형태의 객체를 전달 (O)
이벤트를 실행할 코드를 그대로 전달하는 것이 아니라 아래 onClick처럼 함수의 형태로 객체를 전달합니다.

<button onClick={
    ()=>{
        this.setState({
        message : ''
        })
    }
}>


DOM요소에만 이벤트 설정 가능
직접 만든 리액트 컴포넌트에는 이벤트를 자체적으로 설정할 수 없습니다. <div> <button> <p> <input> 등 DOM요소에만 이벤트를 사용할 수 있습니다.

아래와 같이 직접 만든 <EventPractice>에는 이벤트를 사용해도 적용이 되지 않습니다.

render() {
    return (
        <EventPractice onLoad={
            ()=>{
            console.log("test");
            }
        }/>
    );
}
이벤트 작성하기
function키워드를 사용해 이벤트 함수를 작성합니다.
onClick={함수명}으로 등록한 이벤트를 호출합니다.
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
📌 실습하러 가기 →

이벤트 핸들링 하기
1. 함수로 작성하여 핸들링 하기

함수의 형태로 객체를 넘기기 때문에 함수 형태로 작성해야 합니다.

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


2. 함수 미리 작성 후, 핸들링

미리 작성한 함수를 전달하여 핸들링도 가능합니다. 생성자 함수에서 만들어 놓은 함수를 바인딩 해줘야 합니다.

바인딩이란? react 컴포넌트에 이벤트를 연결하는 것을 의미합니다.

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
📌실습하러 가기 →

이벤트 핸들러에 인수 전달하기
보통 반복문 안에서 id값을 추가 인수로 전달해야 하는 경우가 있습니다.

<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
위 코드에서 화살표 함수 id값을 부여할 때, event를 e로 전달해주어야 합니다. 하지만 두번째 bind()를 사용하는 경우, event를 따로 전달하지 않아도 자동으로 전달됩니다.
