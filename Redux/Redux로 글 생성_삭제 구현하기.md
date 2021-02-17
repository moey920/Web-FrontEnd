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

스토어를 생성한 뒤 리듀서를 작성하세요.
스토어를 처음 생성하게 되면 바로 초기 액션과는 상관없이 호출되는데 그때 state(상태) 값은 undefined입니다.
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
3. action을 dispatch를 통해서 전달해서 UI 업데이트

State값이 바뀔 때 subscribe를 하고 있는 함수들을 호출하는 것을 통해서 UI가 업데이트됩니다.
글 목록을 클릭했을 때 액션을 만들고 액션 타입이 ‘SELECT’ 일 때, state.contents[i].id 라는 state값과 액션을 리턴해야 합니다.
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
여기서 state값을 리턴할때는 다음과 같이 반드시 복제된 state을 리턴해야 합니다.
newState = Object.assign({}, state, {
    mode:action.mode
});
4. subscribe를 통해서 자동 갱신 되도록 처리

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
