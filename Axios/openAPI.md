# API

OpenAPI에 대해 알아보기 전에 API에 대해 먼저 알아봅시다. API는 **Application Programming Interface**의 줄임말로 **다양한 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스**를 말합니다.

만약 여러분이 밥을 먹기 위해 식당을 갔다고 해봅시다. 손님인 여러분은 요리사에게 음식 주문을 해야 밥을 먹을 수 있습니다. 하지만 직접 요리사에게 말하지는 않죠. 일반적인 경우 점원을 통해 주문을 할 텐데요. 이때 점원 역할이 바로 API라고 생각하시면 됩니다. 즉, 프로그램과 프로그램을 연결해 주는 다리 역할을 하는 것이 API입니다.

## OpenAPI

그렇다면 OpenAPI는 무엇인지 알아보겠습니다. OpenAPI(Open Application Programming Interface, Open API, 공개 API)는 누구나 사용할 수 있도록 공개되어 개발자에게 사유 응용 소프트웨어나 웹 서비스에 프로그래밍적인 권한을 제공하는 API입니다. 말 그대로 누구에게나 공개된 API가 OpenAPI입니다.

즉, 누구나 음식점에 들어와서 주문을 하고 음식을 먹을 수 있다는 의미입니다! OpenAPI의 예시로는 국가에서 제공하는 데이터인 공공데이터 포털 또는 네이버의 데이터 등 다양하게 있습니다.

### OpenAPI를 사용하는 이유

위의 예시에 등장한 것처럼 다양한 OpenAPI들이 있습니다. 이러한 데이터들로 자신만의 서비스를 만들고 싶다면 OpenAPI를 활용해야 합니다. OpenAPI를 이용하여 개발하는 방법은 어느 정도 획일화되어 있기 때문에 다른 사람들과 협업하기가 편리합니다. 

또한 코드를 작성하는 시간이 절약되어 개발 비용이 절감되는 장점이 있습니다. OpenAPI를 사용하지 않고 스스로 모든 풀스택 개발을 하는 것은 정말 어렵습니다. 또한 OpenAPI를 사용하면 API 테스트를 통한 품질 보장이 가능하고 사용자와의 상호작용을 중요시하는 서비스를 개발할 수 있습니다.

### OpenAPI를 제공하는 이유

이번에는 기업들이 왜 OpenAPI를 제공하는지 알아보겠습니다. 기업들은 다양한 서비스나 기술을 제공하지만 사용자가 원하는 모든 것을 충족하기는 것은 쉽지 않습니다. 따라서 기업들은 OpenAPI를 고객들에게 제공함으로써 사용자가 기업의 서비스나 기술을 유연하게 이용할 수 있도록 합니다. 즉, **고객이 자신의 요구에 적합한 방식으로 서비스를 이용할 수 있다는 것을 의미하며 기업은 고객과의 관계를 강화**할 수 있게 됩니다.

이렇게 고객이 원하는 방식으로 만들어진 인터페이스는 다른 사람들에게도 공유됩니다. 공유된 방식은 좀 더 확장되어 API를 제공한 기업에서 자사의 서비스에 통합할 수 있습니다. 개발자들이 기업의 API를 연구하고 통찰하여 새로운 서비스를 만들어내면, 기업은 그것을 참고하여 고객이 진정으로 원하는 서비스가 무엇인지 더 고민할 수 있는 계기가 됩니다.

### 애플리케이션 등록

네이버에서 제공하는 OpenAPI를 사용하기 위해 애플리케이션 등록을 진행하는 방법을 알아보겠습니다. 네이버 OpenAPI를 이용하기 위해서는 네이버에 로그인이 필요합니다. 아래 순서에 따라 애플리케이션 등록을 진행해봅시다. 자세한 설명은 링크에도 소개되어 있으니 참고 바랍니다!

1. 링크<https://developers.naver.com/apps/#/register?defaultScope=search>에 접속합니다.
2. 해당 화면에서 애플리케이션 이름은 자유롭게 채워주세요. 그리고 사용 API에는 검색을 선택하고 비로그인 오픈 API 서비스 환경에는 http://localhost를 입력하세요.

- 애플리케이션 이름: 자신이 신청한 OpenAPI의 이름입니다.
- 사용 API: 사용할 OpenAPI를 선택합니다. 앞으로의 실습에서는 검색 API를 활용할 것이기 때문에 검색을 선택해줍니다.
- 비로그인 오픈 API 서비스 환경: 네이버 OpenAPI에 로그인을 하고 사용해야 하는 것과 그렇지 않은 것이 있는데, 비로그인 환경에서 사용할 도메인 주소를 입력합니다. 일반적으로 http://localhost를 입력해주면 됩니다.

3. 애플리케이션 등록이 완료되면 아래와 같은 Client ID와 Client Secret을 얻을 수 있습니다. 해당 키를 가지고 OpenAPI에 접근할 수 있습니다. 부여되는 키는 개인의 것이므로 공유되지 않도록 유의해야 합니다.

- Client ID: OpenAPI 사용에 대한 인증 및 권한 부여에 사용되는 사용자의 ID입니다.
- Client Secret: OpenAPI 사용에 대한 인증 및 권한 부여에 사용되는 사용자의 비밀번호입니다.

> API를 호출할 수 있는 횟수가 일별로 제한되어 있음을 참고 바랍니다. 더불어 네이버 OpenAPI 외에도 다양한 OpenAPI가 존재하기 때문에 이번에 익힌 사용법을 바탕으로 구현하고 싶은 기능에 맞는 데이터를 찾아 사용하면 됩니다!


#### Postman

앞서 생성한 OpenAPI 애플리케이션이 잘 생성되었는지 Postman을 이용해서 확인해봅시다. Postman은 API를 테스트하기 위한 도구로 사용되며, 링크에서 다운로드를 받을 수 있으며 크롬 확장 프로그램으로 설치하여 이용할 수도 있습니다. Postman 설치 후 아래 과정에 따라 API 테스트를 진행해봅시다.

##### API 테스트

1. Collections를 선택한 후 + 버튼을 눌러 새로운 Collection을 만드세요.

2. Collection의 이름을 자유롭게 설정한 후 Add a request를 클릭하여 새로운 request를 만드세요.

3. HTTP 요청 상태를 GET으로 설정하고 API 주소 https://openapi.naver.com/v1/search/shop를 입력하세요. 그리고 ?query=컴퓨터와 같은 형태로 검색하고 싶은 단어를 넘겨주시면 됩니다. Params에 KEY와 VALUE 값을 직접 입력해도 괜찮습니다! 즉, query에 입력된 것이 검색어입니다. 다른 요청 변수에 대한 설명은 링크를 참조하시면 됩니다.

4. 다음으로 Headers에서 OpenAPI를 생성했을 때 받은 키를 넘겨줍니다. KEY X-Naver-Client-Id에 VALUE는 생성한 애플리케이션에서 얻은 Client ID를 넘겨주고, KEY X-Naver-Client-Secret에 VALUE는 생성한 애플리케이션에서 얻은 Client Secret을 넘겨줍니다.

5. 마지막으로 Send 버튼을 클릭하고 요청 결과를 확인하세요!

6. GET 이외의 요청 : 
만약 GET 이외의 다른 API 요청을 하고 싶으면 아래 사진처럼 GET 이외에 다른 요청으로 설정해주면 됩니다. 단, 요청을 할 API가 다른 요청을 허용하는지 확인해야 합니다!

### OpenAPI 사용 실습

axios.get()을 이용해서 네이버 OpenAPI를 사용해봅시다. 요청할 url은 아래와 같습니다.

<https://openapi.naver.com/v1/search/shop>

기존에는 GET 요청할 url만 넘겨주었지만, 이번에는 검색어인 query와 키 정보를 같이 넘겨주어야 합니다. 요청 변수와 출력 결과에 대한 정보는 링크에 자세히 나와 있습니다.

즉, 아래처럼 GET 요청을 해주면 됩니다.
```
axios.get( 요청할 url,
    { params: { query: 검색어 }, 
      headers: {'X-Naver-Client-Id': Client ID, 'X-Naver-Client-Secret': Client Secret}
    })
```
이후 .then을 이용하여 반환된 상태 코드를 확인해봅시다.

1. componentDidMount()에서 axios.get(요청할 url, params와 headers 정보)을 넘겨주세요.
2. .then을 이용하여 요청 시 반환되는 응답 코드인 response.status를 state인 result 변수에 저장하세요.
3. 요청할 url을 우회하지 않으면 아래와 같은 내용을 콘솔창에서 확인하실 수 있습니다. 왜 이러한 에러가 발생하는 것인지 다음 이론에서 살펴보겠습니다.

> Tips : 이번 실습에서는 CORS 문제 때문에 정상적인 값을 확인할 수 없습니다. 해당 원인에 대해 다음 이론에서 살펴보겠습니다.
```
import React from 'react';
import axios from 'axios';

class Shopping extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: []
        };
    }

    componentDidMount() {
        
        // axios.get을 호출하고 result에 반환되는 HTTP 응답 코드를 저장하세요.
        axios.get('https://openapi.naver.com/v1/search/shop', {
            params: { query: '핸드폰' },
            headers: {'X-Naver-Client-Id': '3GBzYi_GDx_npg9zr93n', 'X-Naver-Client-Secret': 'qcNdRdrfgh'}
        })
        .then( response => {
            this.setState({
                result : response.status
            })
        })
        
    }

    render() {
        const { result } = this.state;
        
        return (
            <div>
                <h4>HTTP 상태 코드</h4>
                <div>
                    {result}
                </div>
            </div>
        );
    }

}

export default Shopping;
```

# CORS

이전 실습에서 네이버 OpenAPI의 접근이 CORS 문제 때문에 정상적인 실행이 되지 않았습니다. 도대체 CORS가 무엇인지 한 번 살펴보겠습니다.

## CORS란?

CORS란 **Cross-Origin Resource Sharing**의 줄임말로 **한 애플리케이션이 다른 도메인의 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 것**을 말하며 애플리케이션이 사용할 자원을 가진 서버의 도메인이 자신의 도메인과 다를 때 실행합니다. 예를 들어, https://domain-a.com 도메인을 사용하는 프론트엔드에서 https://domain-b.com/data.json 도메인을 사용하는 백엔드에 있는 API 요청을 할 때 CORS가 사용됩니다.

기존에는 서버에 있는 자원을 사용할 때 다른 외부의 접근은 해킹과 같은 악의적인 목적뿐일 것으로 생각했습니다. 그래서 이러한 자원 요청을 차단하였지만, 최근에는 OpenAPI 같은 것이 등장하면서 외부의 접근이 자연스러워졌습니다. 그에 따라 서로 다른 도메인의 자원에 접근이 가능하도록 CORS가 만들어진 것입니다.

## CORS 에러

CORS를 이용해 외부 자원에 접근할 수는 있지만, 서버에서 무조건 이를 허용하는 것은 아닙니다. 여전히 악의적인 목적으로 자원을 이용할 여지가 있기 때문입니다. 네이버에서도 다른 사람의 클라이언트 키를 도용해서 API를 호출하는 것을 막기 위해서 무조건 CORS를 허용하지는 않습니다. 또한 API 사용 시 CORS를 지원하지 않는 경우도 있기 때문에 해결 방법을 알아두는 것이 좋습니다.

## 에러 해결 방법

CORS 에러를 해결하기 위한 다양한 방법이 있습니다. 한 가지 예시로 백엔드에서 특정 도메인에 대한 CORS를 허용함으로써 CORS 에러를 해결할 수 있습니다. 하지만 이는 OpenAPI에서 사용하기는 쉽지 않은 방법입니다.

다른 방법으로 JSONP를 이용하는 방법이 있는데, HTML의 <script> 태그는 보안 정책이 적용되지 않는다는 점을 이용하여 외부 자원을 JSON 형태로 변환해 데이터를 받아오는 방법입니다.

그 외에도 다양한 해결 방법이 있지만, 앞 장에서 잠깐 살펴본 프록시 설정을 통해 문제를 해결할 수 있습니다. 서버와 사용자 간에 통신을 할 때 중계기 역할을 하는 것이 프록시 서버입니다. 즉, API와 사용자 간에 프록시 설정을 하여 서버의 자원을 프록시 서버에서 받아오고 사용자에게는 CORS가 허용된 것처럼 HTTP 요청을 허용해주는 것입니다.

React 프로젝트에서 프록시 설정도 가능하지만, <https://cors-anywhere.herokuapp.com/>을 이용하면 CORS 프록시 설정을 간편하게 할 수 있습니다. 해당 주소 뒤에 사용할 API 주소를 이어 붙이기만 하면 됩니다. 사용 시 버튼 클릭을 통해 기능을 활성화만 해주면 됩니다!


### CORS 프록시 실습

CORS 에러 때문에 출력 결과가 제대로 나오지 않았던 실습을 프록시로 해결해봅시다.

작성했던 코드의 API 주소에 앞에 아래 주소를 이어붙이면 됩니다.

<https://cors-anywhere.herokuapp.com/>

다시 한번 OpenAPI GET 요청에 대한 상태 코드를 확인해 볼까요?

1. [실습1]에서 발생했던 에러를 프록시를 통해 해결하세요.

> Tips : 프록시를 사용해도 해결되지 않는 경우 프록시 주소로 들어가 Request temporary access to the demo server 버튼을 눌러주세요!
한 번 허용해주면 계속되는 것이 아니기 때문에 이후 실습에서 실행이 안 되는 경우 프록시 주소로 들어가 버튼을 눌러주시기 바랍니다.
```
import React from 'react';
import axios from 'axios';

class Shopping extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: []
        };
    }

    componentDidMount() {
        
        // axios.get을 호출하고 result에 반환되는 HTTP 응답 코드를 저장하세요.
        axios.get('https://cors-anywhere.herokuapp.com/https://openapi.naver.com/v1/search/shop', {
            params: { query: '컴퓨터' },
            headers: {'X-Naver-Client-Id': '3GBzYi_GDx_npg9zr93n', 'X-Naver-Client-Secret': 'qcNdRdrfgh'}
        })
        .then( response => {
            this.setState({
                result : response.status
            })
        })
        
    }

    render() {
        const { result } = this.state;
        
        return (
            <div>
                <h4>HTTP 상태 코드</h4>
                <div>
                    {result}
                </div>
            </div>
        );
    }

}

export default Shopping;
```

### 상품 리스트 출력 실습

이제 OpenAPI를 통해 제대로 된 상품 정보를 출력해봅시다.

앞에서 프록시로 우회해서 접근한 API에 GET 요청을 params, headers와 같이 넘겨주었습니다. 그 후 HTTP 상태 코드에 대한 데이터를 받았지만, 이번에는 데이터를 state에 저장해봅시다.

단, 저장된 데이터는 딕셔너리로 이루어진 배열 형태이기 때문에 map을 활용해서 출력해야 합니다. 아래는 index를 이용하여 key값을 부여하여 todos 배열에 있는 딕셔너리들의 key가 text인 value들을 출력하는 코드입니다.
```
const todoItems = todos.map((todo, index) =>
  <li key={index}>
    {todo.text}
  </li>
);
```
위의 코드를 활용하여 컴퓨터를 검색한 결과를 얻어봅시다.

1. 발급받은 자신의 OpenAPI 키를 입력하세요.
2. .then을 이용해 GET 요청 결과 반환되는 아이템인 response.data.items를 result state에 저장하세요.
3. map() 함수를 이용해 반환된 아이템들의 title을 출력하세요. 태그는 <li>로 설정하고 각 항목의 키는 index로 지정하세요.


> Tips :  반환되는 데이터의 구조를 확인하고 싶다면 console.log(response)를 이용해 콘솔창에 출력해보세요.
매번 변하는 OpenAPI이기 때문에 검색 결과는 달라질 수 있습니다.

```
import React from 'react';
import axios from 'axios';

class Shopping extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: []
        };
    }

    componentDidMount() {
        // 자신의 OpenAPI 키를 입력하세요.
        const CLIENT_ID = '3GBzYi_GDx_npg9zr93n';
        const CLIENT_SECRET = 'qcNdRdrfgh';
        
        axios.get('https://cors-anywhere.herokuapp.com/https://openapi.naver.com/v1/search/shop',
            { params: { query: '컴퓨터' }, 
              headers: {'X-Naver-Client-Id': CLIENT_ID, 'X-Naver-Client-Secret': CLIENT_SECRET}
            })
            // axios.get을 호출하고 result에 반환되는 아이템을 저장하세요.
            .then( response => {
                this.setState({
                    result : response.data.items
                })
            })
    }

    render() {
        const { result } = this.state;
        // map() 함수를 이용해 검색된 title을 출력하세요.
        const goods = result.map((todo, index) => 
            <li key={index}>
                {todo.title}
            </li>
        );
        return (
            <div>
                <h4>상품 리스트</h4>
                <div>
                    {goods}
                </div>
            </div>
        );
    }

}

export default Shopping;
```

### dangerouslySetInnerHTML 실습

앞에서 출력된 결과의 일부가 태그로 감싸여 있습니다. 이는 OpenAPI 문서에서 제목에서 검색어와 일치하는 부분은 태그로 감싸고 반환한다고 설명이 되어 있습니다.

이것을 그대로 텍스트로 출력하면 보기가 좋지 않습니다. 따라서 아래처럼 dangerouslySetInnerHTML을 이용하면 HTML 태그를 적용한 결과를 출력할 수 있습니다.
```
<div dangerouslySetInnerHTML={__html: 'HTML 태그가 포함된 문자열'} />
```
앞서 map() 함수를 적용하여 출력했던 결과에 dangerouslySetInnerHTML을 적용하여 보기 좋게 출력해 봅시다.

1. map() 함수를 이용해 출력하는 <li> 태그에 dangerouslySetInnerHTML을 적용하여 HTML 태그가 적용된 title을 출력하세요.


> Tips : dangerouslySetInnerHTML<https://ko.reactjs.org/docs/dom-elements.html#dangerouslysetinnerhtml>에 대한 공식 문서도 확인해보세요!

### 상품 검색 기능 구현 실습

원하는 상품명을 입력하고 검색 버튼을 클릭하면 검색 결과를 반환하는 코드를 작성해봅시다.

지금까지는 componentDidMount()에서 딱 한 번 GET 요청을 하였지만, 여러 번 GET 요청을 하도록 이를 이벤트로 등록해야 합니다.

오른쪽 코드에는 두 가지 state가 존재합니다. search는 <input> 태그에 저장된 검색어가 저장되며 handleChange 이벤트에서 state가 설정됩니다. goods에는 반환되는 데이터가 아래에 대한 map() 함수를 적용한 뒤 저장해야 합니다.
```
(good, index) => (<li key={index} dangerouslySetInnerHTML={{__html: good.title}} ></li>)
```
앞서 작성했던 코드들을 떠올리며 검색 기능을 구현해 봅시다!

1. handleClick 이벤트에서 axios.get()을 이용하여 GET 요청을 하세요. 단, query는 search state를 넘겨주세요.
2. .then을 이용하여 반환된 response.data.items가 출력이 가능하도록 map() 함수를 적용하세요. 그리고 적용한 결과를 goods state에 저장하세요.

> Tips : response.data.items에 map() 함수를 적용한 결과를 임시 변수에 저장하고, setState를 이용해 goods에 임시 변수를 저장하면 됩니다.

```
import React from 'react';
import axios from 'axios';

class Shopping extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            search: '',
            goods: null
        };
    }
    
    handleChange = e => { 
        this.setState({ search: e.target.value }); 
    }
    
    // 버튼 클릭 시 입력된 검색어로 GET 요청을 하고 반환된 결과를 출력 가능한 형태로 state에 저장하세요.
    handleClick = e => {
        const CLIENT_ID = '3GBzYi_GDx_npg9zr93n';
        const CLIENT_SECRET = 'qcNdRdrfgh';
        
        axios.get('https://cors-anywhere.herokuapp.com/https://openapi.naver.com/v1/search/shop',
            { params: { query: this.state.search }, 
              headers: {'X-Naver-Client-Id': CLIENT_ID, 'X-Naver-Client-Secret': CLIENT_SECRET}
            })
            .then(response => this.setState({ goods: response.data.items.map((todo, index) => 
                <li key={index} dangerouslySetInnerHTML={ {__html: todo.title} } >
                </li> 
            )})
        );
        // map() 함수를 이용해 검색된 title에 dangerouslySetInnerHTML을 적용하여 출력하세요.
    }
    

    render() {
        return (
            <div>
                <h4>상품 검색</h4>
                <input onChange={this.handleChange} />
                <button onClick={this.handleClick}> 검색 </button>
                <div>
                    {this.state.goods}
                </div>
            </div>
        );
    }

}

export default Shopping;
```
