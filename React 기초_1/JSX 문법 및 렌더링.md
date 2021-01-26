# JSX 문법 및 렌더링
JSX문법을 학습하여 기존의 HTML코드를 변환하는 실습을 진행해보겠습니다.

## JSX

**JSX는 자바스크립트 XML의 약자**이며 여기서 **XML은 HTML의 한계를 극복하기 위해 만들어진 마크업 언어**입니다. 

즉 **JSX는 자바스크립트를 확장한 문법이며 HTML을 React에서 쉽게 쓰기 위해 사용**됩니다. 아래 코드를 살펴봅시다.

```
const element = <h1> Hello, elice! </h1>;
```

코드에는 HTML 태그가 들어가지만 그렇다고 해당 코드가 HTML 문법은 아닙니다. 이러한 문법이 바로 JSX이며, React에서 사용되는 문법입니다. 

React는 JSX 문법을 이용해 마크업 언어와 코드의 로직을 따로 분리하지 않고 두 가지를 포함한 컴포넌트라는 것을 사용합니다. 

컴포넌트에 대한 설명은 추후에 살펴보도록 하겠습니다.

### 변수

간단한 변수 선언 방식에 대해 먼저 알아봅시다. 변수 선언 방식은 ```const, let, var``` 세 가지가 있습니다. 형태는 다음과 같습니다.
```
변수선언방식 변수명 = 값;
```

- ```var``` 같은 경우 아래처럼 재선언이 가능하지만 다른 선언 방식은 불가능합니다.
```
var name = "Chris";
var name = "John"
```

- ```var과 let```은 아래와 같은 재정의가 가능하지만 **const는 불가능**합니다.
```
let name = "Chris";
name = "John"
```

이를 간단히 표로 정리하면 다음과 같습니다.

| 선언 방식 | 재선언 | 재정의 |
|:---:|:---:|:---:|:---:|
| var | 가능 | 가능 |
| let | 불가능 | 가능 |
| const | 불가능 | 불가능 |
				
### 표현식

JSX에서 중괄호를 이용해 사용 가능한 표현식들의 예시를 살펴보겠습니다. 

먼저 중괄호를 이용해 HTML 내에 변수를 표현할 수 있습니다. 아래 element 변수는 위의 예시와 동일한 값을 가집니다.
```
const name = 'elice';
const element = <h1> Hello, {name}! </h1>;
```

또한 중괄호를 이용해 함수 표현식을 넣는 것도 가능합니다.
```
function greeting(){
  return "Hello, elice!";
}

const element = <h1>{greeting()}</h1>;
```
그리고 함수 내에서 표현식을 적용할 수도 있습니다.
```
function formatGreeting(name){
  return "Hello" + ' ' + name;
}

function getGreeting(user) {
  return <h1>Hello, {formatName("elice!")}!</h1>;
}
```

### 속성

큰 따옴표를 이용해 JSX의 속성을 지정할 수 있습니다.
```
const element = <a href = "https://kdt.elice.io/explore">엘리스로 이동</a>;
```

마찬가지로 속성도 표현식을 이용해 지정하는 것도 가능합니다.
```
const link = "https://kdt.elice.io/explore";
const element = <a href = {link}>엘리스로 이동</a>;
```

### 자식 정의

자식 태그가 여러개 포함된 코드를 저장하기 위해서는 자식 태그를 부모 태그로 감싸야 합니다. 

여기서 <div> 태그가 부모 태그, <h1>과 <h2>가 자식 태그입니다.
```
const element = (
  <div>
    <h1>Hello,</h1>
    <h2>elice!</h2>
  </div>
);
```

그리고 **모든 태그는 반드시 닫혀야 한다는 것에 유의**하세요. 

다만 아래 코드에서 원래 태그 이름을 맞춰서 </input>처럼 닫아야 하지만, 이름은 생략하고 />만 이용해서 닫아도 괜찮습니다.
```
const element = <input type="text" />;
```

### 객체 표현

React.createElement() 메소드를 이용하면 JSX 문법을 이용하지 않고 객체로 표현할 수 있습니다. 

자세한 사용 방법은 아래 예제와 함께 살펴보겠습니다. 아래의 두 코드는 문법이 조금 다르지만 같은 내용을 담고 있습니다.
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

기존 JSX 문법 대신에 ```React.createElement()``` 메소드를 이용하여 **매개변수로 헤더, 속성, 출력 값을 순서대로 넘겨주면 됩니다.**
