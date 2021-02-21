# Axios란?

Axios는 웹 브라우저와 Node.js를 위한 HTTP 비동기(작성된 순서대로 실행되지 않는 처리) 통신 라이브러리입니다. 쉽게 말해서 백엔드와 프론트엔드 간 통신을 쉽게 하기 위해 사용되는 것으로 Ajax처럼 사용되는 것입니다. **비동기 통신 라이브러리를 사용하지 않으면 모든 코드가 순차적으로 처리되어야 하므로 코드의 순서를 신경 써서 작성해야 합니다. 즉, 코드 작성이 매우 복잡해집니다.** 따라서 비동기 통신을 쉽게 해주는 Axios나 Ajax 같은 것이 자주 사용되는 것입니다.

Ajax란 비동기 자바스크립트란 의미로 **Asynchronous JavaScript and XML**의 약자입니다. Ajax는 브라우저가 가지고 있는 XMLHttpRequest 객체를 이용하여 화면 전체를 새로 고침 하지 않고 변경된 일부 데이터만 로드하는 비동기 처리가 가능합니다. **Axios는 React에서 제공하는 Ajax와 유사하며 OpenAPI를 이용한 통신을 할 때 주로 사용**합니다.

Axios는 Promise를 기반으로 만들어진 라이브러리입니다. Promise는 자바스크립트 ES6에서 비동기 처리를 위해 주로 사용되는 객체입니다.

## CRUD

CRUD가 Create, Read, Update, Delete의 제일 앞 문자를 하나씩 따와 만든 줄임말이었던 것을 기억하시나요? 또한 CRUD 각각은 아래처럼 매칭이 되었습니다.
- C : Create(생성) - POST
- R : Read(조회) - GET
- U : Update(수정) - PUT
- D : Delete(삭제) - DELETE

### Axios 사용법

React에서 Axios를 사용하는 방법에 대해 알아봅시다. 먼저 아래와 같이 import를 해줘야 합니다.
```
import axios from 'axios'
```
각 메소드가 어떠한 형태로 사용되는지 아래에서 살펴보세요.

### POST
```
axios.post(url, data 객체)
```
POST는 새로운 자원을 생성할 때 사용합니다.
```
import React from 'react';
import axios from 'axios';

class Users extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: ""
        };
    }

    componentDidMount() {
        // 삽입할 데이터 객체를 선언하세요.
        const data = { "email": "eve.holt@reqres.in", "password": "cityslicka" }
        // axios.post를 호출하고 result에 반환되는 토큰 값을 저장하세요.
        axios.post('https://reqres.in/api/login', data)
        .then( response => {
            this.setState({
                result : response.data.token
            })
        })
        
    }

    render() {
        const { result } = this.state;
        return (
            <div>
                <h4>React Axios로 HTTP POST 요청하기</h4>
                <div>
                    Token: {result}
                </div>
            </div>
        );
    }

}

export default Users;
```

### GET
```
axios.get(url)
```
GET은 자원을 요청할 때 사용합니다.
```
import React from 'react';
import axios from 'axios';

class Users extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: ""
        };
    }

    componentDidMount() {
        // axios.post를 호출하고 result에 반환되는 데이터를 저장하세요.
        axios.get('https://reqres.in/api/users/2')
        .then( response => {
            console.log(response)
            this.setState( {
                result : response.data.data
            })
        })

        
    }

    render() {
        const { result } = this.state;
        return (
            <div>
                <h4>React Axios로 HTTP GET 요청하기</h4>
                <div>
                    {/* result를 이용해 출력 결과와 동일하게 출력하세요. */}
                    Name : {result.first_name+ ' ' +result.last_name} <br/>
                    Email : {result.email}
                </div>
            </div>
        );
    }

}

export default Users;
```

### PUT
```
axios.put(url, data 객체)
```
PUT은 자원을 갱신할 때 사용합니다.
```
import React from 'react';
import axios from 'axios';
// DB의 정보가 수정되는 것은 아니다!!!
class Users extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: ""
        };
    }

    componentDidMount() {
        // 수정할 데이터를 선언하세요.
        const data = { "first_name": "White", "last_name": "Rabbit" , "email": "alice@elice.io" }
        //  axios.put을 호출하고 result에 반환되는 사용자 데이터를 저장하세요.
        axios.put('https://reqres.in/api/users/2', data)
        .then( response => {
            this.setState({
                result : response.data
            })
        })
        
    }

    render() {
        const { result } = this.state;
        return (
            <div>
                <h4>React Axios로 HTTP PUT 요청하기</h4>
                <div>
                    Name: {result.first_name + " " + result.last_name} <br/>
                    Email: {result.email} <br/>
                    Update Date: {result.updatedAt} <br/>
                </div>
            </div>
        );
    }

}

export default Users;
```

### DELETE
```
axios.delete(url)
```
DELETE는 자원을 삭제할 때 사용합니다.
```
import React from 'react';
import axios from 'axios';
// 실제로 서버에 있는 데이터가 삭제되지는 않는다!!
class Users extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: ""
        };
    }

    componentDidMount() {
        // axios.delete를 호출하고 result에 반환되는 HTTP 응답 코드를 저장하세요.
        axios.delete("https://reqres.in/api/users/2")
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
                <h4>React Axios로 HTTP DELETE 요청하기</h4>
                <div>
                    {/* result를 이용해 출력 결과와 동일하게 출력하세요. */}
                    Status: {result}
                </div>
            </div>
        );
    }

}

export default Users;
```

PUT과 DELETE는 **REST 기반 API 프로그램에서 데이터베이스에 저장된 내용을 다룰 때 사용되는 메소드입니다. OpenAPI를 다룰 때는 사용할 일이 거의 없습니다.** Axios 메소드가 사용되는 방법은 이후 실습에서 자세히 알아보겠습니다!

### 백엔드

이번에는 직접 API를 만들고, 해당 API를 이용해 HTTP 요청을 해보겠습니다.

즉 직접 백엔드 서버를 구동하고 프론트엔드에서 서버에 있는 데이터를 가져오는 것입니다!

오른쪽 코드는 여러분들이 Flask를 실습하셨을 때 살펴보았던 코드입니다. jsonify를 통해 JSON 데이터를 반환하는 get 메소드를 가진 HelloElice 클래스를 이용해 간단한 API를 만든 실습입니다.

이번 실습에서 백엔드 서버를 구동시키고, 다음 실습에서 프론트엔드를 구현해봅시다!
```
from flask import Flask, jsonify
from flask_restful import reqparse, abort, Api, Resource

app = Flask(__name__)
api = Api(app)


class HelloElice(Resource):
    def get(self):
        # msg 변수에 dictionary type으로 메세지를 입력해보세요!!
        msg = {"message" : "Hello Elice!"}
        return jsonify(status = "success", result = msg)

api.add_resource(HelloElice, '/')

if __name__ == '__main__':
    app.run()
```

### 프론트엔드

앞선 실습에서 백엔드 서버를 구동시켰습니다. 해당 API 주소에 GET 요청을 해봅시다.

앞에서 실습했던 axios.get() 메소드를 이용해 API에서 반환했던 message를 호출할 수 있습니다.

그런데 그냥 호출하면 콘솔창에서 다음과 같은 에러가 나오며 제대로 GET 요청이 되지 않습니다.
image

왜냐하면 교차 출처 리소스 공유 (CORS) 문제 때문인데, 쉽게 말하면 구현한 백엔드에 접근할 권한이 없는 것입니다. 자세한 내용은 바로 다음 장에서 학습하겠습니다.

이것을 해결할 수 있는 간단한 방법은 백엔드 서버에 우회하여 접근하는 것입니다. 아래 링크를 들어가 봅시다.

<https://cors-anywhere.herokuapp.com/>

그러면 아래와 같은 화면이 나오고, 버튼을 클릭하면 해당 주소를 통해 서버를 우회하여 접근할 수 있게 됩니다.

위의 서버 우회를 위한 주소와 백엔드 실습에서 복사한 주소를 합하여 해당 백엔드 서버에 우회하여 접속할 수 있습니다. 그렇다면 지시사항에 따라 직접 만든 API에 HTTP 요청을 해봅시다!
```
import React from 'react';
import axios from 'axios';

class Messages extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            result: "",
        };
    }

    componentDidMount() {
        // 백엔드 API 주소를 입력하세요.
        axios.get('https://cors-anywhere.herokuapp.com/fsxbrjteflccrbexrhaz6jecemkomed0.runner-forwarder-a-02.elice.io/?_=419981')
            .then(response => this.setState({ result: response.data.result.message }));
    }

    render() {
        const { result } = this.state;
        return (
            <div>
                <h5>HTTP GET 요청</h5>
                <div>
                    Message: {result}
                </div>
            </div>
        );
    }

}

export default Messages;
```

### OpenAPI 사용

axios.get()을 이용해서 네이버 OpenAPI를 사용해봅시다. 요청할 url은 아래와 같습니다.

<https://openapi.naver.com/v1/search/shop>

기존에는 GET 요청할 url만 넘겨주었지만, 이번에는 검색어인 query와 키 정보를 같이 넘겨주어야 합니다. 요청 변수와 출력 결과에 대한 정보는 링크에 자세히 나와 있습니다.

즉, 아래처럼 GET 요청을 해주면 됩니다..
```
axios.get( 요청할 url,
    { params: { query: 검색어 }, 
      headers: {'X-Naver-Client-Id': Client ID, 'X-Naver-Client-Secret': Client Secret}
    })
```
이후 .then을 이용하여 반환된 상태 코드를 확인해봅시다.
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
        axios.get('https://openapi.naver.com/v1/search/shop',
            { params: { query: '더치커피' }, 
              headers: {'X-Naver-Client-Id': 'TVug9wlxUWhSpdoEWCgw', 'X-Naver-Client-Secret': 'WqsufT0Bgk'}
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
