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



