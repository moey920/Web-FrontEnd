### 사용자 리스트 출력

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

# 비동기 처리

API 호출 시 비동기 처리를 하지 않으면 API가 응답을 보내주기 전까지 프로그램이 진행되지 않을 것입니다. 앞서 배운 Axios도 .then을 이용한 콜백 함수의 형태로 비동기 처리를 한 것입니다. 하지만 복잡한 비동기 처리를 하기 위해서 .then을 이용한 콜백 함수를 자주 사용하면 가독성이 나빠집니다.
```
axios.get(`요청할 url 1`)
  .then(res => axios.get(`요청할 url 2`))
  .then(res => {
    const ps = res.data.map(user => axios.get(`요청할 url 3`));
    ···
  })
  .then(ress => ···)))
  .then(repoArrs => {
    ···
    }
    ···
  })
```
이러한 것을 콜백 지옥<https://librewiki.net/wiki/%EC%BD%9C%EB%B0%B1_%EC%A7%80%EC%98%A5>이라고 표현합니다. 콜백 지옥을 벗어나기 위해 ```async```와 ````await````를 이용할 수 있습니다. **즉, 콜백 함수와 .then을 사용하지 않고 비동기 처리를 할 수 있는 것**입니다.

## async / await

async와 await에 대해 살펴보기 전에 Promise가 무엇인지 알아봅시다. Promise란 비동기 처리에서 사용되는 객체로 Promise가 상태를 관리함으로써 다른 코드가 비동기적으로 실행될 수 있도록 해주는 객체입니다. 앞서 배웠던 Axios 역시 Promise를 기반으로 만들어진 것입니다. Promise에 대한 자세한 설명은 링크<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise>를 참고하세요!

이제 async와 await을 어떻게 사용해야 하는지 예시를 통해 살펴봅시다. 아래에는 2초 뒤 Promise 객체를 반환하는 함수 ```resolveAfter2Seconds``` 함수와 해당 함수를 호출하는 ```asyncCall``` 함수가 있습니다. resolveAfter2Seconds에서는 2초 뒤에 Promise 객체를 반환합니다. 여기서 resolve는 코드를 이행하는 것으로 resolved라는 문자열을 반환하게 됩니다.
```
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
}

asyncCall();
```
코드 실행 후 asyncCall에는 calling을 콘솔창에 출력한 뒤, 2초 후 resolved를 출력합니다. 여기서 async, await 키워드가 사용되는 방법을 익혀두세요! **async는 함수 이름 부분의 제일 앞**에, await는 **결과를 기다릴 함수 호출 부분 앞**에 작성합니다.

async는 해당 함수에서 비동기 처리를 위한 Promise 동작을 한다는 것을 명시하는 것이고, await는 호출되는 함수가 적절한 결과를 반환할 때까지 기다리도록 동작합니다. **실질적인 동작은 await이고, await을 사용하기 위해 async를 명시**해야 한다고 이해하시면 됩니다!

### async / await 실습

앞선 실습에서 Axios와 콜백 함수로 작성했던 코드를 기억하시나요?

해당 코드를 async와 await를 이용해 비동기 처리가 될 수 있도록 수정해봅시다.

1. componentDidMount() 메소드 앞에 async를 붙이세요.
2. axios.get()을 한 결과를 response 변수에 저장하세요. 단, 비동기 처리가 될 수 있도록 await를 붙여주세요.
3. setState를 이용해 response.data를 users에 저장하세요.
```
import React from 'react';
import axios from 'axios';

class Users extends React.Component {
    constructor() {
        super();
        this.state = { users: [] };
    }
    // async를 추가하세요.
    async componentDidMount() {
        // axios.get()으로 GET 요청을 하세요. 단, await를 이용해 비동기 처리가 될 수 있도록 하세요.
        const response = await axios.get('https://jsonplaceholder.typicode.com/users');
        // setState를 이용해 데이터를 users에 저장하세요.
        this.setState({
            users : response.data
        })
    }

    render() {
        const userName = this.state.users.map(
            (user) => (<li key={user.id}> {user.name} </li>)
        );
        
        return (
            <>
                <h4>사용자 리스트</h4>
                <div> {userName} </div>
            </>
        );
    }

}

export default Users;
```

### Hook으로 API 다루기 실습

지금까지는 클래스형 컴포넌트에서 State를 이용해서 API를 사용했습니다. 이번에는 useState와 useEffect를 이용해 API를 다루는 방법을 실습해보겠습니다.

함수형 컴포넌트에서 기존 클래스의 state를 useState로 관리하고, componentDidMount()에서 작성했던 코드를 useEffect에서 작성하면 됩니다.

단, useEffect는 반드시 함수를 반환해야 하는데 async는 Promise 객체를 리턴하기 때문에 사용할 수 없습니다. 이를 해결하기 위해서는 useEffect에서 새로운 async 함수를 만들고 useEffect에서는 새로 만든 함수를 반환하도록 하면 됩니다.

아래를 참고하여 지시사항에 따라 코드를 작성해보세요!
```
useEffect(() => {
    async function fetch() {
        const response = await axios.get( 요청할 url );
    };
    fetch();
}, []);
```

1. useState를 이용해 state인 users를 선언하세요. 초깃값은 []로 설정하세요.
2. async와 await를 이용한 useEffect에서 axios.get()을 한 결과를 users state에 저장하세요. 단, useEffect에 바로 async를 사용할 수 없음으로 새로운 async 함수를 만드세요.

```
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function Users() {
    // state인 users를 useState()로 선언하세요.
    var [users, setUsers] = useState([])
    
    // async와 await를 이용한 useEffect()를 선언하세요.
    useEffect(() => {
        async function fetch() {
            const response = await axios.get('https://jsonplaceholder.typicode.com/users');
            setUsers(response.data);
        };
        fetch();
    }, []);
    
    
    const userName = users.map(
        (user) => (<li key={user.id}> {user.name} </li>)
    );

    return (
        <>
            <h4>사용자 리스트</h4>
            <div> {userName} </div>
        </>
    );
}

export default Users;
```

### API 호출 에러 핸들링 실습

API 호출 도중 에러가 발생했을 때 핸들링하는 실습을 해보겠습니다. 예외 처리는 아래처럼 try ~ catch를 이용해서 하면 됩니다.
```
try {
    ···
} catch(e) {
    ···
}
```

오른쪽 코드에서 에러 내용을 저장할 state인 error가 선언되어 있습니다. GET 요청 시 예외가 발생하는 경우 발생한 에러 내용인 e를 error state에 저장해봅시다.

만약 에러가 발생해 e에 값이 들어가게 되면 에러 발생! 이라는 문구가 출력됩니다. 일부러 잘못된 API 주소를 넣어 테스트해 봅시다!

1. try ~ catch를 이용해 예외 처리를 하세요. try에서는 GET 요청을 하고 예외 발생 시 error state에 에러 내용을 저장하세요.

```
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function Users() {
    const [users, setUsers] = useState([]);
    const [error, setError] = useState(null);
    
    useEffect(() => {
        async function fetchUser() {
            // try ~ catch를 이용해 예외 처리를 하세요.
            try {
                const response = await axios.get(
                    'https://jsonplaceholder.typicode.com/error' // 에러 발생 API 주소
                    // 'https://jsonplaceholder.typicode.com/users' // 정상 API 주소
                );
                setUsers(response.data);
            } 
            catch(e) {
                setError("에러 발생!")
            }
        };
        fetchUser();
    }, []);
    
    const userName = users.map(
        (user) => (<li key={user.id}> {user.name} </li>)
    );

    if (error) return <h4>에러 발생!</h4>;
    return (
        <>
            <h4>사용자 리스트</h4>
            <div> {userName} </div>
        </>
    );
}

export default Users;
```

