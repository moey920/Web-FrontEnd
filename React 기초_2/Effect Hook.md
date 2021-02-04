# Effect Hook의 사용

React의 컴포넌트는 아래와 같은 생명주기, **Mounting, Updating, Unmounting**을 가지며 각 과정은 컴포넌트가 생성되고, 수정되고, 해제될 때를 의미합니다.

Effect Hook을 사용하면 함수 컴포넌트에서 side effect를 수행할 수 있다는 것을 기억하시나요? side effect는 **렌더링 된 이후에 비동기로 처리되어야 하는 부수적인 효과**들을 말합니다.

정리하자면 Effect Hook은 클래스형 컴포넌트의 생명주기 메소드인 **componentDidMount, componentDidUpdate, componentWillUnmount가 합쳐진 것**으로 생각해도 좋습니다. 해당 메소드들은 위의 그림에서 알 수 있듯 Mounting, Updating, Unmounting가 이후 실행되는 메소드입니다.

## 정리(Clean-up)

Effect Hook을 직접 사용하기 전 정리(Clean-up)에 대해 알아봅시다. React 컴포넌트에는 정리(Clean-up)가 필요한 것과 그렇지 않은 것 두 종류의 side effects가 있습니다. 

정리란 클래스형 컴포넌트에서 Unmounting시 ```componentWillUnmount```를 이용해서 더 이상 사용하지 않는 컴포넌트를 해제하는 것을 말합니다. 예를 들어 메모리를 많이 사용하는 컴포넌트는 메모리 누수를 막기 위해 사용하지 않는 경우 componentWillUnmount 메소드에서 메모리를 해제하는 설정을 해줘야 합니다.

### 정리가 필요하지 않은 side effects

React가 DOM을 업데이트한 뒤 **추가로 코드를 실행해야 하는 경우 side effects 정리가 필요 없습니다.** 즉, 컴포넌트 실행 이후 신경 쓸 것이 없는 경우 별다른 정리를 하지 않아도 됩니다. 아래 예시는 버튼 클릭 시 1씩 카운트를 추가하는 컴포넌트입니다. 해당 컴포넌트는 렌더링 이후 계속 사용되기 때문에 따로 정리가 필요하지 않습니다.
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }
  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

### 정리를 이용하는 side effects

한편 정리(clean-up)가 필요한 side effects도 있습니다. React가 DOM을 업데이트한 뒤 추가로 코드를 실행할 필요가 없으면 정리를 해줘야 합니다. 그렇지 않으면 경우에 따라 메모리 누수가 발생해 시스템에 치명적인 영향을 미칠 수 있기 때문입니다. 아래는 채팅 앱에서 친구의 상태를 보여주는 컴포넌트입니다.
```
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

ChatAPI 모듈이나 subscribeToFriendStatus, unsubscribeFromFriendStatus 함수는 그냥 예시이기 때문에 자세한 동작에 대해서는 크게 신경 쓰지 않으셔도 됩니다. 

간단히 설명하자면 해당 컴포넌트는 **Mounting 시** subscribeToFriendStatus를 통해 **접속 중인 친구 정보**를 가져옵니다. 그리고 **Unmounting** unsubscribeFromFriendStatus를 통해 **접속 중인 친구 정보를 더 이상 가져오지 않는 것**입니다. (다만 해당 예제가 완전하기 위해서는 친구의 상태가 변하는 것을 감지하기 위해 Updating에 대한 componentDidUpdate도 필요합니다)

만약 정리하지 않으면, 계속해서 컴포넌트가 친구 정보를 가져오기 때문에 **메모리 누수**가 발생하는 것입니다.

## 그래서 Effect Hook은 왜 사용하나요?

혹시 정리에 대한 예제 코드들의 문제점이 보이시나요? 바로 각 생명주기 메소드에 똑같은 코드들이 들어 있는 것인데요. Effect Hook을 이용하면 이렇게 중복되는 코드를 함수형 컴포넌트에서 간단하게 관리할 수 있습니다! 자세한 사용 방법은 실습을 통해 알아봅시다.

## 정리가 필요 없는 **클래스형** 컴포넌트 실습

Effect Hook을 사용하기 전 정리가 필요 없는 클래스형 컴포넌트에 대해 확인해보겠습니다.

정리가 필요 없는 컴포넌트란 React가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있어 side effects 정리가 필요 없는 컴포넌트를 말합니다.

즉 컴포넌트가 Unmounting된 후 호출되는 componentWillUnmount()가 따로 필요 없는 경우입니다.

오른쪽 코드는 컴포넌트가 Mounting 되면 0번 클릭했습니다.라는 경고문을 띄우고, 이후에 버튼을 클릭할 때마다 클릭한 횟수를 띄우는 프로그램입니다.

생명주기 메소드와 alert(출력 문구) 메소드를 이용해 버튼 클릭 횟수를 띄우는 코드를 작성해볼까요?

1. componentDidMount() 메소드를 생성하고 count State를 이용해 버튼이 클릭 된 횟수를 경고창으로 띄우세요.
2. componentDidUpdate() 메소드를 생성하고 count State를 이용해 버튼이 클릭 된 횟수를 경고창으로 띄우세요.

> Tips
- componentDidMount()에서 경고창을 띄우는 코드가 있다면 프로그램이 실행되기 직전에 경고창이 나오게 됩니다.
- 문자열 내 변수를 표현하기 위해서는 ```${변수명}```과 같이 작성해야 합니다.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';


import React from 'react';

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
  
  // componentDidMount() 메소드를 완성하세요.
  componentDidMount() {
    alert(`${this.state.count}번 클릭했습니다.`);
  }

  
  // componentDidUpdate() 메소드를 완성하세요.
  componentDidUpdate() {
    alert(`${this.state.count}번 클릭했습니다.`);
  }

  render() {
    return (
      <div>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          버튼 클릭
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Counter />,document.getElementById('root'));

serviceWorker.unregister();
```

## 정리가 필요 없는 **함수형** 컴포넌트 실습

앞의 실습에서 구현한 정리가 필요 없는 클래스형 컴포넌트를 Effect Hook을 이용한 함수형 컴포넌트로 구현해보겠습니다.

먼저 Effect Hook을 구현하기 위해서는 useEffect를 import 해줘야 합니다.
```
import React, { useEffect } from 'react';
```
그리고 useEffect() 메소드와 화살표 함수를 이용해 아래처럼 작성하면 됩니다.
```
useEffect(() => {
    실행할 코드;
});
```
useEffect는 우리가 작성한 함수(이를 “effect”라고 합니다)를 기억하고 있다가 렌더링 이후 DOM 업데이트 시마다 실행합니다.

useEffect() 메소드는 클래스형 컴포넌트에 있는 두 생명주기 메소드와 동일한 기능을 한다고 이해하시면 됩니다.
```
componentDidMount() {
    실행할 코드;
}
componentDidUpdate() {
    실행할 코드;
}
```
정리하자면 생명주기 메소드를 함수형 컴포넌트에서 사용하기 위해 useEffect를 이용하는 것입니다! 직접 실습해 볼까요?

1. useEffect를 import 하세요.
2. useEffect()와 화살표 함수를 이용해 버튼이 클릭된 횟수(count)를 경고창으로 띄우세요.

> Tips
- import를 여러 개 해야 한다면, 중괄호 내 반점을 이용해 ```{ useState, useEffect }```처럼 작성하면 됩니다.
- 코드 내 함수형 컴포넌트에서 State를 사용하기 위해 useState를 사용하고 있습니다.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';

// useEffect를 import 하세요.
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);
  
  // useEffect()와 화살표 함수를 이용해 버튼이 클릭된 횟수를 경고창으로 띄우세요.
  useEffect(() => {
    alert(`${count}번 클릭했습니다.`)
  });

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
          버튼 클릭
        </button>
      </div>
  );
}

ReactDOM.render(<Counter />,document.getElementById('root'));

serviceWorker.unregister();
```

## 정리가 필요한 **클래스형** 컴포넌트 실습

이번에는 정리(Clean-up)가 필요한 클래스형 컴포넌트에 대해 알아보겠습니다.

정리란 클래스형 컴포넌트에서 Unmounting시 componentWillUnmount()를 이용해서 더 이상 사용하지 않는 컴포넌트를 해제하는 것을 말합니다.

텍스트를 반환하는 Child 컴포넌트와 해당 컴포넌트를 출력하고 버튼을 가지고 있는 Container 컴포넌트가 있습니다.

Container 컴포넌트의 버튼을 클릭하면 출력된 텍스트(Child 컴포넌트에 담겨 있는 텍스트)가 제거됩니다.

이때, Child 컴포넌트가 Unmounting 될 때 경고를 띄우는 코드를 작성해보세요.

- Child 컴포넌트에서 componentWillUnmount() 메소드를 생성하고 텍스트가 제거 되었습니다! 라는 경고창을 띄우세요.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';


class Container extends React.Component {
  constructor(props) {
    super(props);
    this.state = {show: true};
  }
  delHeader = () => {
    this.setState({show: false});
  }
  render() {
    let myheader;
    if (this.state.show) {
      myheader = <Child />;
    };
    return (
      <div>
        {myheader}
        <button type="버튼" onClick={this.delHeader}> Delete Header </button>
      </div>
    );
  }
}

class Child extends React.Component {
  // componentWillUnmount() 메소드를 생성하고 경고창을 띄우세요.
  componentWillUnmount() {
    alert("텍스트가 제거 되었습니다!")
  }
  
  render() {
    return (
      <p>버튼을 클릭해 해당 텍스트를 제거하세요.</p>
    );
  }
}

ReactDOM.render(<Container />,document.getElementById('root'));

serviceWorker.unregister();
```

## 정리가 필요한 **함수형** 컴포넌트 실습

마지막으로 정리가 필요한 함수형 컴포넌트에 대해 알아봅시다. 클래스형 컴포넌트에서 componentWillUnmount() 메소드를 통해 실행하던 코드를 useEffect를 이용해 실행해야 합니다.

이때 정리가 필요한 컴포넌트는 아래처럼 useEffect 내 함수의 반환을 통해 구현합니다. Mounting과 Updating 시 실행할 코드는 구현한 함수 위에 작성해주면 됩니다.
```
useEffect(() => {
    // Mounting 및 Updating 시 실행할 코드
    return function 함수명() {
      // Unmounting 시 실행할 코드
    }
});
```
이렇게 함으로써 생명주기 메소드를 함수형 컴포넌트 한 곳에서 관리할 수 있습니다.

컴포넌트가 정리될 때, 즉 Unmounting 되는 시점에 useEffect에서 메소드가 반환되는 것을 실습을 통해 알아봅시다.

- Child 컴포넌트에서 useEffect()를 화살표 함수로 생성하고 텍스트가 제거 되었습니다! 경고창을 띄우도록 함수를 만들어 반환하세요.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';
import React, { useState, useEffect } from 'react';

function Container() {
  const [show, setShow] = useState(true);
  
  let myheader;
  if (show) {
    myheader = <Child />;
  }
  
  return (
    <div>
    {myheader}
    <button onClick={() => setShow(false)}>버튼</button>
    </div>
  );
}

function Child() {
  // useEffect() 내 경고 문구를 출력하는 cleanup() 메소드를 반환하세요.
  useEffect(() => {
  // Mounting 및 Updating 시 실행할 코드
  // alert("Mountiong or Updating 되었습니다.")
    // Unmounting 시 실행할 코드
    return function cleanup() {
        alert("텍스트가 제거 되었습니다!")
    }
  });
  
  return (
    <p>버튼을 클릭해 해당 텍스트를 제거하세요.</p>
  );
  
}

ReactDOM.render(<Container />,document.getElementById('root'));

serviceWorker.unregister();
```

