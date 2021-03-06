# 01 Controlled Component 및 State 끌어올리기

> 리액트 고유성을 위한 key 설정 및 사용자가 제출한 폼에 따른 제어 기술을 배워봅니다.

## 1) Forms

폼(form)이란 웹 페이지에서 사용자가 정보를 입력할 수 있도록 만든 HTML의 형태를 의미합니다. 

예시로 회원가입을 위해 입력을 받는 화면이 있는데, 보통은 이러한 화면에서 폼을 통해 입력된 데이터가 서버로 전달되고 데이터베이스에 저장된 데이터를 처리하는 데 사용됩니다. 

즉, 폼은 입력을 위한 양식이라고 생각하면 됩니다. 폼은 ```<form>``` 태그를 이용해 만들 수 있습니다.

아래 예시 코드는 이름(name)값을 받는 HTML 폼입니다.
```
<form>
  <label>
    Name:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="Submit" />
</form>
```

위 폼은 사용자가 폼 내용을 전송(submit)할 때, 기본적으로 새로운 페이지로 이동하는 동작을 합니다. 

만약, React에서도 똑같이 동작하길 원한다면 위 코드와 동일하게 React에서 적용하면 됩니다.

다만 **React에서 폼 엘리먼트는 다른 DOM 엘리먼트와는 조금 다르게 다뤄집니다.**

컴포넌트 렌더링 결과물에 영향을 주는 데이터인 state가 폼 내부에 이미 있기 때문입니다.

폼을 전송하는 function이 필요하거나 사용자가 폼을 입력하는 데이터에 접근을 해야 하는 상황이기 때문에 React에서는 ```Controlled Component(제어 컴포넌트)```를 사용해야 합니다.

## 2) Controlled Component(제어 컴포넌트)

Controlled Component란 **사용자가 state를 제어할 수 있는 컴포넌트**를 말합니다. 

HTML에서 사용하는 폼 엘리먼트 ```<input>, <select>, <textarea>```등을 Controlled Component를 통해 React에서도 동일하게 구현할 수 있습니다.

위에서 설명한 것처럼 **React의 폼 엘리먼트는 각자의 state를 가지고 있으며 사용자가 입력하는 값에 따라 state 값을 자유롭게 업데이트할 수 있습니다.** 

React에서 이러한 state 값은 컴포넌트의 속성이며 **오직 ```setState()```를 사용해서 업데이트**를 할 수 있습니다.
<https://ko.reactjs.org/docs/react-component.html#setstate>

Controlled Component는 ```<input>```처럼 state를 가진 태그를 렌더링하며 또한, ```<input>```의 state를 관리합니다. 아래 코드와 함께 보면서 이해해보겠습니다.

동작하는 순서는 아래와 같습니다.

1. 사용자가 ```<input>```에 값을 입력합니다.
2. onChange에 할당된 handleChange가 실행됩니다.
3. setState()에 의해 state 값이 바뀝니다. 즉, 사용자에게서 입력받은 값으로 바뀝니다.
4. ```<input>```의 value 값에 바뀐 state 값이 할당됩니다.
5. render()가 다시 실행되어 ````<input>````이 렌더링 됩니다.

```
class NameForm extends React.Component { 
  constructor(props) {
    super(props);
    //NameForm이라는 클래스 컴포넌트는 state 값으로 value를 가지고 있는 것을 확인할 수 있습니다.
    //그렇다면, 여기의 value는 무엇일까요? 바로 아래 <input> 태그의 value입니다. value={this.state.value}
    this.state = {value: ''}; 
  }

  handleChange = (event) => {
    //앞에서 부여했던 value의 state 값을 event.target.value로 수정합니다.
    //여기서 event.target.value의 값은 내가 <input> 태그에 입력한 값입니다.
    this.setState({value: event.target.value});
  }

  handleSubmit = (event) => {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return(
      <form onSubmit={this.handleSubmit}>
        <label>
            Name:
            {/*value 값을 할당해주고, onChange로 handleChange 함수를 주고 있습니다. 이때, 이 handleChange 함수는 setState()를 합니다. */}
            <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    )
  }
}
```

> controlled component는 모든 폼 엘리먼트 state가 변화를 handle 하는 handler function을 가지고 있습니다. 

따라서, 사용자에게서 입력을 받거나 입력한 값을 수정하는 것이 간단해집니다. 

만약, 위 코드에서 ```<input>```을 통해 입력받은 값을 모두 대문자로 바꾸고 싶을 때는 아래와 같이 value값을 수정해주면 간단하게 바꿀 수 있습니다.

```
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}
```

### React Form 태그 실습들

#### input 태그

HTML과 React의 폼 사용에 대해 비교해보고 controlled component(제어 컴포넌트)가 언제 쓰이는지 알아봅시다.

** HTML vs React **

HTML은 다양한 입력 폼 엘리먼트를 통해 자신의 state를 관리&업데이트합니다.

반면 React는 변경할 수 있는 자신의 상태가 컴포넌트의 state에 유지되며, setState()에 의해 업데이트됩니다.

이러한 방식으로 React에 의해 값이 제어되는 입력 폼 엘리먼트를 제어하는 컴포넌트를 controlled component라고 합니다.

폼 엘리먼트 종류는 다음과 같으며, 이 외에도 다양한 종류가 존재합니다.

- ```<input>, <textarea>, <select>```
앞으로 위의 세 가지 태그를 가지고 controlled component를 만드는 실습을 진행해 보겠습니다.

이번에는 ```<input>``` 태그를 controlled component를 통해 React에서 구현해 보겠습니다.

사용자로부터 문자, 숫자, 클릭 등의 값을 입력받을 수 있는 태그입니다. 문법은 아래와 같습니다.
```
<input type="타입 명" value="초기 데이터" onChange={이벤트} />
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

// 컴포넌트 내에서 정의된 여러 메소드나 속성을 참조하기 위해 this를 잘 활용하세요.
class InputData extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    // 정의한 이벤트를 바인딩합니다.
    // 바인딩이란 React 컴포넌트에 이벤트를 연결하는 것을 의미하며 bind() 메소드를 이용해서 구현합니다.
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  //state의 값을 변경하는 이벤트
  handleChange(event) {
  // setState를 사용하여 입력된 값을 바탕으로 state의 value값을 변경합니다.
  // handleChange이벤트에서 event.target.value를 사용하여 사용자가 입력한 데이터를 가져올 수 있습니다.
    this.setState({value: event.target.value});
    
  }

  //제출 버튼 클릭 시 경고창을 출력하는 이벤트
  handleSubmit(event) {
    alert('경고! ' + this.state.value);
    event.preventDefault();
  }

  render() {
  //input태그에 handleChange이벤트를 등록합니다.
  //input태그에 value를 설정합니다.
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          경고 문구를 입력하세요:        
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

ReactDOM.render(<InputData />,document.getElementById('root'));

serviceWorker.unregister();
```

#### textarea 태그

```<textarea>``` 태그를 controlled component를 통해 React에서 구현해 봅시다.

```<textarea>``` 태그는 사용자로부터 여러 줄을 입력받는 태그입니다. 입력값이 문자열로 정해져 있기 때문에 type을 지정할 필요는 없습니다. 문법은 아래와 같습니다.
```
<textarea value="초기 데이터" onChange={이벤트} />
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';


class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: '200자 이내의 자기소개서를 입력해주세요'
    };
    //정의한 이벤트를 바인딩합니다.
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  //state의 값을 변경하는 이벤트
  handleChange(event) {
    //setState를 사용하여 입력된 값을 바탕으로 state의 value값을 변경합니다.
    this.setState({value: event.target.value});
  }

  //제출 버튼 클릭 시 경고창을 출력하는 이벤트
  handleSubmit(event) {
    alert(this.state.value);
    event.preventDefault();
  }

  render() {
  //form태그에 handleSubmit이벤트를 등록합니다.
  //textarea태그에 handleChange이벤트를 등록합니다.
  //textarea태그에 value를 설정합니다.
    return (
      <form onSubmit={this.handleSubmit}>
        <h2>당신을 소개하는 글을 200자 이내로 적어주세요.</h2>
          <textarea value={this.state.value} onChange={this.handleChange} />
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

ReactDOM.render(<EssayForm />,document.getElementById('root'));



serviceWorker.unregister();
```

#### select 태그

```<select> 태그는 <option> 태그```와 함께 사용되며 드롭다운 목록을 생성합니다. ```<select>``` 태그의 value 값을 설정하여 초기에 선택되는 옵션을 설정합니다. 문법은 아래와 같습니다.
```
<select value="초기 선택 옵션" onChange={이벤트}>
```
select 태그 예시
```
<select value={this.state.value} onChange={this.handleChange}>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';


class YearOfBirth extends React.Component {
  constructor(props) {
    super(props);
    // 초기 상태 값을 설정합니다.
    this.state = {value: '1990'};
    //정의한 이벤트를 바인딩합니다.
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('태어난 년도: ' + this.state.value);
    event.preventDefault();
  }

  render() {
  //form태그에 handleSubmit이벤트를 등록합니다.
    return (
      <form onSubmit={this.handleSubmit} >
        <label>
          태어난 년도를 선택하세요 : 
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="1960">1960~1969</option>
            <option value="1970">1970~1979</option>
            <option value="1980">1980~1989</option>
            <option value="1990">1990~1999</option>
            <option value="2000">2000~2009</option>
            <option value="2010">2010~2019</option>
            <option value="2020">2020~2029</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
ReactDOM.render(<YearOfBirth />,document.getElementById('root'));



serviceWorker.unregister();
```

#### 다중 입력

사용자로부터 여러 입력값을 받을 때 다중입력을 사용합니다. 

여러 ```<input>``` 엘리먼트를 제어해야 할 때, 각 엘리먼트별로 name 속성을 추가한 후 event.target.name 값을 통해 핸들러의 동작을 결정할 수 있습니다.

> 다중 입력 폼

```
<form>
  제목:
  <input
    name="checkData"
    type="text"
    checked={this.state.checkData}
    onChange={this.handleInputChange} />
<br />
  내용:
  <input
    name="numberData"
    type="text"
    value={this.state.numberData}
    onChange={this.handleInputChange} />
</form>
```

> 입력 처리 이벤트

```
handleInputChange(event) {
  const target = event.target;
  const value = target.value;
  const name = target.name;

  this.setState({
    [name]: value
  })
}
```

- 코드 설명

동일한 이벤트를 사용해 두 개의 ```<input>``` 태그의 입력값을 처리하는 방법입니다. 

태그마다 name을 지정하여 태그를 구분합니다. 이벤트 발생 시 name의 값을 기준으로 state의 값을 변경하여 입력값을 저장합니다.

이를 참고하여 사용자로부터 이름과 나이를 입력받는 페이지를 작성해 봅시다. 이후, 개발자 도구를 통해 저장된 데이터를 확인해봅시다.

> Tips : setState() 내에서 대괄호를 이용해 ```[name]: value```처럼 작성하면, 폼 내에 name별 값을 저장할 수 있습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';


class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: ' ',
      age: 20
    };

    //정의된 이벤트를 바인딩합니다.
    this.handleInputChange = this.handleInputChange.bind(this)
  }
    
  
  handleInputChange(event) {
  //입력된 데이터의 value와 name을 저장합니다.
    const target = event.target;
    const value = target.value;
    const name = target.name;

    //value 와 name을 사용해 입력받은 데이터를 state에 저장합니다.
    this.setState({
      [name]: value
    });
    console.log(this.state.name + ", " + this.state.age);
  }

  render() {
  //이름을 입력받는 태그를 정의합니다.
  //나이를 입력받는 태그를 정의합니다.
    return (
      <form>
        <label>
          이름 :  <input
                    name="name"
                    type="text"
                    value={this.state.name}
                    onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          나이 :  <input
                    name="age"
                    type="number"
                    value={this.state.age}
                    onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}

ReactDOM.render(<Reservation />,document.getElementById('root'));

serviceWorker.unregister();
```

#### Input Null 값 제어

controlled component의 태그 내 value 값을 지정하면 사용자가 값을 변경할 수 없도록 제어할 수 있습니다.

예를 들어, 아래처럼 ```<input>``` 태그의 값을 지정하면 사용자가 값을 변경할 수 없습니다.
```
<input value='haha' />
```

그러지 않고 value의 값을 null로 설정한다면 사용자가 값을 변경할 수 있습니다.
```
<input value={null} />
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

//사용자가 수정할 수 있는 데이터와 수정할 수 없는 데이터를 설정합니다.
const element = (
    <fieldset>
    <legend>개인정보 입력란</legend>
        이름 : 
        <input value='김지우' />
        <br/>
        주민등록번호 : 
        <input value='971029-*******' />
        <br/>
        주소 : 
        <input value={null} />
        <br/>
        전화번호 : 
        <input value={null} />
    </fieldset>
)

ReactDOM.render(element, document.getElementById('root'));

serviceWorker.unregister();
```

## 3) State 끌어올리기

여러 컴포넌트들에 데이터의 변화를 모두 반영해야 할 때, 각 컴포넌트의 state를 통합해야 합니다. 

통합한 state는 가장 가까운 부모 컴포넌트가 관리해야 하는데, 이것을 state 끌어올리기하고 합니다. 

state 끌어올리기는 종종 여러 컴포넌트에 동일한 데이터를 변경하고 반영하고 싶을 때, 공통된 부모 컴포넌트로 통합하고 관리하기 위해서 사용합니다.

### 온도 계산 컴포넌트로 State 끌어올리기

State 끌어올리기를 위한 예제를 만들어 봅시다. 온도의 단위는 화씨와 섭씨 두 가지가 있습니다. 

두 단위 중 하나에 대해 온도를 입력받으면, 다른 단위로 변경하여 출력하고 입력된 온도가 물이 끓는 온도인지 확인하는 코드를 작성하려고 합니다.

즉, 입력되는 온도 하나가 업데이트되면 온도의 출력과 물이 끓는 온도인지에 대한 출력 두 개가 동시에 업데이트되는 컴포넌트가 필요한 것입니다. 해당 state 끌어올리기 예제를 코드를 통해 알아보겠습니다.

가장 먼저, BoilingVerdict라는 컴포넌트를 확인하겠습니다. 

이 컴포넌트는 props로 celsius(섭씨) 온도를 받아 그 온도가 물이 끓을 수 있는 온도인지 나타내는 컴포넌트입니다.
```
function BoilingVerdict(props) {
//100도에서 물이 끓음으로, props로 받은 온도가 끓을 수 있는 온도인지 확인
  if (props.celsius >= 100) {
    return <p>물이 끓습니다.</p>;
  }
  return <p>물이 끓지 않습니다.</p>;
}
```

다음으로 확인해 볼 컴포넌트는 TemperatureInput으로 온도를 입력받아 화면에 표시합니다. 

handleChange 이벤트에서 온도의 변화를 확인하며, **scale 변수는 화씨와 섭씨**를 나타냅니다.
```
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.props.onTemperatureChange(e.target.value);
  }

  render() {
    const temperature = this.props.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

마지막으로 Calculator 컴포넌트(부모 컴포넌트)에서 위의 두 컴포넌트에 대해 State 끌어올리기를 합니다. 

여기서 render() 내 HTML을 확인해보면 온도의 변화에 대해 섭씨와 화씨에 따른 변환과 끓는점인지의 여부를 동시에 확인할 수 있도록 이벤트가 등록되어 있습니다.

```
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    //temperature 값과 scale 값을 state로 할당
    this.state = {temperature: '', scale: 'c'};
  }

//입력한 temperature 값을 scale에 따라 할당
  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        {/*사용자가 온도를 입력하면 scale에 따라 이벤트 동작! */}
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />
        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />
        {/*온도 체크*/}
        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }
}

ReactDOM.render(
  <Calculator />,
  document.getElementById('root')
);
```




# 환율 변환 계산기 컴포넌트 제작

그동안 익힌 내용을 바탕으로 환율 계산 페이지를 작성합니다. 페이지를 작성하는 절차는 크게 5가지로 나뉩니다.

1. 원화 입력 컴포넌트 제작
2. 달러 입력 필드 추가
3. 환율 변환 함수 작성
4. State 끌어올리기
5. 두 필드 동기화

이번 실습에서는 그 중 첫 번째 단계인 사용자로부터 값을 입력받는 원화 입력 컴포넌트 제작을 진행합니다.

## 원화 입력 컴포넌트

1. constructor() 메소드에서 money의 state를 빈 문자열로 초기화하고 handleChange 이벤트를 바인딩하세요.
2. setState()를 이용해 사용자로부터 입력받은 원화를 money에 저장하는 handleChange 이벤트를 정의하세요.
3. render() 메소드에서 원화를 입력받는 아래의 HTML 코드를 반환하세요.
```
<fieldset>
<legend>환율 계산기</legend>
원화: <input
    value={this.state.money}
    onChange={this.handleChange} />
</fieldset>
```
4. MoneyInput 컴포넌트를 ReactDOM에 렌더링하세요.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

// Calculator 클래스 컴포넌트를 정의합니다.
class MoneyInput extends React.Component {
  constructor(props) {
    super(props);
    // money의 state 초기화 및 이벤트 바인딩합니다.
    this.state = {money: ' '};
    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(event) {
    // 입력받은 원화를 money에 저장합니다.
    this.setState({money: event.target.value});
  }

  render() {
    const KRW = this.state.money;
    // 원화를 입력받는 아래의 HTML 코드를 반환합니다.
    <fieldset>
    <legend>환율 계산기</legend>
    원화: <input
        value={this.state.money}
        onChange={this.handleChange} />
    </fieldset>
  };
}


//정의한 Calculator 컴포넌트를 ReactDOM에 렌더링합니다.
ReactDOM.render(<MoneyInput />,document.getElementById('root'));

serviceWorker.unregister();
```

## 달러 입력 필드 추가

이번 실습에서는 두 번째 단계인 **달러 입력 필드 추가**를 진행해 보겠습니다. 

기존에 제작한 원화를 입력받는 컴포넌트 MoneyInput을 재사용하여 달러 입력 필드를 추가합니다.

1. React.Component를 상속받는 Calculator 클래스 컴포넌트를 생성하세요.
2. Calculator 컴포넌트의 render() 메소드 내에서 아래 HTML을 반환하세요.
```
    <div>
        <MoneyInput unit="K" />
        <MoneyInput unit="D" />
    </div>
```
3. Calculator 컴포넌트를 ReactDOM에 렌더링합니다.

> Tips
- render()에서 반환되는 HTML은 MoneyInput을 2번 호출하여 2개의 입력 필드를 생성하고 있습니다. MoneyInput 호출 시, 원화와 달러를 구분하기 위해 props를 추가한 것입니다.
  - 원화 props: unit="K"
  - 달러 props: unit="D"

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

const unitNames = {
  K: '원화',
  D: '달러'
};

class MoneyInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {money: ''};
  }

  handleChange(e) {
    this.setState({money: e.target.value});
  }

  render() {
    const unit = this.props.unit;
    return (
      <fieldset>
        <legend>환율 계산기</legend>
        {unitNames[unit]}: <input
          value={this.state.money}
          onChange={this.handleChange} />
      </fieldset>
    );
  }
}

//Calculator 클래스 컴포넌트를 생성합니다.
class Calculator extends React.Component {
    constructor(props) {
        super(props);
    }
    
    render() {
        return(
                <div>
                    <MoneyInput unit="K" />
                    <MoneyInput unit="D" />
                </div>
        )
    }
}



//정의한 Calculator 클래스를 ReactDOM에 렌더링합니다.
ReactDOM.render(<Calculator />,document.getElementById('root'));

serviceWorker.unregister();
```

## 환율 변환 함수 작성

이번 실습에서는 세 번째 단계인 환율 변환 함수 작성을 진행합니다. 

환율을 변환하는 함수로 원화를 달러로 변환하는 함수와 달러를 원화로 변환하는 함수 2개를 만들어 봅시다.

1. 원화를 달러로 변경하는 함수 toDollar()를 정의하세요. 인자값으로 원화를 받은 후, 달러로 변경하여 반환하세요.
  - 달러(dollar) = 원화(KRW) * 0.00091
2. 달러를 원화로 변경하는 함수 toKRW()를 정의합니다. 다음 공식을 이용해 인자값으로 달러를 받은 후, 원화로 변경하여 반환합니다.
  - 원화(KRW) = 달러(dollar) * 1098.23

> Tips
- tryConvert(): 문자열로 된 금액과 변환함수를 인자값으로 받아 환율을 계산한 후, 문자열로 결과를 반환하는 함수입니다.
- calcKRW: 입력된 컴포넌트가 달러일 경우 환율 변환 함수를 호출합니다. 입력된 컴포넌트가 원화일 경우 그대로 money 값을 받습니다.
- calcDollar: 입력된 컴포넌트가 원화일 경우 환율 변환 함수를 호출합니다. 입력된 컴포넌트가 달러일 경우 그대로 money 값을 받습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

const unitNames = {
  K: '원화',
  D: '달러'
};

//원화를 달러로 변경하는 toDollar 함수를 정의합니다.
function toDollar(krw) {
    return krw*0.00091;
}

//달러를 원화로 변경하는 toKRW 함수를 정의합니다.
function toKRW(dollar) {
    return dollar*1098.23;
}

// tryConvert : 문자열로 된 금액과 변환함수를 인자값으로 받아 환율을 계산한 후, 문자열로 결과를 반환하는 함수입니다.
function tryConvert(temperature, convert) {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return '';
  }
  const output = convert(input);
  return output.toString();
}

class MoneyInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {money: ''};
  }

  handleChange(e) {
    this.setState({money: e.target.value});
  }

  render() {
    const unit = this.props.unit;
    const money = this.state.money;
    // 입력된 컴포넌트가 달러일 경우 환율 변환 함수를 호출합니다. 입력된 컴포넌트가 원화일 경우 그대로 money 값을 받습니다.
    const calcKRW = unit === 'D' ? tryConvert(money, toKRW) : money;
    const calcDollar = unit === 'K' ? tryConvert(money, toDollar) : money;
    return (
      <div>
      <fieldset>
        <legend>환율 계산기</legend>
        {unitNames[unit]}: <input
          value={money}
          onChange={this.handleChange} />
          
      </fieldset>
      원화: {calcKRW}
      <br/>
      달러: {calcDollar}
      </div>
    );
  }
}

class Calculator extends React.Component {
  render() {
    return (
      <div>
        <MoneyInput unit="K" />
        <MoneyInput unit="D" />
      </div>
    );
  }
}

ReactDOM.render(<Calculator/>, document.getElementById('root'));
```

## State 끌어올리기

이번 실습에서는 네 번째 단계인 State 끌어올리기를 진행합니다. 

이전 실습에서 진행한 실습에서는 두 MoneyInput 컴포넌트가 독립적으로 money state를 저장합니다. State 끌어올리기를 적용해 이를 해결할 수 있습니다.

컴포넌트들이 동일한 state를 공유하고 싶은 경우에 사용합니다.

컴포넌트 간의 가장 가까운 공통 조상으로 state를 끌어올린 후, 각 컴포넌트에서 조상 컴포넌트의 state를 참조합니다. 

이러한 방식을 통해 컴포넌트들이 동일한 state를 사용할 수 있습니다.

아래 순서를 참고하세요!

1. state를 조상 컴포넌트에 저장합니다.
2. 자식 컴포넌트 호출 시, 아래의 값을 props로 제공합니다.
  - 컴포넌트 구분자
  - state 데이터
  - setState 이벤트
```
<MoneyInput 
unit="D" 
money={money} 
onMoneyChange={this.handleMoneyChange} />
```
3. 자식 컴포넌트에서 필요한 props를 추출하여 사용합니다.
```
const money = this.props.money;
```

직접 MoneyInput 컴포넌트에 존재하는 state를 공통조상인 Calculator 컴포넌트로 끌어올려 봅시다. 이를 통해 원화와 달러가 같은 state를 공유할 수 있습니다.

1. MoneyInput 컴포넌트의 handleChange에서 데이터의 참조 방식을 아래처럼 props를 참조하는 방식으로 변경하세요.
```
this.props.onMoneyChange(e.target.value);
```
2. handleKRWChange 함수와 handleDollarChange 함수에서 money의 state를 매개변수 money로 설정하세요.
3. render() 함수 내 onMoneyChange이벤트와 handleKRWChange 함수를 연결하는 코드, handleDollarChange 함수를 연결하는 코드를 작성하세요.

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';


const unitNames = {
  K: '원화',
  D: '달러'
};

function toDollar(krw) {
  return krw*0.00091;
}

function toKRW(dollar) {
  return dollar*1098.23;
}

function tryConvert(temperature, convert) {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return '';
  }
  const output = convert(input);
  return output.toString();
}

class MoneyInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
  }
  
  // 참조 방식을 props를 참조하는 방식으로 변경하세요.
  handleChange(e) {
    // this.setState({money: e.target.value});
    this.props.onMoneyChange(e.target.value);
  }

  render() {
    const unit = this.props.unit;
    const money = this.props.money;
    const calcKRW = unit === 'D' ? tryConvert(money, toKRW) : money;
    const calcDollar = unit === 'K' ? tryConvert(money, toDollar) : money;

    return (
      <div>
      <fieldset>
        <legend>환율 계산기</legend>
        {unitNames[unit]}: <input
          value={money}
          onChange={this.handleChange} />
          
      </fieldset>
      원화: {calcKRW}
      <br/>
      달러: {calcDollar}
      </div>
    );
  }
}

class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleKRWChange = this.handleKRWChange.bind(this);
    this.handleDollarChange = this.handleDollarChange.bind(this);
    this.state = {money: ''};
  }

  // money의 state를 매개변수 money로 설정하세요.
  handleKRWChange(money) {
    this.setState({money: money});
  }
  handleDollarChange(money) {
    this.setState({money: money});
  }

  render() {
    const money = this.state.money;
    return (
      <div>
        {/* 함수와 이벤트를 연결하는 코드를 작성하세요. */}
        <MoneyInput unit="K" money={money} onMoneyChange={this.handleKRWChange} />
        <MoneyInput unit="D" money={money} onMoneyChange={this.handleDollarChange} />
      </div>
    );
  }
}

ReactDOM.render(<Calculator/>, document.getElementById('root'));

serviceWorker.unregister();
```

## 두 필드 동기화

이번 실습에서는 다섯 번째 단계인 두 필드 동기화를 진행해보겠습니다.

이전 실습을 통해 컴포넌트들이 동일한 state를 사용하도록 수정했습니다. 이번 실습에서는 환율을 계산하는 기능을 동기화해봅시다.

1. 삼항 연산자를 사용하여 정의된 calcKRW를 참고하여 calcDollar를 정의하세요. 입력된 컴포넌트가 원화일 경우 환율 변환 함수를 호출하고 달러일 경우 그대로 money 값을 받도록 하세요.

2. render() 내 HTML 반환 시 MoneyInput 컴포넌트 호출 시 props로 onMoneyChange로 정의된 이벤트인 handleKRWChange와 handleDollarChange을 각각 알맞게 넘겨주세요.

> Tips

- ender() 내에서 컴포넌트 호출 시, 아래의 값들을 props로 제공합니다.
  - 컴포넌트 구분자
  - state 데이터
  - setState 이벤트
- 삼항 연산자는 변수 = 조건식? 참일 때 대입할 값 : 거짓일 때 대입할 값; 과 같은 형태로 사용되는 연산자입니다.

------
