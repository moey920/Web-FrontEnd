# State

State는 앞서 배운 **Props처럼 컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 갖고 있는 객체**입니다. 

다만 Props는 컴포넌트에 전달되어 사용되는 반면 **State는 컴포넌트 안에서 관리**된다는 차이가 있습니다. 

즉 Props는 함수의 매개변수처럼 사용되는 것이고 **State는 함수 내에 선언된 변수처럼 사용**되는 것입니다. 

앞에서 사용했던 시간을 표시하는 코드를 가지고 State를 사용하는 방법을 차례차례 알아봅시다.
```
function tick() {
  const element = (
    <div>
      <h1>{new Date().toLocaleTimeString()}</h1>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

위의 컴포넌트에서 현재 시간을 띄우는 코드를 따로 캡슐화하여 시간을 표시하는 부분과 분리하겠습니다. 

그러기 위해 시간을 표시하는 컴포넌트에서 실제 시간을 가져올 때 앞에서 배웠던 Props를 이용하겠습니다. 

참고로 이런식으로 캡슐화를 하는 경우, 시간을 표시하는 양식이 달라졌을 때 시간을 구해주는 tick 컴포넌트를 재사용할 수 있는 장점이 있습니다.
```
function Clock(props) {
  return (
    <div>
      <h1>{props.date.toLocaleTimeString()}.</h1>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

위에서 Props를 사용한 이유는 **함수형 컴포넌트에서는 State를 사용할 수 없기 때문**입니다. 

따라서 함수형 컴포넌트를 클래스형 컴포넌트로 변환해보겠습니다. 

> 클래스형 컴포넌트를 만들 때 React.Component를 상속받고 render() 메소드를 구현해야 하는 것을 유의하며 변환해야 합니다. 

HTML 요소 자체는 그대로 사용하면 됩니다.
```
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>{this.props.date.toLocaleTimeString()}.</h1>
      </div>
    );
  }
}
```

마지막으로 State로 구현한 결과를 살펴봅시다. 

1. render() 메소드에서 Props를 state로 바꿔주고, 

2. 클래스 내에 초기 this.state를 지정하는 constructor()를 추가합니다. this.state에 실제 시간이 입력되어야 합니다. 

3. 그리고 실제로 렌더링을 하는 ReactDOM.render()을 작성해줍니다. 

기존의 tick 컴포넌트와 다르게 더 이상 필요없는 date props는 지우고 작성하면 됩니다.

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>{this.state.date.toLocaleTimeString()}.</h1>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

# Props vs State

Props와 State의 가장 큰 차이로 Props는 부모 컴포넌트에서 자식 컴포넌트로 전달하는 값으로 

자식 컴포넌트에서는 Props를 직접 수정할 수 없지만 

State는 컴포넌트 내부에서 선언하며 내부에서 관리되는 값으로 값을 변경할 수 있다는 점이 있습니다.

따라서 값이 변경되어야하는 상황, 

예를 들면 매초 변하는 시간을 출력해야 하거나 버튼 클릭시 값이 변하는 것을 출력해야 한다면 State를 사용해야 합니다. 

정리하자면 Props는 읽기 전용으로 수정이 불가능하고, State는 원하는 경우 수정이 가능하기 때문에 상황에 따라 알맞은 것을 사용하면 됩니다.


## setState()

앞서 배운 State의 값을 변경하기 위한 메소드에 대해 알아봅시다. 

State를 변경하기 위해서는 직접 값을 수정하는 것이 아니라 setState() 메소드를 이용해야 합니다. 

아래는 버튼 클릭 시 출력되는 텍스트가 red에서 blue로 수정되는 코드입니다. 

참고로 시간이 변하는 것처럼 주기적으로 발생하는 것이 아니라 버튼 클릭과 같은 

특정 이벤트로 상태가 변하는 것을 State가 비동기적으로 변경된다고 합니다.
```
class Change extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      color: "red"
    };
  }
  changeColor = () => {
    this.setState({color: "blue"});
  }
  render() {
    return (
      <div>
        <h1>It is a {this.state.color}</h1>
        <button
          type="button"
          onClick={this.changeColor}
        >Change color</button>
      </div>
    );
  }
}
```

## 생명주기

컴포넌트의 생명주기(Life cycle)에 대해 알아봅시다. 생명주기란 앱이 실행되고 종료되는 과정을 특정 시점 별로 나눠둔 것을 말합니다. 

파이썬의 클래스 객체로 예를 들면, 클래스가 생성되면 생성자가 호출되고 소멸되면 소멸자가 호출됩니다. 

간단하지만 이러한 요소의 시작과 끝이 바로 생명주기입니다.

## React의 생명주기

React의 생명주기는 컴포넌트가 이벤트를 다룰 수 있는 특정 시점을 말하며 마운트, 업데이트, 언마운트 상태로 구성되어 있습니다. 

컴포넌트가 실제 DOM에 삽입되는 것을 마운트, 컴포넌트가 변하는 것을 업데이트, 컴포넌트가 DOM 상에서 제거되는 것을 언마운트라고 합니다. 

특정 시점별 호출되는 생명주기 메소드에 대해 알아봅시다.

## 생명주기 메소드

React의 생명주기 메소드는 다음과 같은 것들이 있습니다.

- constructor(): State 데이터를 초기화 하는 메소드
- render(): 클래스 컴포넌트에서 반드시 구현되어야 하는 메소드
- componentDidMount(): 컴포넌트가 마운트 된 직후 호출되는 메소드
- componentDidUpdate(): 업데이트가 진행된 직후에 호출되는 메소드
- componentWillUnmount(): 컴포넌트가 마운트 해제되어 제거되기 직전에 호출되는 메소드

아래는 componentDidMount()를 사용한 예시입니다. 마운트 직후 해당 함수가 호출되면서 표시된 색깔이 red에서 yellow로 변경됩니다. 

참고로 setTimeout()을 이용해서 실행이 되는 타이머를 설정할 수 있습니다. 

따라서 현재 코드를 실행하면 처음에는 red가 표시되다가 1초 뒤에 yellow로 변하게 됩니다.
```
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({favoritecolor: "yellow"})
    }, 1000)
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
    );
  }
}

ReactDOM.render(<Header />, document.getElementById('root'));
```

### 언제 사용하나요?

만약 동적인 앱을 만들고 싶다면 이러한 생명주기에 대해서 잘 알아야 합니다. 

예를 들어 사용자가 특정 행동을 완료할 때마다 알림을 주고 싶다면 

컴포넌트가 마운트 된 이후 호출되는 componentDidMount() 메소드를 이용해 알림을 줄 수가 있습니다. 

즉 원하는 시점에 따라 컴포넌트가 다른 동작을 실행하길 원한다면, 생명주기 메소드에 대해서 잘 알고 있어야 합니다.

### 컴포넌트 재사용을 위한 캡슐화 실습

캡슐화란 모듈 단위로 컴포넌트를 나누어 구현하는 것을 의미합니다. 앞에서 했던 컴포넌트 추출이 바로 컴포넌트를 캡슐화 하는 것입니다.

캡슐화를 통해 얻을 수 있는 이점을 다시 한 번 상기해 봅시다.

- 코드 유지보수성이 향상됩니다.
- 코드 재사용이 용이합니다.
- 가독성 향상됩니다.

캡슐화를 통해 코드의 재사용성을 높이기 위해, 제공된 코드를 수정해봅시다. 제공된 코드는 현재 시간을 출력하는 코드로 아래의 기능을 합니다.

1. 현재 시간을 받아 element를 생성합니다.
2. ReactDOM에 element를 렌더링합니다.
3. 1~2과정을 1초에 한번씩 반복합니다.

#### 지시사항

1. 시간 출력 함수 Clock을 정의하세요. Clock에서 props.변수명.toLocaleTimeString() 로 현재시간을 받을 수 있습니다.
2. element에서 Clock컴포넌트를 호출하세요. Clock 컴포넌트의 props는 ```변수명={new Date()}```로 제공할 수 있습니다.

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//현재시간을 출력하는 컴포넌트
//현재시간의 props를 받아 출력합니다.
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>현재 시간: {props.date.toLocaleTimeString()}</h2>
    </div>
  );
}

//매초 마다 호출되는 함수
function tick() {
  //Clock 컴포넌트를 호출합니다.
  const element = <Clock date = {new Date()} />;
  
  //ReactDOM에 element을 렌더링합니다.
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);

serviceWorker.unregister();
```


### 함수 컴포넌트를 클래스로 변환 실습

함수 컴포넌트는 State를 가질 수 없다는 단점이 있습니다. 

이를 해결하기 위해서 함수 컴포넌트를 클래스 컴포넌트로 변환하는 과정이 필요합니다. 변환 과정은 아래 순서로 이루어집니다.

1. React.Component를 상속받는 컴포넌트 클래스 생성
2. 메소드 명이 render()인 빈 메소드 추가
3. 함수 컴포넌트 내용을 render()메소드로 이동
4. render() 안의 props를 this.props로 변경
5. 기존의 함수 컴포넌트 삭제

##### 컴포넌트 변환 예시

- 함수 컴포넌트
```
function Hello(props){
    reuturn <h1> Hello, {props.name}</h1>;
}
```

- 클래스 컴포넌트
```
class Hello extends React.Component {
    render() {
      return <h1> Hello, {this.props.name}</h1>;      
    }
}
```
컴포넌트 변환 예시를 참고하여 이전 실습에서 생성한 아래의 함수 컴포넌트 Clock을 클래스 컴포넌트로 변경해봅시다.

```
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}</h2>
    </div>
  );
}
```

#### 지시사항

1. React.Component를 상속받는 Clock 클래스를 선언하세요.
2. 클래스 내에 빈 메소드 render()를 정의하세요.
3. render()내에 함수 컴포넌트의 코드를 그대로 넣으세요.
4. props를 this.props로 변경하세요.
5. tick 컴포넌트에서 시간을 props로 념겨 Clock 컴포넌트를 호출하는 element 변수를 정의하세요.

> Tips : Clock 컴포넌트의 props는 ```변수명={new Date()}```로 제공할 수 있습니다.
State란 props와 유사하지만, 비공개이며 컴포넌트에 의해 완전히 제어됩니다. 자세한 내용은 다음 실습에서 설명됩니다.

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//클래스 컴포넌트를 사용하여 Clock컴포넌트를 작성합니다.
class Clock extends React.Component{
    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.props.date.toLocaleTimeString()}</h2>
            </div>
        );
    }
} 


//매초 마다 호출되는 함수
function tick() {
  //Clock 컴포넌트를 호출하고 현재 시간을 props로 넘겨줍니다.
  const element = <Clock date = {new Date()} />;
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);

serviceWorker.unregister();
```

### 클래스에 로컬 State 추가 실습

State는 props와 같이 컴포넌트의 렌더링 결과물에 영향을 주는 데이터를 가진 객체입니다.

props는 컴포넌트에 직접 전달되는 반면, State는 데이터가 컴포넌트 내에서 관리된다는 차이점이 있습니다. 

- State를 사용하면 불필요한 내부 데이터를 은닉할 수 있다는 장점이 있습니다.

다음으로 State를 사용하기 위해 클래스 컴포넌트에서 선언되어야 하는 constructor()에 대해 알아봅시다. 

constructor()메소드는 컴포넌트를 초기화하는 메소드입니다. 해당 메소드는 아래의 과정을 통해 생성됩니다.

1. 클래스 컴포넌트 내에 constructor()메소드 선언
2. constructor(props)메소드 내에 super(props) 호출
3. State 초기화

이와 함께 State를 사용하기 위해서는 다음의 과정이 필수적입니다.

1. 클래스 내에 constructor()메소드 추가
2. super(props) 호출
3. State 내에 데이터 삽입
4. this.props를 this.state로 변경
5. 컴포넌트 호출 시 props 넘겨주지 않으며 props를 제공하는 대신 State에 필요한 데이터 저장

#### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//현재시간을 출력하는 컴포넌트
class Clock extends React.Component {
  // 초기 this.state를 지정하는 constructor() 함수를 추가하세요.
    constructor(props) { // constructor(props)메소드 내에 super(props) 호출
        super(props);
        // this.state = {data: new Data()} 코드를 통해 State를 정의하세요.(State 초기화)
        this.state = {
            date: new Date()
        };
    }

  //props를 state로 변경합니다.
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

//Clock 컴포넌트를 호출합니다.
const element = <Clock date = {new Date()} />;

ReactDOM.render(
  element,
  document.getElementById('root')
);

serviceWorker.unregister();
```

### 생명주기 메서드 추가

컴포넌트는 생성->업데이트->제거의 생명주기를 지닙니다. 

생명주기 메소드의 종류와 역할에 대해서도 확인해봅시다.

생명주기 메소드

- constructor(): State 데이터를 초기화 하는 메소드
- render(): 클래스 컴포넌트에서 반드시 구현되어야 하는 메소드
- componentDidMount(): 컴포넌트가 마운트 된 직후 호출되는 메소드
- componentDidUpdate(): 업데이트가 진행된 직후에 호출되는 메소드
- componentWillUnmoumt(): 컴포넌트가 마운트 해제되어 제거되기 직전에 호출되는 메소드

이번에는 별다른 코드 작성 없이 개발자 도구를 통해 생명주기 절차가 어떻게 진행되는지 확인해봅시다.

#### 지시사항

1. 제공된 코드를 실행하여 결과 페이지를 화면에 띄우세요.
2. 개발자 도구에서 console탭을 통해 컴포넌트의 생명주기를 확인하세요. 크롬의 오른쪽 상단의 메뉴 버튼 클릭 후 “도구 더보기” > “개발자 도구” 클릭하여 개발자 도구를 실행할 수 있습니다.
3. 언제 어떤 메소드가 출력되는지 확인하세요.

#### 해답 코드(개발자 도구의 console창 메서드 확인하기)
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';


class Clock extends React.Component {
  constructor(props) {
    console.log("constructor() 호출")
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    console.log("componentDidMount() 호출")
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    console.log("componentWillUnmount() 호출")
    clearInterval(this.timerID);
  }

  tick() {
    console.log("tick() 호출")
    this.setState({
      date: new Date()
    });
  }

  render() {
    console.log("render() 호출")
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
serviceWorker.unregister();

// constructor() 호출
// render() 호출
// componentDidMount() 호출 은 페이지 생성과 동시에 호출된다.
// 이후 
// 이후 
// tick() 호출 : setState를 통해 컴포넌트 값을 변경한 직후직후(componentDidUpdate()) 메소드가 호출됨
// rander() 호출 이 반복된다. 
// componentWillUnmount()는 어떻게 봐야할지 모르겠다.
```
