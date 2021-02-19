# 사용자 리스트 출력

API 사용법을 더 자세히 배워 보겠습니다. 먼저 이번에 사용할 API를 확인해보기 위해 이전에 사용했던 것과 같은 실습을 해보겠습니다.

사용할 API 주소는 아래와 같습니다. 해당 API에는 여러 사용자에 대한 정보가 들어있습니다.

<https://jsonplaceholder.typicode.com/users>

사용자의 이름을 지시사항에 따라 출력해 봅시다!

1. axios.get()을 이용해 주어진 API에 GET 요청을 하세요.
2. .then을 이용해 GET 요청 결과 반환되는 데이터인 response.data를 users state에 저장하세요.
3. map() 함수를 이용해 반환된 데이터들의 name을 출력하세요. 태그는 <li>로 설정하고 각 항목의 키는 users 데이터에 있는 id로 지정하세요.
4. ```<h4>``` 태그로 감싼 텍스트 사용자 리스트를 출력하고, map() 함수를 적용한 결과는 ```<div>``` 태그로 감싸고 출력하세요. 그리고 이 두 태그를 빈 태그(<>)로 감싸세요.

> Tips
자세한 요소 정보는 반환되는 데이터를 콘솔창에 출력하여 확인할 수 있습니다.
렌더링 시 반환되는 HTML에 부모 태그가 없이 자식 태그만 나열하면 오류가 나기 때문에, 빈 태그(<>)라도 감싸줘야 합니다.

```
import React from 'react';
import axios from 'axios';

class Users extends React.Component {
    constructor(props) {
        super(props);

        this.state = {
            users: []
        };
    }

    componentDidMount() {
        // 주어진 API에 GET 요청을 하여 사용자 데이터를 users state에 저장하세요.
        axios.get('https://jsonplaceholder.typicode.com/users')
        .then( response => {
            this.setState({
                users : response.data.map((todo, index) => 
                <li key={index} dangerouslySetInnerHTML={ {__html: todo.name} } >
                </li> )
            })
        })
        
    }

    render() {
        // 출력 결과와 동일하게 출력될 수 있도록 렌더링하세요.
        return (
            <>
                <h4>사용자 리스트</h4>
                <div>
                    {this.state.users}
                </div>
            </>
        );
    }

}

export default Users;
```


