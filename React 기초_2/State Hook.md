# Hook과 함수형 컴포넌트

State Hook에 대해 알아보기 전에 Hook을 사용할 수 있는 함수형 컴포넌트에 대해 짚고 넘어가겠습니다. React의 함수형 컴포넌트는 일반적으로 이렇게 생겼습니다.
```
function Example(props) {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}
```

또한 아래와 같이 화살표 함수(arrow function)를 이용해 구현되었을 수도 있으며, 마찬가지로 함수형 컴포넌트입니다.
```
const Example = (props) => {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}
```

함수형 컴포넌트가 state가 없는 컴포넌트로 알고 있었을 겁니다. 하지만 Hook은 React state를 함수 안에서 사용할 수 있게 해줍니다! 당연하겠지만 Hook은 클래스 안에서 동작하지 않기 때문에 클래스를 작성하지 않고 사용해야 합니다.

## Hook 사용하기

React의 Hook을 사용하기 위해서는 사용할 Hook을 import를 해줘야 합니다. 만약 State Hook을 사용하기 위해 useState()를 이용하고 싶다면 아래처럼 해주면 됩니다.
```
import React, { useState } from 'react';
```

Hook은 아주 특별한 함수입니다. 위에 나온 useState()는 state를 함수 컴포넌트 안에서 사용할 수 있게 해줍니다. 이제 함수형 컴포넌트를 사용하던 중 state를 추가하고 싶다면 클래스 컴포넌트로 바꿀 필요 없이 함수 컴포넌트 안에서 Hook을 이용하여 state를 사용하면 됩니다. 그 외에 여러 Hook은 나중에 살펴봅시다!

## Hook과 같은 기능을 하는 클래스 실습

State Hook을 이용해 함수형 컴포넌트에서 State를 사용하는 방법에 대해 알아보기 전에 클래스형 컴포넌트의 State를 사용하는 방법을 다시 짚고 넘어가겠습니다.

클래스 내 constructor()에서 State를 초기화해주고, render()에서 setState() 메소드를 이용해 State를 업데이트할 수 있습니다.

버튼 클릭 시 카운트를 하는 프로그램을 통해 다시 한번 살펴보겠습니다. 카운트에 대한 State가 담긴 count를 만들어 문제를 해결해보세요.

1. constructor()에서 count의 State를 0으로 설정하세요.
2. render()의 ```<p>``` 태그에서 클릭 횟수인 count의 State를 출력하세요.
3. render()의 ```<button>``` 태그에서 setState()를 이용해 버튼 클릭 시 count가 1 증가하는 코드를 작성하세요.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';
import React from 'react';

class Example extends React.Component {
  constructor(props) {
    super(props);
    // count의 state를 0으로 설정하세요.
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        {/* count의 state를 출력하세요. */}
        <p>You clicked {this.state.count} times</p>
        {/* setState()를 이용해 버튼 클릭 시 count가 1 증가하는 코드를 작성하세요. */}
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

ReactDOM.render(<Example />,document.getElementById('root'));

serviceWorker.unregister();
```

## State 변수 선언하기 실습

클래스 이용해 State 변수를 선언하기 위해서 constructor() 안에서 this.state를 { count: 0 }으로 설정함으로써 count State를 0으로 초기화했습니다.
```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
```

하지만 함수 컴포넌트는 this를 가질 수 없기 때문에 this.state를 할당하거나 읽을 수 없습니다. 대신 State Hook을 이용해 State를 직접 컴포넌트에 호출할 수 있습니다.

즉, useState() 메소드를 호출하여 State 변수를 선언할 수 있습니다. 위에서 선언한 count가 바로 State 변수입니다. 물론 이 이름은 자유롭게 설정해도 좋습니다.

useState()는 클래스 컴포넌트의 this.state가 제공하는 기능과 똑같습니다. 일반적으로 변수는 함수가 끝날 때 사라지지만 State 변수는 사라지지 않습니다.

useState()의 인자로 넘겨주어야 하는 값은 State의 초깃값입니다. 함수형 컴포넌트의 State는 클래스와 달리 객체일 필요는 없고 숫자나 문자 같은 변수로 사용하면 됩니다.

useState()는 State 변수와 해당 변수를 갱신할 수 있는 함수 두 가지를 반환합니다. 결과적으로 아래와 같은 형태로 사용하면 됩니다.
```
const [State 변수, State 변수를 갱신할 함수] = useState(초깃값);
```
이번 실습에서는 useState()를 이용해 State 변수를 선언하는 방법을 익혀보겠습니다.

1. State Hook을 사용하기 위해 useState를 import 하세요.
2. useState()를 이용해 State인 count와 State를 갱신할 함수 useState를 선언하세요. 단, count의 초깃값은 0으로 설정하세요.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';

// useState를 import하세요.
import React, {useState} from 'react';

function Example() {
  // useState()를 이용해 State인 count와 State를 갱신할 함수 useState를 선언하세요.
  const[count, setCount] = useState(0);
  
  // 변수 선언이 잘 되었는지 확인하기 위한 코드입니다. 수정하지 마세요!
  return (
    <div>
      {count}
      {setCount}
    </div>
  )
}

ReactDOM.render(<Example />,document.getElementById('root'));

serviceWorker.unregister();
```

## State 가져오기 & 갱신하기 실습

앞의 실습에서 useState()가 State 변수와 해당 변수를 갱신할 수 있는 함수 두 가지를 반환한다는 것을 배웠습니다. 이번에는 클래스형 컴포넌트와 비교했을 때, 반환된 두 가지를 어떻게 사용해야 하는지 알아봅시다.

클래스 컴포넌트는 count를 보여주기 위해 this.state.count를 사용했습니다.
```
  <p>You clicked {this.state.count} times</p>
```
반면 함수형 컴포넌트에서는 State인 count를 {count}와 같은 형태로 직접 사용할 수 있습니다.

또한 클래스 컴포넌트는 count를 갱신하기 위해 this.setState()를 호출했습니다.
```
  <button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
  </button>
```
하지만 함수형 컴포넌트에서는 setCount()와 count 변수를 가지고 있음으로 this를 호출하지 않아도 됩니다. 새로 설정할 count의 값을 setCount()의 매개변수로 넘겨주면 됩니다.

즉, 클래스 컴포넌트의 this.state.count가 this.setState와 유사하다고 생각하시면 됩니다.

1. ```<p>``` 태그에서 count의 State를 화면에 출력하세요.
2. ```<button> ```태그에서 버튼 클릭 시 count가 1 증가하도록 setCount()의 매개변수에 count+1을 넘겨주는 코드를 작성하세요.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';

import React, { useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      {/* count의 State를 화면에 출력하세요. */}
      <p>You clicked {count} times</p>
        {/* setCount()를 이용해 버튼 클릭 시 count가 1 증가하는 코드를 작성하세요. */}
        <button onClick={() => setCount(count+1)}>
          Click me
        </button>
    </div>
  )
}

ReactDOM.render(<Example />,document.getElementById('root'));

serviceWorker.unregister();
```

## State Hook 요약 실습

지금까지 State Hook을 사용하는 방법에 대해 알아보았습니다. 이번에는 지금까지 배운 내용을 활용해보는 실습을 해보겠습니다.

앱을 실행하면 가지고 있는 사과의 개수가 출력됩니다. 처음에는 5개의 사과를 가지고 있습니다.

Eat apple 버튼을 클릭하면 사과의 개수가 하나 줄어들고, Buy apple 버튼을 클릭하면 사과의 개수가 하나 늘어납니다.

지시사항에 따라 위에서 설명한 동작을 하는 코드를 작성해볼까요?

1. usetState를 import 하세요.
2. 함수형 컴포넌트를 만들고 useState() 함수를 사용해 State 변수와 State를 설정하는 함수를 만드세요. State의 초깃값은 5로 설정하세요.
3. 아래 태그의 순서와 규칙대로 코드를 작성하여, 함수형 컴포넌트에서 반환하세요.
```
<div>
    <p> 남은 사과의 개수를 출력 결과와 동일하게 출력</p>
        <button onClick 속성과 State 설정 함수를 이용해 사과의 개수 감소</button>
        <button onClick 속성과 State 설정 함수를 이용해 사과의 개수 증가</button>
</div>
```

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';
import React, {useState} from 'react';

// 지시사항에 따라 출력 결과와 동일한 동작을 하는 코드를 작성하세요.
function Apple() {
    const [count, setCount] = useState(5);
    
    return (
        <div>
            <p>당신에게 {count}개의 사과가 남았습니다.</p>
                <button onClick={() => setCount(count-1)}>
                Eat apple</button>
                <button onClick={() => setCount(count+1)}>
                Buy apple</button>
        </div>
    
    )
}

ReactDOM.render(<Apple />,document.getElementById('root'));

serviceWorker.unregister();
```

## State Hook 팁 실습

State Hook을 사용할 때 유용한 두 가지 팁을 소개해드리려고 합니다.

### 배열 구조 분해
앞서 아래처럼 대괄호를 이용하여 State 변수를 선언하는 것을 보셨을 겁니다.
```
const [count, setCount] = useState(0);
```

이론에서 설명했듯이 대괄호 왼쪽의 State 변수는 사용하고 싶은 이름으로 선언할 수 있습니다. 아래는 count라는 이름 대신 fruit라는 이름으로 사용한 것입니다.
```
const [fruit, setFruit] = useState('banana');
```
이렇게 대괄호를 이용해 값을 대입하는 자바스크립트 문법을 구조 분해 할당 중에서도 배열 구조 분해라고 합니다.

useState()를 사용하면 fruit이라는 첫 번째 값과 setFruit이라는 두 번째 값을 반환하여 총 2개의 값을 만들고 있습니다. 이는 아래의 코드와 같은 기능을 하는 것입니다.
```
var fruitStateVariable = useState('banana'); // 두 개의 아이템이 있는 쌍을 반환
var fruit = fruitStateVariable[0]; // 첫 번째 아이템
var setFruit = fruitStateVariable[1]; // 두 번째 아이템
```

여기서 첫 번째 아이템은 현재 State 변수를 의미하고 두 번째 아이템은 해당 변수를 설정해주는 함수입니다. 다만 배열 구조 분해라는 특별한 방법으로 변수를 선언해주었기 때문에 인덱스([0] 이나 [1])로 배열에 접근하는 것은 권장되지 않습니다.

### 여러 개의 State 변수를 사용하기

```[State 변수, State 변수를 갱신할 함수]```의 쌍으로 State 변수를 선언하는 방식을 통해 이름이 다른 여러 개의 State 변수를 선언할 수 있습니다.
```
function ExampleWithManyStates() {
  // 여러 개의 state를 선언할 수 있습니다!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
}
```

위의 코드는 age, fruit, todos라는 State 변수가 각각 존재하고 개별적으로 갱신할 수 있습니다.

배열 구조 분해를 이용하여 여러 개의 State를 직접 만드는 실습을 해봅시다.

1. 함수형 컴포넌트에서 반환되는 HTML 코드를 확인하고 name과 email에 대한 State 변수와 State 값을 갱신하는 함수를 각각 선언하세요.

> Tips : State 변수를 갱신할 함수 이름 역시 자유롭게 설정할 수 있지만 set상태변수와 같이 설정하는 것이 일반적입니다.

```
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';

import React, { useState } from 'react';

function UserFormFunction() {
  // name과 email에 대한 State를 각각 선언하세요.
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  
  return (
    <>
      <label>
        Name:
        <input
          type="text"
          value={name}
          onChange={({ target: { value } }) => setName(value)}
        />
      </label>
      <br/>
      <label>
        Email:
        <input
          type="email"
          value={email}
          onChange={({ target: { value } }) => setEmail(value)}
        />
      </label>
      <br/>
      <h3> 이름: {name}  이메일: {email} </h3>
    </>
  )
}

ReactDOM.render(<UserFormFunction />,document.getElementById('root'));



serviceWorker.unregister();
```
