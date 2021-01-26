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


## HTML을 JSX로 변환하기

JSX란 자바스크립트를 확장한 문법입니다.

자바스크립트 코드 안에서 UI 관련 작업을 할 때 효과적으로 활용됩니다.

JSX를 사용할 때는 다음의 사항에 대해 유의해야 합니다.

HTML을 JSX로 변환할 때, 변수 내에 HTML코드를 저장합니다.

여러 자식 태그로 구성된 HTML 코드는 반드시 부모 태그 내에 구성되어야 합니다.

문장의 끝은 세미콜론(;)을 사용해야 합니다.

### 지시사항

1. 이미 선언된 element 변수를 확인하세요.
2. element 변수에 아래 제시된 HTML 코드를 JSX로 변경하여 저장하세요. 단, 해당 HTML은 <div> 태그를 부모 태그로 가집니다.
```
<h2>
        코더랜드에 오신것을 환영합니다:)
</h2>
<h2>
        즐거운 React! 함께 공부해봐요~
</h2>
```

### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//HTML을 JSX로 변환하여 element에 저장합니다.
const element = (
    <div>
        <h2>코더랜드에 오신것을 환영합니다:)</h2>
        <h2>즐거운 React! 함께 공부해봐요~</h2>
    </div>
);

ReactDOM.render(element, document.getElementById('root'));

serviceWorker.unregister(); # 앱 배포 시 캐시가 남지 않도록 하는 코드
```

## JSX에 표현식 포함하기

JSX 중괄호(```{}```) 안에는 여러 자바스크립트 표현식을 사용할 수 있습니다. 

예를 들면 다음과 같은 자바스크립트 표현식들을 JSX에서 그대로 활용할 수 있습니다.

- 산술식: 숫자 표현 (ex. 3.141593.14159, -2−2)
- 문자열: 문자열 표현 (ex. "234", "Fred")
- 논리식: 참 또는 거짓 표현 (ex. true, false)
- 기본 표현식: 자바스크립트의 기본 키워드 및 일반 표현식 (ex. 3 + 5)

아래 예시를 참고하여 JSX내 표현식으로 Josh Perez에게 인사하는 페이지를 작성해봅시다!

기본 표현식 사용 예시
```
const expression = 3*5
const element = <h1>3*5= {expression}</h1>;
```

### 지시사항
- name변수를 선언한 후, Josh Perez 문자열을 저장하세요.
- element 변수에 표현식을 사용하여 저장한 name 변수가 출력되도록 만드세요.

> Tips : 자세한 자바스크립트의 표현식은 링크<https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Expressions_and_Operators#%ED%91%9C%ED%98%84%EC%8B%9D>를 참고하세요!

### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//name변수를 선언하고, 이름을 저장합니다.
var name = "Josh Perez"

//표현식을 사용하여 name을 포함합니다.
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element,document.getElementById('root'));

serviceWorker.unregister();
```

## JSX에 함수 표현식 넣기

함수 표현식도 마찬가지로 중괄호(```{}```)를 사용하여 호출할 수 있습니다.

함수를 정의하는 방법은 다음과 같습니다.

1. function 키워드를 사용하여 함수를 정의합니다.
2. 필요 시, 매개변수 값을 받아 함수 내에서 사용합니다.
3. return 키워드를 통해 결과를 반환합니다.

함수 정의 및 호출 예시
```
function multiplication(num1, num2){
  return num1 + "*" + num2 + " = " + num1*num2;
}

const element = <h1>{multiplication(5, 9)}</h1>;
```

위의 예시를 참고하여 출력문구를 반환하는 함수 welcome()을 정의하고, 결과를 출력하는 페이지를 작성해봅시다.

### 지시사항

1. function키워드를 사용해 문자열을 반환하는 함수를 정의하세요.
2. 함수표현식을 사용하여 정의한 함수를 element 변수에 호출하세요. 출력 문구는 출력결과와 동일해야 하며 <h2>태그를 사용합니다.

### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//함수를 정의합니다.
function call() {
    return "안녕하세요! 코더랜드에 오신걸 환영합니다:)"
}

//함수표현식을 사용하여 함수를 호출합니다.
//<h2>태그를 사용해 함수의 결과값을 화면에 출력합니다.
const element = <h2>{call()}</h2>;


ReactDOM.render(element, document.getElementById('root'));

serviceWorker.unregister();
```

## 함수에 JSX 활용하기

**함수도 표현식의 한 종류**입니다. 따라서 함수 내에 중괄호(```{}```)를 사용하여 다른 함수 표현식을 추가할 수 있습니다.

앞의 이론에서 살펴보았던 예시를 아래에서 다시 살펴보세요.

함수 내 다른 함수 표현식 사용 예시
```
function formatGreeting(name){
  return "Hello" + ' ' + name;
}

function getGreeting(user) {
  return <h1>Hello, {formatName("elice!")}!</h1>;
}
```

함수 내에 다른 함수 표현식을 사용하는 방법에 대해 실습해 볼까요? 

지시사항에 따라 정의된 함수 getGreeting()에 JSX를 활용하여 인사문구를 출력해봅시다.

### 지시사항

1. 인사문구를 출력하는 함수 getGreeting() 내에서 이름을 출력하는 함수 formatName()을 호출하세요.
2. 호출한 formatName()의 매개변수로 변수 user를 넘겨주세요.
3. getGreeting(user)를 호출한 결과를 element 변수에 저장합니다.


### 해답 코드
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//고객의 이름을 출력하는 함수
function formatName(user){
  return user.lastName + ' ' + user.firstName;
}

//고객의 이름을 저장하는 변수
const user = {
  lastName: '코딩하는',
  firstName: '엘리스'
}

//인사문구를 출력하는 함수
//formatName()함수를 사용해 출력문구를 완성합니다.
function getGreeting(user) {
  return <h1>Hello, {formatName(user)}!</h1>;
}


//getGreeting()의 결과값을 element에 저장합니다.
const element = <h1>{getGreeting(user)}</h1>;

ReactDOM.render(element, document.getElementById('root'));

serviceWorker.unregister();
```
