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
