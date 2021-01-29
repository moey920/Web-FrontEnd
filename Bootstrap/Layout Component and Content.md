# 레이아웃 컴포넌트 및 컨텐츠

부트스트랩 컴포넌트, 객체 및 컨텐츠 활용 방법에 대해 배우고 적용할 수 있습니다.

## Bootstrap의 Card

### Card 개념

카드는 부트스트랩이 지원하는 유연하고 확장 가능한 콘텐츠 컨테이너입니다. 

여기에는 머리글 및 바닥 글 옵션, 다양한 콘텐츠, 상황 별 배경색 및 강력한 표시 옵션이 포함됩니다.

#### 지시사항

1. App.js 파일 내 App 클래스 내 card를 만드는 코드를 아래처럼 추가하세요.
```
 <div class="card">
  <img class="card-img-top" src='rabbit04.png' alt="elice"/>

  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="/" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

#### 해답 코드 (App.js, App.css)
```
// App.js
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';

class App extends React.Component {
render() {
    return (
        <div className="App">
        <h1 className="title">Hello, React!</h1>
            <div class="card"> {/* 카드 콘텐츠 컨테이너 */}
                <img class="card-img-top" src='20140409_225552.jpg' alt="bori"/>

                <div class="card-body">
                    <h5 class="card-title">카드 제목입니다.</h5>
                    <p class="card-text">카드의 텍스트를 입력하는 부분입니다.</p>
                    <a href="/" class="btn btn-primary">버튼입니다.</a>
                </div>
            </div>
        </div>
    );
}
}
export default App;
```

```
// App.css
.App {
  text-align: center;
}

.App-logo {
  height: 40vmin;
  pointer-events: none;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

.App-link {
  color: #61dafb;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.title {
    font-style: italic;
}


.card {
width: 18rem;
}


.card-img-top{
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 5px;
  width:210px;
  height:300px;
    background-image: url('20140409_225552.jpg');
}
```
![image-4.png](./image-4.png)

## bootstrap의 Form

### Form 개념

Bootstrap의 Form은 브라우저와 모바일에서 보다 일관된 렌더링을 위해 맞춤형 디스플레이를 선택할 수 있습니다.

이메일 확인, 번호 선택 등과 같은 새로운 입력 컨트롤을 활용하려면 모든 입력에 적절한 유형 속성 (예 : 이메일 주소의 이메일 또는 숫자 정보의 번호)을 사용해야합니다.

다음은 Bootstrap의 form 양식 스타일을 보여주는 간단한 예입니다.
```
<form>
<h1>로그인</h1>
<p>이름을 입력하세요:</p>
<input
type="text"
/>
</form>
```

#### 지시사항

##### Form 띄우기
1. App.js 파일 내 App 클래스 내 이름 입력하는 form을 만드는 코드를 아래처럼 추가하세요.
```
<form>
<h1>로그인</h1>
<p>이름을 입력하세요:</p>
<input
type="text"
/>
</form>
```

2. 그 밑에 회원가입 form을 넣으세요 (수정필요: 결과 예시 이미지를 참고하세요)

#### 실습 코드
```
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';

class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>
        <form>
            <h1>로그인</h1>
            <p>이름을 입력하세요:</p>
            <input
            type="text"
            />
        </form>
        <form>
            <h2>Email</h2><input type="email" />
            <h2>비밀번호</h2><input type="password" />
        </form>
    </div>
  );
}
}

export default App;
```
![image-5.png](./image-5.png)

## bootstrap의 List-group과 테이블

### List 개념

기본 목록 그룹을 만들려면 .list-group 클래스가있는 ul 와 .list-group-item 클래스가있는 li 를 사용합니다. 

> 간단히 말해 리스트 아이템인 li 태그 그룹을 ul 태그로 묶는 것입니다.

### Table 개념

Bootstrap 4 테이블은 게시판 글 목록이나 차트를 표현할때 유용합니다. .table 클래스는 테이블에 기본 스타일을 추가합니다.

#### 지시사항

##### List group 띄우기

1/ App.js 파일 내 App 클래스 내 ```<div className="App">``` 내에 list group의 기본적인 형태를 만드는 코드를 입력하세요.
```
   <div class="list-group">
  <a href="/" class="list-group-item list-group-item-action active">
    Cras justo odio
  </a>
  <a  class="list-group-item list-group-item-action">Dapibus ac facilisis in</a>
```
2. ```<a class="list-group-item list-group-item-action"></a>``` 태그에 링크를 이렇게 걸어보세요
```
<a  href="www.elice.com" class="list-group-item list-group-item-action">
```

##### table 띄우기

1. 다음 형식을 활용해서 글 목록 테이블을 만들어 보세요.
```
 <table class="table table-hover">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">제목</th>
      <th scope="col">작성자</th>
      <th scope="col">날짜</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>  
      <td>공지글</td>
      <td>Mark </td>
      <td>20.12.23</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td>뮤직 리뷰</td>
      <td>Thom Yorke</td>
      <td>20.11.23</td>
    </tr>
    <tr>
      <th scope="row">3</th>
      <td colspan="2">평론가 리뷰</td>
      <td>21.1.10</td>
    </tr>
  </tbody>
</table>
```

#### 실습 코드
```
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';

class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>
        
        <div class = "padd">list를 만드세요 </div>
            <div class="list-group">
                <a href="/" class="list-group-item list-group-item-action active">
                    Cras justo odio
                </a>
                <a href="www.elice.com" class="list-group-item list-group-item-action">Dapibus ac facilisis in</a>
            </div>

        <div class = "padd">테이블을 입력하세요 </div>
         <table class="table table-hover">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">제목</th>
                    <th scope="col">작성자</th>
                    <th scope="col">날짜</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <th scope="row">1</th>
                        <td>공지글</td>
                        <td>Mark </td>
                        <td>20.12.23</td>
                </tr>
                <tr>
                    <th scope="row">2</th>
                        <td>뮤직 리뷰</td>
                        <td>Thom Yorke</td>
                        <td>20.11.23</td>
                </tr>
                <tr>
                    <th scope="row">3</th>
                        <td colspan="2">평론가 리뷰</td>
                        <td>노하람</td>
                        <td>21.01.10</td>
                </tr>
            </tbody>
        </table>
    </div>
  );
}
}

export default App;
```
![image-6.png](./image-6.png)

## bootstrap의 Typography 활용

### Typography 개념

부트스트랩은 기본 전 타이포그래피 및 문단조절을 설정합니다. 

타이포그래피의 많은 설정으로 alignment, heading, font 크기 등을 맞춤화 할 수 있습니다. 

더 많은 스타일이 필요한 경우 bootstrap의 텍스트 유틸리티 클래스 documentation을 확인하십시오.

#### 지시사항

1. App.js 파일 내 App 클래스 내 ```<div className="App">``` 내에 흐려지는 텍스트를 완성하는 코드를 입력하세요.
```
<h3>
  Fancy display heading
  <small class="text-muted">With faded secondary text</small>
</h3>
```

2. 디스플레이 헤딩을 사용해보세요

3. html 텍스트 효과 다양하게 활용해보세요

4. blockquote로 text alignment(텍스트 위치)를 다르게 해보세요.

#### 실습 코드
```
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';

class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>

        <h3>
            <p>흐린 텍스트 처리</p>
            Fancy display heading
            <small class="text-muted">With faded secondary text</small>
        </h3>

        <p>디스플레이 헤딩 예시</p>
        <h1 class="display-1">Display 1</h1>
        <h1 class="display-2">Display 2</h1>
        <h1 class="display-3">Display 3</h1>
        <h1 class="display-4">Display 4</h1>
        <h1 class="display-5">Display 5</h1>
        <h1 class="display-6">Display 6</h1>

        <p>html 텍스트 효과</p>
        <p> 마크 태그를 사용하여 텍스트를<mark> 강조 표시 </ mark> 할 수 있습니다.</p>
        <p><del>이 문장은 삭제된 텍스트로 취급됩니다.</del></p>
        <p><s>이 문장은 더 이상 정확하지 않은 것으로 간주됩니다. </s></p>
        <p> <ins>이 문장은 문서에 추가된 것으로 취급됩니다. </ ins></ p>
        <p><u>이 줄 밑줄로 표시됩니다. </u></p>
        <p><small>이  문장은 작은 글씨로 처리됩니다. </small></p>
        <p><strong>이 줄은 bold 텍스트로 렌더링되었습니다. </strong></p>
        <p><em>이 줄은 italic 텍스트로 렌더링되었습니다. </em></p>

        <p>텍스트 정렬</p>
        <blockquote class="blockquote text-center">
            <p class="mb-0">중앙정렬.</p>
            <footer class="blockquote-footer">footer <cite title="Source Title">Source Title</cite></footer>
        </blockquote>
        <blockquote class="blockquote text-left">
            <p class="mb-0">왼쪽정렬.</p>
            <footer class="blockquote-footer">footer in <cite title="Source Title">Source Title</cite></footer>
        </blockquote>
    </div>
   
 
  );
}
}

export default App;
```

![image-7.png](./image-7.png)

## bootstrap의 Border

### Display 유틸리티

부트스트랩의 디스플레이 유틸리티를 사용하여 컴포넌트가 보여지는 속성 등을 빠르고 신속하게 전환할 수 있습니다.

*여기서 디스플레이 유틸리티란 부트스트랩에서 제공하는 비교적 작은 범주의 컴포넌트라고 이해하면 됩니다.

반응형 디스플레이 클래스를 사용하여 표시 할 수 있는 모든 컴포넌트의 일부만 의도적으로 보여줄 수 있습니다. 필요에 따라 다양한 효과를 위해 클래스를 결합 할 수 있습니다.

### Border

Border를 사용하여 컴포넌트의 테두리, 반경, 스타일등을 빠르게 지정할 수 있습니다. 이미지, 버튼, 텍스트 또는 기타 요소에 적합합니다.

#### 지시사항

1. App.js 파일 내 App 클래스 내 ```<div className="App">``` 내에 d-inline으로 컴포넌트를 가로로 배치하는 코드를 입력하세요.
2. Display 속성(d-block)으로 컴포넌트(텍스트)를 세로로 배치하세요.
3. 다음 코드로 테두리(Border) 색 설정하세요.
4. 테두리(Radius) 반경을 설정하세요.

#### 실습 코드
```
import React from 'react';
import './App.css';
import { Component} from 'react';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';

class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>
        
        <div class ="padd">/**Component Display 가로*/</div>
        <div class="d-inline p-2 bg-primary text-white">a-inline</div>
        <div class="d-inline p-2 bg-dark text-white">b-inline</div>
        <span class="d-inline p-2 bg-primary text-white">a-inline</span>
        <span class="d-inline p-2 bg-dark text-white">b-inline</span>

        <div class ="padd">/**Component Display 세로*/</div>
        <div class="d-block p-2 bg-primary text-white">a-block</div>
        <div class="d-block p-2 bg-dark text-white">b-block</div>
        <span class="d-block p-2 bg-primary text-white">a-block</span>
        <span class="d-block p-2 bg-dark text-white">b-block</span>
        
        <div class ="padd">/**Border 색 정하기*/</div>
        <span class="border border-primary"></span>
        <span class="border border-secondary"></span>
        <span class="border border-success"></span>
        <span class="border border-danger"></span>
        <span class="border border-warning"></span>
        <span class="border border-info"></span>
        <span class="border border-light"></span>
        <span class="border border-dark"></span>
        <span class="border border-white"></span>

        <div class ="padd">/**Border radius 정하기*/</div> 
        <img src="..." class="rounded" alt="..."/>
        <img src="..." class="rounded-top" alt="..."/>
        <img src="..." class="rounded-right" alt="..."/>
        <img src="..." class="rounded-bottom" alt="..."/>
        <img src="..." class="rounded-left" alt="..."/>
        <img src="..." class="rounded-circle" alt="..."/>
        <img src="..." class="rounded-pill" alt="..."/>
        <img src="..." class="rounded-0" alt="..."/>
    </div>
  );
}
}

export default App;
```

## bootstrap의 stretched-link

stretched-link는 CSS를 통해 중첩된 부분을 확장하여 HTML 요소 또는 부트 스트랩 구성 요소를 클릭 할 수 있도록합니다.

예를들어 실습1에서 만들었던 카드를 가로로 늘리거나 줄일 수 있습니다.

카드는 부트 스트랩에서 기본적으로 위치 : 상대적이므로이 경우 다른 HTML 변경없이 카드의 링크에 .stretched-link 클래스를 안전하게 추가 할 수 있습니다.

#### 지시사항
1. App.js 파일 내 App 클래스 내 ```<div className="App">``` 내에 이미 만들어진 카드 아래 stretched-link를 사용하는 코드를 입력하세요.

#### 실습 코드
```
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';



class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>   
        <div class="card">
            <img class="card-img-top" src='20140409_230641.jpg' alt="elice"/>
            
            <div class="card-body">
                <h5 class="card-title">Card title</h5>
                <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
                <a href="/" class="btn btn-primary">Go somewhere</a>

                <div class="card2">
                    <div class="row no-gutters position-relative">
                        <img class="card-img-bot" src="20140409_230641.jpg" alt="elice"/>
                        <div class="col-md-6 position-static p-4 pl-md-0">
                            <h5 class="mt-0">Columns with stretched link</h5>
                            <p>(컨텐츠 내용) another instance of placeholder content for this other custom component. It is intended to mimic what some real-world content would look like, and we're using it here to give the component a bit of body and size.</p>
                            <a href="#" class="stretched-link">Go somewhere</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  );
}
}

export default App;
```

## bootstrap의 Spinner

부트스트랩 Spinner 를 사용하여 프로젝트/웹페이지의 로딩 상태를 표시 할 수 있습니다. 

Spinner는 사용자에게 편리한 UI를 만들기 위해 프론트엔드에 필수적으로 적용되는 컴포넌트입니다. 

HTML 및 CSS로만 제작되므로 자바 스크립트가 필요하지 않습니다. 그러나 가시성을 전환하려면 사용자 정의 JavaScript가 필요합니다. 

뛰어난 유틸리티 클래스를 사용하여 모양, 정렬 및 크기를 쉽게 사용자 지정할 수 있습니다.

#### 지시사항
- App.js 파일 내 App 클래스 내 ```<div className="App">``` 내에 Spinner 만드는 코드를 입력하세요.
1. Spinner 만들기

#### 실습 코드
```
import React from 'react';
import './App.css';
import './bootstrap.min.css';
import './bootstrap-grid.css';
import './bootstrap-grid.min.css';



class App extends React.Component {
render() {
  return (
    <div className="App">
        <h1 className="title">Hello, React!</h1>
   
<div class="padd">Spinner를 만드세요</div>
    <div class="spinner-border" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-secondary" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-success" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-danger" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-warning" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-info" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-light" role="status">
        <span class="sr-only">Loading...</span>
    </div>
    <div class="spinner-border text-dark" role="status">
        <span class="sr-only">Loading...</span>
    </div>


<div class="padd">로딩 버튼을 만드세요</div>
    <button class="btn btn-primary" type="button" disabled>
        <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
        <span class="sr-only">Loading...</span>
    </button>
    <button class="btn btn-primary" type="button" disabled>
        <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
    Loading...
    </button>


    </div>
  
   
 

  );
}
}

export default App;
```
