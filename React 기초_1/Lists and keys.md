# Lists and Keys

여러가지 컴포넌트를 리스트로 구성하는 방법에 대해 학습하도록 하겠습니다. 

여기서 주의할 점은 여러가지 컴포넌트가 동시에 렌더링이 되기 때문에 컴포넌트를 구분하기 위해서는 key값이 필요합니다. 

여기서 key가 무엇이고 어떤 역할을 하는지 함께 알아보도록 하겠습니다.

```
const numbers = [1, 2, 3, 4, 5]; //numbers라는 arrary, 1~5까지 아이템이 존재한다.
const doubled = numbers.map(number => number * 2); //각 아이템의 2배를 저장
console.log(doubled); // 결과: [2, 4, 6, 8, 10]
```
위 코드를 돌려보면 console에 [2, 4, 6, 8, 10]이 출력되는 것을 확인할 수 있습니다. 

리액트에서 컴포넌트로 리스트를 구성하는 것도 이와 비슷합니다.

## 리스트 만들기

1, 2, 3, 4, 5가 들어있는 numbers 변수를 표현하고 있는 number이라는 리액트 엘리먼트는 즉, 컴포넌트의 리턴 값입니다. 

그 리턴 값을 할당하고 있는 변수는 listItems입니다.

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map(number =>
  <li>{number}</li> /*컴포넌트의 리턴 값*/
);
```

그럼 array의 리턴 값을 할당하고 있는 변수 listItems는 아래 코드에서 보시다시피 ```<ul>``` 이라는 html태그 안에서 {}를 사용하여 표현할 수 있습니다. 

왜냐하면 앞서 JSX에서 학습했다시피 {} 안에서는 어떠한 자바스크립트 표현도 가능합니다.

따라서, numbers 배열을 **map()을 통해서 컴포넌트들의 array로** 바꾼 상태입니다. 그 값을 listItems가 할당하고, ```<ul>```태그 안에서 사용하게 됩니다.

```
ReactDOM.render(
  <ul>{listItems}</ul>, /*컴포넌트의 리턴 값 출력*/
  document.getElementById('root')
);
```

이번에는 컴포넌트들로 구성된 리스트를 반환하는 컴포넌트를 만들어보겠습니다.

```
function NumberList(props) { /*리액트 엘리먼트를 반환하는 NumberList라는 function 컴포넌트*/
  const numbers = props.numbers; /*위에서 사용했던 array를 props 받아와 numbers 변수에 할당*/
  const listItems = numbers.map(number => /*map()을 통해 숫자를 컴포넌트로 변환*/
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul> /*컴포넌트로 반환한 값을 반환*/
  )
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
다만, 이 코드를 실행했을 때는 경고가 나오게 됩니다. 리스트 안에는 ```<li>```가 만들어낸 리액트 엘리먼트가 여러 개 들어가 있습니다. 

그 엘리먼트끼리 구별이 가지 않습니다. 리액트의 입장에서 엘리먼트 내 들어가있는 값을 동일하게 인식합니다. 

그렇다면 어떻게 구별을 해주어야 할까요?

바로, **key값**을 추가해야 합니다! 태그에는 key값을 부여할 수 있는데, 리액트의 입장에서 key값을 통해 구분할 수 있습니다. 

**key는 string값을 가지는 props**입니다. 따라서, 태그마다 유니크한 key값을 주어야 합니다.

```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>/*li태그에 직접 key값을 부여*/
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

# Keys

위에서 잠깐 언급된 key에 대해 더 자세히 학습해보겠습니다. 

key는 리스트의 각 아이템이 추가되거나, 수정, 삭제될 때 리액트의 입장에서 빠르게 알아차릴 수 있도록 도와주는 역할을 합니다.

key는 ```map()```이 실행될 때 주어져야 합니다. 이에 대한 설명은 아래에서 다루도록 하겠습니다.
```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) => /*map() 실행*/
  <li key={number.toString()}> /*key값 부여*/
    {number}
  </li>
);
```

가장 좋은 key값을 부여하는 방법은 다른 엘리먼트들과 다른 UNIQUE한 string값을 부여하는 것 입니다.

대부분, **데이터의 id 값을 key값으로 부여**합니다.
```
const todoItems = todos.map((todo) =>
//<li>의 key값으로 todo.id라고, id값을 부여한 것을 확인할 수 있습니다.
  <li key={todo.id}> 
    {todo.text}
  </li>
);
```

만약, 변하지 않고 고정적인 key 값을 부여하는 것이 정말! 어렵다면 index를 사용하여 부여합니다.
```
const todoItems = todos.map((todo, index) =>
  // index를 이용하여 key값 부여하기
  <li key={index}>
    {todo.text}
  </li>
);
```

하지만, 그럴 경우 문제가 생길 수도 있습니다. array내 아이템의 순서가 바뀔 수도 있기 때문입니다.

> index를 key값으로 부여할 경우 좋지 않은 이유 알아보기<https://robinpokorny.medium.com/index-as-a-key-is-an-anti-pattern-e0349aece318>

> 더 자세히 알고 싶다면 왜 키가 필요한가? 에 대해 더 알아보세요. :) <https://reactjs-kr.firebaseapp.com/docs/reconciliation.html#recursing-on-children>

## key로 컴포넌트 추출하기

우리가 key값을 부여할 때는 **컴포넌트들을 아이템으로 가지고 있는 리스트 컴포넌트를 렌더링하고 싶을 때 사용**합니다. 

예를 들어서, 아래 코드의 ListItem 컴포넌트를 추출한 경우, ListItem 자체의 ```<li>``` 컴포넌트 요소가 아닌 배열의 ```<ListItem />``` 컴포넌트가 키를 가지고 있어야 합니다.

### 🔽 키 값을 잘 못 부여한 경우
```
function ListItem(props) {
  const value = props.value;
  return (
    // 키를 지정할 필요가 없습니다! : 배열값을 반환하지 않기 때문이죠.
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 키 값을 지정해야합니다! : 배열값을 반환하기 때문이죠.
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5]; //배열
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

### 🔽 키 값을 올바르게 부여한 경우
```
function ListItem(props) {
  // 배열값을 반환하지 않으니, 키 값을 지정하지 않습니다!
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 배열값을 반환하므로, 키 값을 지정합니다!
    <ListItem key={number.toString()}
              value={number} />

  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

## JSX에서 map() 포함하기

아래 코드에서는 listItems변수에 컴포넌트의 배열을 할당하고 JSX안에 그 변수를 ```{listItems}``` 형태로 작성한 것을 볼 수 있습니다.
```
function NumberList(props) {
  const numbers = props.numbers;
    //listItems를 선언하고, JSX에 포함
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    //{listItems} 형태로 출력
    <ul>
      {listItems}
    </ul>
  );
}
```

여기서! JSX는 {}를 이용하면 어떠한 자바스크립트 표현식<https://reactjs-kr.firebaseapp.com/docs/introducing-jsx.html#embedding-expressions-in-jsx>을 넣을 수 있기 때문에 map() 또한, 넣을 수 있습니다.
```
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```
때론 map()전체를 JSX 안에 넣으면 코드가 깔끔해질 수도 있습니다. 

개발을 하실 때, 가독성이 더 좋은 방향으로 판단하여 작성하시면 됩니다. 

map()이 너무 중첩되어있다면, 컴포넌트로 추출하는 것이 더 좋습니다.
