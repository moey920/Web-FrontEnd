# CRUD 개념

CRUD 라는 개념을 처음 접해보신 분들도 있지만 이전에 flask 웹 프로그래밍(05장 REST API)에서 다뤘었습니다.

CRUD는 Create, Read, Update, Delete의 제일 앞 문자를 하나씩 따와 만든 줄임말입니다. 데이터를 처리하는 시스템이 지속성을 갖기 위해 갖춰야 하는 기본적인 데이터 처리 4가지 기능입니다. 따라서, 시스템에서 데이터를 Create, Read, Update, Delete를 할 수 없다면 정상적으로 작동하는 시스템이 아니라는 것입니다.

게시판 혹은 블로그가 가장 대표적인 CRUD 구현의 예라고 할 수 있습니다. 만약에 게시판의 모든 게시글의 컴포넌트들은 각자의 기능에 맞추어 이 함수만 호출하도록 작성한다면 아주 효율적이고 깔끔한 프론트엔드 개발을 할 수 있습니다. 그리고 이러한 기능을 제공하는 것이 리덕스가 되겠습니다.

이 장 실습에서 HTML, CSS 컴포넌트를 클릭할 때마다 본문이 자동갱신되는 애플리케이션을 만들어보겠습니다.

# 리덕스로 애플리케이션 상태 관리하기

실습 이전에 리덕스1 에서 배웠던 리덕스 핵심 개념에 대해 간단하게 복습해봅시다.

- 리덕스 특징
리덕스는 모든 상태 데이터를 한 객체에 모으게 함으로써 애플리케이션에서 상태를 보는 관점을 단순하게 유지해줍니다.

- 스토어
리덕스에서 스토어는 애플리케이션의 상태 데이터를 저장하고 모든 상태 갱신을 처리합니다. 앞에서 만든 여러 리듀서를 조합하고 합성해서 스토어가 단일 리듀서를 만들 수 있습니다.

- 액션
액션은 애플리케이션 상태 중에서 어떤 부분을 바꿀지 지시하고 그런 변경에 필요한 데이터를 제공합니다.

- 리듀서 정의
리듀서는 현재 상태와 액션을 인자로 받아 새로운 상태를 만들어 반환하는 함수입니다.
리듀서는 액션이 호출될 때 이전의 state(상태)값과 호출된 이후인 액션값을 입력으로 받습니다.

- state(상태값) 변경하기
1. state를 바꾸기 위해서는 action을 만들어야 합니다.
2. action을 dispatch에게 제출하면 dispatch가 reducer를 호출합니다. 이때 이전의 state 값과 action의 값을 동시에 줍니다.
3. reducer 함수가 그것을 분석해서 state에 최종적인 값을 return 해줍니다.

- 리덕스 컴포넌트 부품화
리덕스를 순수 html/css/javascript로 구현할 때는 반드시 컴포넌트를 부품화 해야 합니다.

# 클라이언트 언어(HTML, CSS, javascript) 에 리덕스 적용하기

리덕스를 클리이언트 언어에 적용하기 위해 밟아야 하는 순서는 이렇습니다.

1. 각각의 기능에 대해 모듈화

순수 html의 컴포넌트들을 부품화 시켜서 자바스크립트로 구현하기 쉽게 설정합니다.

2. store 생성, reducer생성과 state 사용하기

- 스토어를 생성한 뒤 리듀서를 작성하세요.
- 스토어를 처음 생성하게 되면 바로 초기 액션과는 상관없이 호출되는데 그때 state(상태) 값은 undefined입니다.
```
function reducer(state, action){
    if(state === undefined){
        return {
            contents:[
                {id:1,title:'제목1',desc:'내용..'},
                {id:2,title:'제목2', desc:'내용..'}
            ]
        }
    }
}
var store = Redux.createStore(reducer);
subject();
```

3. action을 dispatch를 통해서 전달해서 UI 업데이트

- State값이 바뀔 때 subscribe를 하고 있는 함수들을 호출하는 것을 통해서 UI가 업데이트됩니다.
- 글 목록을 클릭했을 때 액션을 만들고 액션 타입이 ‘SELECT’ 일 때, state.contents[i].id 라는 state값과 액션을 리턴해야 합니다.
```
while(i<state.contents.length){
liTags = liTags + `
    <li>
        <a onclick="
            event.preventDefault();
            var action = {type:'SELECT', id:${state.contents[i].id}}
            store.dispatch(action);
            " href="${state.contents[i].id}">
            ${state.contents[i].title}
        </a>
    </li>`;
i = i + 1;
}
```
- 여기서 state값을 리턴할때는 다음과 같이 반드시 복제된 state을 리턴해야 합니다.
```
newState = Object.assign({}, state, {
    mode:action.mode
});
```

4. subscribe를 통해서 자동 갱신 되도록 처리
```
function description(){
    var state = store.getState();
    if(state.mode === 'create'){
        document.querySelector('#content').innerHTML = `
        <article>

        </article>
     `
}
function reducer(state, action){
    if(state === undefined){
        return {
            max_id:2,
            mode:'create',
            selcted_id:2,
            contents:[
                {id:1,title:'제목1',desc:'제목1의 내용..'},
                {id:2,title:'제목2', desc:'제목2의 내용..'}
            ]
        }
    }
var store = Redux.createStore(reducer);
store.subscribe(description); // 다음과 같이 subscribe를 통해서 description 함수가 자동 갱신 되도록 처리
```

### 부품화 된 리액트 컴포넌트에 스토어 생성하기 실습

다음 index.js 에 작성된 코드는 아주 간단하게 redux를 사용하여 글생성과 글삭제를 구현하기 위해 html의 모든 컴포넌트들을 부품화 시킨 코드입니다.
```
subject();
TOC();
control();
article();
```

컴포넌트 부품화를 끝낸 index.html의 function들의 이름만 봐도 어떤 컴포넌트와 관련된 것인지 한눈에 알 수가 있습니다. 이제 리덕스를 적용하여 컴포넌트에 기능을 연결해 봅시다.

- 앞으로 이 실습들은 계속 inspect<console 창을 열어서 state값을 확인하시면 리덕스의 상태 관리를 이해하기 쉬워집니다.

1. index.html파일 내 <script> 내 맨 아래 코드 위에 바로 리듀서를 생성한 다음 그 리듀서를 받는 스토어를 생성하세요.
```
subject();
TOC(); //입력된 개체를 화면에 표시
control();
article();
```

- 먼저 function reducer를 작성한 다음 state가 undefined일 경우, 다음과 같은 내용을 content 내에 반환하세요.
```
contents:[
{id:1,title:'Redux',desc:'Redux is ..'},
{id:2,title:'React-Redux', desc:'React-Redux is ..'}
]
```

2. GUI창 확장<마우스 우클릭<inspect<console 에 store.getState()에서 초기값이 무엇인지 확인하세요.

```
function reducer(state, action) {
    if(state === undefined){
        return {
            contents : [
                {id:1, title:'Redux', desc:'Redux is ..'},
                {id:2, title:'React-Redux', desc: 'React-Redux is ..'}
            ]
        }
    }
}

var store = Redux.createStore(reducer);
```

### 부품화된 리액트 컴포넌트에 state사용 실습

이제 글 목록 타이틀을 state를 사용하여 반환하는 모듈을 만들어보겠습니다.

TOC 라는 function 내에 <li>태그로 둘러쌓인 글목록이 있습니다.

1. function TOC() 내 <li>태그 내 글목록 번호와 타이틀을 스토어에 있는 정보를 바탕으로 가져오는 state를 가져오세요.
ex) 타이틀:
```
( {state.contents[i].title]} )
```
이런식으로 state에 따라서 변하는 웹페이지를 생성할수 있게 만들수 있습니다.

```
function TOC(){
  var state = store.getState();
 
    var i = 0;
    var liTags = '';
    while(i<state.contents.length){
    //  1. <li> </li> 내에 글목록을 스토어에 있는 정보를 바탕으로 가져오는 state를 가져오세요.
        liTags = liTags + `
            <li>
              <a href="${state.contents[i].id}">${state.contents[i].title}</a>
            </li>`;
        i = i + 1;
    }
    document.querySelector('#toc').innerHTML = `
    <nav>
        <ol>${liTags}</ol>
    </nav>
    `;
}
```

### 리덕스 적용하여 글목록 수정하기 실습

바로 이전 [실습2] 까지는 state에 따라서 만들어지는 웹페이지를 생성할 수 있었다면 이번 실습부터 우리가 해야 되는것은 글 목록을 클릭했을때 그것에 해당하는 본문이 나올수 있게 해야 하는 것입니다.

store의 state값을 변경하기위해서 action을 발생시키고 그 action이 dispatch를 통해서 리듀서를 실행시키면 리듀서가 state의 새로운 값을 나타냅니다.

그리고 state값이 바뀌면 subscribe하고 있는 그 함수들을 호출한 뒤 UI가 변경됩니다.

TOC 라는 function 내에 <li>태그로 둘러쌓인 글목록이 있습니다.

function TOC() 객체를 onclick을 하게 됐을 때 store.dispatch에 액션 정보를 줍니다.

1. event.preventDefautlt(); 밑에 액션 타입이 ‘SELECT’인 경우에 이런식으로 액션을 디스패치하세요.
```
var action = {
    type:'SELECT', 
    id:${state.contents[i].id}
}
store.dispatch(action);
```

2. ```" href="${/*...*/ }"``` 내에 해당 UI의 제목과 아이디를 업데이트 하세요.

아이디 업데이트 예시:
state.contents[i].id

제목 업데이트 예시:
state.contents[i].title

```
function TOC(){
    var state = store.getState();
    var i = 0;
    var liTags = '';
    while(i<state.contents.length){
        liTags = liTags + `
        <li>
            <a onclick="
                event.preventDefault();
                var action = {type:'SELECT', id:${state.contents[i].id}}
                store.dispatch(action);
            " href="${state.contents[i].id}">
                ${state.contents[i].title}
            </a>
        </li>`;
        i = i + 1;
    }
    document.querySelector('#toc').innerHTML = `
    <nav>
        <ol>${liTags}</ ol>
    </nav>
    `;
}
```

### 리덕스를 적용한 글생성(create) 실습

리듀서에 모드(mode)라는 객체를 줘서 mode가 만약 ‘create’일 경우 와 ‘delete’일 경우 다르게 작동하도록 구현해보겠습니다.

form에 제목(title)과 내용(description)을 입력하고 submit버튼을 눌렀을 때 title이라는 변수에 입력값을 저장해줍니다.

#### Index.html 전체적인 구조 설명

- function control() 이라는 함수 내 create 버튼이 글을 생성할 겁니다.

1. function article() 내 onsubmit 버튼이 눌릴 때, title 태그에 입력한 데이터를 불러들이는 코드를 작성하세요. 이 때 title과 description을 변수에 저장하세요.
```
<form onsubmit="
event.preventDefault();
/*이곳에 코드를 입력하세요*/
})
```

- title = this.title.value()는 title 태그내의 값을 저장합니다.

2. 1번에서 저장한 변수 두개를 스토어에 dispatch 하세요.
```
<form onsubmit="
event.preventDefault();
/* title과 desc 태그 내의 데이터를 저장한 후에 코드를 입력하세요*/
})
```

ex) 다음과 같은 데이터를 스토어에 디스패치합니다.

- var title과 _desc에 저장된 내용
```
type: 'CREATE',
title:_title,
desc:_desc
```
이 디스패치가 실행될 때 리듀서가 호출되어 액션값이 리듀서의 else if(action.type === 'CREATE') 에 들어갑니다.

```
function article(){
    var state = store.getState();
    if(state.mode === 'create'){
        document.querySelector('#content').innerHTML = `
        <article>
            <form onsubmit="
                event.preventDefault();
                var _title = this.title.value;
                var _desc = this.desc.value;
                store.dispatch({
                    type:'CREATE',
                    title:_title,
                    desc:_desc
                })
            ">
                <p>
                    <input type="text" name="title" placeholder="title">
                </p>
                <p>
                    <textarea name="desc" placeholder="description"></textarea>
                </p>
                <p>
                    <input type="submit">
                </p>
            </form>
        </article>
        `
    } else if(state.mode === 'read'){
        var i = 0;
        var aTitle, aDesc;
        while(i < state.contents.length){
            if(state.contents[i].id === state.selcted_id) {
                aTitle = state.contents[i].title;
                aDesc = state.contents[i].desc;
                break;
            }
            i = i + 1;
        }
        document.querySelector('#content').innerHTML = `
        <article>
            <h2>${aTitle}</h2>
            ${aDesc}
        </article>
        `
    }
}
```

### 리덕스를 적용한 글생성(create) 실습

리듀서에 모드(mode)라는 객체를 줘서 mode가 만약 ‘create’일 경우 와 ‘delete’일 경우 다르게 작동하도록 구현해보겠습니다.

form에 제목(title)과 내용(description)을 입력하고 submit버턴을 눌렀을 때 title이라는 변수에 입력값을 저장해줍니다.

1. index.html 내 function reducer(state, action) 내

액션 타입(action.type)이 ‘CREATE’ 일 경우 newContents에 새로운 컨텐츠(입력받은 title과 description)를 다음과 같이 push 하세요.
```
newContents.push({id:newMaxId, .. });
```

- newContents에 타이틀과 내용(description)도 push 해야 합니다.

```
function reducer(state, action){
    if(state === undefined){
        return {
            max_id:2,
            mode:'create',
            selcted_id:2,
            contents:[
                {id:1,title:'HTML',desc:'HTML is ..'},
                {id:2,title:'CSS', desc:'CSS is ..'}
            ]
        }
    }
    var newState;
    if(action.type === 'SELECT'){
        newState = Object.assign({}, state, {selcted_id:action.id});
        
        
    } else if(action.type === 'CREATE'){
        var newMaxId = state.max_id + 1;
        var newContents = state.contents.concat();
        /*1.이곳에 새로운 컨텐츠(입력받은 title과 description)를 push 하세요 */
        newContents.push({id:newMaxId, title:action.title, desc:action.desc});
        newState = Object.assign({}, state, {
            max_id:newMaxId,
            contents:newContents,
            mode:'read'
        })
    }
    console.log(action, state, newState);
    return newState;
}
```

### 리덕스를 적용한 글 삭제(delete) 실습

이제 마지막 단계인 글 삭제를 구현해봅시다.

복잡한 코드로 충분히 헷갈릴 수 잇기때문에 코드 142줄 부터 어떻게 작동하는지 설명해드리겠습니다.

배열을 생성해서 newContents라고 부르겠습니다.
```
var newContents = [];
```

만약에 선택된 아이디와 배열의 순차적인 컨텐츠의 아이디가 같지 않을 경우
새로운 컨텐츠로 push 할겁니다.
```
var i = 0;
while(i < state.contents.length){
    if(state.selcted_id !== state.contents[i].id){
        여기서 새로운 컨텐츠로 push 합니다
    );
    }
    i = i + 1;
}
```

삭제를 하게되면 mode가 welcome 이 됩니다. mode가 welcome이 될경우에는 state에 변화를 주었기 때문에 article에도 바뀝니다.
```
else if(action.type === 'CHANGE_MODE'){
newState = Object.assign({}, state, {
//모드 업데이트
});
```

1. function reducer()내 'DELETE' 조건문내에 만약 action이 ‘DELETE’인 경우는 현재 state의 값의 컨텐츠의 총 크기(state.contents.length) 와 this.state.selected_id와 삭제 하고싶은 목록의 아이디(state.contents[i].id ) 가 같다면 newContents를 push 하세요
```
else if(action.type === 'DELETE'){
var newContents = [];
var i = 0;
while(i < state.contents.length){
if(state.selcted_id !== state.contents[i].id){
/*이곳에 코드를 입력하세요 */
}
i = i + 1;
}
}
}
```

2. 만약에 액션 타입이 ‘DELETE’라면 다음과 같은 조건을 입력해서 컨텐츠가 삭제될경우 디폴트로 보여줄 객체 (‘welcome’)를 띄웁니다. 그러기 위해서는 mode를 welcome으로 바꾸세요.
```
newState = Object.assign({},state, {
contents:newContents,
/*이곳에 코드를 입력하세요 */
})
} else if(action.type === 'CHANGE_MODE'){
newState = Object.assign({}, state, {
});
}
```

#### 전체 코드
```
<!DOCTYPE html>
<html>
    <head>
        <script src="rdx.js"></script>
    </head>
    <body>
        <div id="subject"></div>
        <div id="toc"></div>
        <div id="control"></div>
        <div id="content"></div>    
        <script>
function subject(){
    document.querySelector('#subject').innerHTML = `
    <header>
        <h1>WEB</h1>
        Hello, WEB!
    </header>
    `
}
function TOC(){
    var state = store.getState();
    var i = 0;
    var liTags = '';
    while(i<state.contents.length){
        liTags = liTags + `
        <li>
            <a onclick="
                event.preventDefault();
                var action = {type:'SELECT', id:${state.contents[i].id}}
                store.dispatch(action);
            " href="${state.contents[i].id}">
                ${state.contents[i].title}
            </a>
        </li>`;
        i = i + 1;
    }
    document.querySelector('#toc').innerHTML = `
    <nav>
        <ol>${liTags}</ ol>
    </nav>
    `;
}
function control(){
    document.querySelector('#control').innerHTML = `
    <ul>
        <li><a onclick="
            event.preventDefault();
            store.dispatch({
                type:'CHANGE_MODE',
                mode:'create'
            })
        " href="/create">create</a></li>
        <li><input onclick="
            store.dispatch({
                type:'DELETE'
            });
        " type="button" value="delete"></li>
    </ul>
    `;
}
function article(){
    var state = store.getState();
    if(state.mode === 'create'){
        document.querySelector('#content').innerHTML = `
        <article>
            <form onsubmit="
                event.preventDefault();
                var _title = this.title.value;
                var _desc = this.desc.value;
                store.dispatch({
                    type:'CREATE',
                    title:_title,
                    desc:_desc
                })
            ">
                <p>
                    <input type="text" name="title" placeholder="title">
                </p>
                <p>
                    <textarea name="desc" placeholder="description"></textarea>
                </p>
                <p>
                    <input type="submit">
                </p>
            </form>
        </article>
        `
    } else if(state.mode === 'read'){
        var i = 0;
        var aTitle, aDesc;
        while(i < state.contents.length){
            if(state.contents[i].id === state.selcted_id) {
                aTitle = state.contents[i].title;
                aDesc = state.contents[i].desc;
                break;
            }
            i = i + 1;
        }
        document.querySelector('#content').innerHTML = `
        <article>
            <h2>${aTitle}</h2>
            ${aDesc}
        </article>
        `
    } else if(state.mode === 'welcome'){
        document.querySelector('#content').innerHTML = `
        <article>
            <h2>Welcome</h2>
            Hello, Redux!!!
        </article>
        `
    }
}
function reducer(state, action){
    if(state === undefined){
        return {
            max_id:2,
            mode:'welcome',
            selcted_id:2,
            contents:[
                {id:1,title:'HTML',desc:'HTML is ..'},
                {id:2,title:'CSS', desc:'CSS is ..'}
            ]
        }
    }
    var newState;
    if(action.type === 'SELECT'){
        newState = Object.assign(
            {}, 
            state, 
            {selcted_id:action.id, mode:'read'});
    } else if(action.type === 'CREATE'){
        var newMaxId = state.max_id + 1;
        var newContents = state.contents.concat();
        newContents.push({id:newMaxId, title:action.title, desc:action.desc});
        newState = Object.assign({}, state, {
            max_id:newMaxId,
            contents:newContents,
            mode:'read'
        })
    } else if(action.type === 'DELETE'){
        var newContents = [];
        var i = 0;
        while(i < state.contents.length){
            if(state.selcted_id !== state.contents[i].id){
                newContents.push(
                    state.contents[i]
                );
            }
            i = i + 1;
        }
        newState = Object.assign({},state, {
            contents:newContents,
            mode:'welcome'
        })
    } else if(action.type === 'CHANGE_MODE'){
        newState = Object.assign({}, state, {
            mode:action.mode
        });
    }
    console.log(action, state, newState);
    return newState;
}
var store = Redux.createStore(reducer);
store.subscribe(article);
store.subscribe(TOC);
subject();
TOC();
control();
article();
        </script>
    </body>
</html>
```
