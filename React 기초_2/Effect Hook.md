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
