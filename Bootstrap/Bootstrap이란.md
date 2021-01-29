# Bootstrap이란?

부트스트랩은 트위터에서 만든 프론트엔드 개발을 빠르고 쉽게 할 수 있는 프레임워크입니다.

> 프레임워크(framework): 재사용 가능한 요소의 집합과 툴, 확장 가능한 기반 코드

수많은 무료 및 전문 템플릿에서 제공하는 유용한 위젯, 차트로드, 4가지 대시 보드 변형, 애플리케이션 모음 등으로 웹개발하는데 바로 적용해볼 수 있습니다.

- 부트스트랩은 웹사이트를 쉽게 만들 수 있게 도와주는 HTML, CSS, JS 프레임워크이다. 하나의 CSS로 휴대폰, 태블릿, 데스크탑까지 다양한 기기에서 작동합니다. 다양한 기능을 제공하여 사용자가 쉽게 웹사이트를 제작, 유지, 보수할 수 있도록 도와줍니다.

- 개발자가 12개 이상의 사용자 지정 JQuery 플러그인을 활용할 수 있다.

## Bootstrap을 사용하는 이유

1. 웹 사이트를 개발할 때, **웹 사이트 디자인으로 인해 개발 시간이 길어지는 문제를 해결**하기 위해 만들어 졌습니다.
2.** 모바일 환경에 적합한 반응형 웹 사이트 개발**을 하기 위해 만들어 졌습니다.

프론트엔드 개발자는 디자이너와 협엽하거나 CSS나 SCSS를 공부해서 아주 세련되고 미적으로 훌륭한 웹사이트를 만들 수 있는데 왜 부트스트랩이 필요한걸까요? 

부트스트랩의 가장 큰 장점은 광범위한 브라우저 호환성을 유지하고 무엇보다 **일관된 디자인을 제공**한다는 점입니다. 

그렇기 때문에 사용하기가 매우 쉽고 초보자가 빠르게 완성도있는 프론트엔드 디자인을 할 수 있습니다.

웹 사이트를 구축할 때, 기능을 구현하는 시간보다 UI를 구현하는 시간이 더 많이 소요되는 경우가 많습니다. 

기능이 더 중요하지만, 사용자들에게 보이는 화면이 웹 사이트의 첫 인상을 좌우하기 때문입니다.

## Bootstrap 특징

위에서도 언급했지만, 부트스트랩의 가장 큰 장점은 내부의 클래스들만 알고 있다면 빠르고 쉽게 여러 형태의 웹 페이지를 제작할 수 있다는 점입니다. 

그리고 대부분은 각 해상도에 따른 처리가 되어있기 때문에 반응형 처리도 어렵지 않습니다. 또한, 퀄리티가 나쁘지 않아 많은 기업에서 사용하고 있습니다.

부트스트랩을 사용한 홈페이지 보기
VOGUE 홈페이지 → <http://www.vogue.co.kr/?international>

- 자바스크립트를 선택적으로 확장할수 있으며 github 오픈 소스로 사용이 가능하기 때문에 개인적으로 상업적으로 이용이 가능합니다.
- HTML과 CSS기본지식을 가진 누구나 쉽게 접근 가능합니다.
- 반응형 CSS를 포함한 단일코드로 모든 디바이스에 적용할수 있습니다.
- 그리드 시스템이 매우 훌륭해서 디자인을 바로 쓰기 좋습니다.
- 반응형 모바일이 가능한 웹사이트를 빠르게 디자인하고 맞춤 설정할 수 있습니다.
- 재사용 가능한 구성 요소를 사용하고 이해하기 편합니다.

Bootstrap 공식 사이트 바로가기 → <https://getbootstrap.com/>

# Yarn이란?

```yarn```은 페이스북에서 개발한 자바스크립트의 새로운 패키지 매니저입니다.

yarn에 대해서 자세히 알아보기에 앞서 먼저 ```npm```에 대해서 알아봅시다.

npm이란 ```Node Package Manager```, node.js로 만들어진 Package(Module)를 관리해주는 도구입니다.

npm2에서 npm3로 업데이트한 다음 npm2로 단 12초가 걸렸던 설치 시간이, npm3로는 50초의 상당히 긴 시간으로 증가했습니다. 

페이스북 개발자들이 이 상황을 보면서 해결 방법이 없는지 모색하기 시작한 결과 yarn이 탄생하게 되었습니다.

따라서 yarn은 npm 같은 패키지 매니저로 npm보다 빠르고 가벼우며 안정적입니다. 

이를 통해 전 세계의 다른 개발자와 코드(예 : JavaScript)를 사용하고 공유 할 수 있습니다.

> 패키지 매니저는 프로그램의 **의존성(dependencies)** 을 관리하는 도구입니다.

의존성을 관리한다는 것은 개발자가 제품 또는 응용 프로그램이 사용하고 의존하는 프로그램 집합을 지정, 제공, 설치, 업데이트 및 일반적인 관리를 한다는 뜻입니다.

## dependencies(종속성)가 왜 필요할까요?

많은 패키지들은 다른 패키지가 설치되어 있어야만 제대로 동작합니다.

이 경우에 기존 패키지를 제대로 동작시키기 위해 필요한 다른 패키지를 ‘dependency(의존성)’라고 말합니다.

따라서 패키지를 사용하고자 할 때 dependency에 해당되는 다른 패키지들을 전부 설치해줄 필요가 있습니다.

npm이나 yarn같은 패키지 매니저가 이 dependency를 관리합니다.

### 패키지 매니저가 공통적으로 수행하는 일

- 패키지의 dependency 관리
- 패키지의 보안관리 ㅡ 신뢰할 수 있고(authenticity), 손상되지 않음(integrity)을 보장
- 여러 패키지를 기능에 따라 그룹으로 묶어 정리
- 패키지 압축 해제
- Software repository로부터 패키지를 찾고, 다운로드하고, 설치하고, 업데이트하는 역할

다음은 개발자들이 말하는 npm과 yarn의 장점에 대한 통계입니다.
출처: <https://stackshare.io/stackups/npm-vs-yarn>


| npm의 장점 | yarn의 장점 |
|:---:|:---:|
| javascript의 최고의 패키지 관리 시스템 | 뛰어난 속도 |
| 오픈 소스 편리성 | 오픈 소스 편리성 |
| 큰 npm이용자 커뮤니티 | 사용하기 간편 |
| 수많은 패키지 포함 | 모든 npm패키지 설치 가능 |


# Package.json이란?

npm에서 핵심적인 역할을 하는 게 package.json입니다.

package.json 은 현재 프로젝트에 대한 정보와 의존성(dependencies)을 관리하는 문서입니다. 

패키지와 dependencies 버전에 관한 정보를 프로젝트의 루트 디렉토리에다가 저장하고 있습니다.

이미 작성된 package.json 문서는 어느 곳에서도 동일한 개발 환경을 구축할 수 있게 해줍니다. 

**JSON 포맷**으로 작성해야 하며, 다음과 같은 package.json 파일의 내용이 추가될 수 있습니다.

- name : 

URL이나 Command Line의 일부로 사용될 소문자로 표기된 214자 이내의 프로젝트(패키지) 이름으로, 간결하고 직관적인 이름으로 설정하되 다른 모듈과 동일한 이름을 피하세요.

Package.json의 name은 프로젝트 이름으로, 가장 중요합니다. 중앙 저장소에 배포할 때 version과 함께 필수 항목입니다. 

url로 사용되고, 설치할 때 디렉토리 이름이 되기 때문에 url이나 디렉터리에서 쓸 수 없는 이름을 사용하면 안 됩니다.

또한, 이름에 node나 js가 들어가면 안 됩니다. name은 214자보다 짧아야 하며, 점(.)이나 밑줄로 시작할 수 없습니다.

대문자를 포함해서는 안 되며, require() 함수의 인수로 사용되며 짧고 알기 쉬운 것으로 짓는 것이 좋습니다.

- version

SemVer(The semantic versioner for npm)로 분석 가능한 형태의 버전을 지정합니다.

- description

프로젝트(패키지)의 설명을 지정합니다.
(npm search 사용 시 도움이 됩니다.)

- keywords : 

프로젝트(패키지)의 키워드를 배열로 지정해서 프로젝트를 검색할 때 참조되는 키워드입니다.
description과 마찬가지로 npm search로 검색된 리스트에 표시됩니다.

- homepage : 

프로젝트 홈페이지 주소입니다.
url 항목과는 다르며, url을 설정하면 예상치 못한 움직임을 하게 되므로 주의합니다.

- author : 

프로젝트 작성자 정보로, 한 사람만을 지정합니다. JSON 형식으로 name, email, url 옵션을 포함합니다.

- contributors : 

프로젝트에 참여한 공헌자 정보로, 여러 사람을 배열로 지정할 수 있습니다.

- repository : 

프로젝트의 소스 코드를 저장한 저장소의 정보입니다.
소스 코드에 참여하고자 하는 사람들에게 도움이 될 수 있습니다. 프로젝트의 홈페이지 url을 명시해서는 안 됩니다.

- scripts : 

프로젝트에서 자주 실행해야 하는 명령어를 scripts로 작성해두면 npm 명령어로 실행 가능합니다.

- private : 

이 값을 true로 작성하면 중앙 저장소로 저장하지 않습니다.

- dependencies : 

프로젝트 의존성 관리를 위한 부분입니다. 현재의 패키지가 의존하고 있는 모듈들에 대한 리스트를 보여주며, 각자의 모듈의 이름과 버전 범위에 대해서 나타냅니다. 일반적으로 package.json에서 가장 많은 정보가 입력되는 곳입니다.

이 프로젝트가 어떤 확장 모듈을 요구하는지 정리할 수 있으며 버전 범위는 하나의 버전을 가르킬 수 도 있으며, range 범위 안에 포함될 수도 있습니다.

애플리케이션을 설치할 때 이 내용을 참조하여 필요한 확장 모듈을 자동으로 설치합니다. 예를들어 npm install 명령은 여기에 포함된 모든 확장 모듈들을 설치하게 되어 있습니다.

따라서 개발한 애플리케이션이 특정한 확장 모듈을 사용한다면 여기에 꼭 명시를 해주어야 합니다.

- devDependencies : 

패키지의 개발 시 사용될 의존성 모듈을 지정합니다.
(배포 시 포함되지 않습니다)

- engines : 

실행 가능한 노드 버전의 범위를 결정합니다.

## Bootstrap 파일 구조

npm이나 yarn으로 리액트 환경 안에서 react-bootstrap을 설치하면 다음과 같이 파일구조가 형성됩니다.

개발 환경은 비주얼 스튜디오 코드(visual studio code)입니다.

- my-app
    - node_modules : npm을 설치할 때 형성된 dir. 초기 작동 반응 앱에 필요한 모든 dependencies를 포함합니다.
    - package.json : 프로젝트와 관련된 다양한 메타 데이터 포함, 프로젝트에서 사용되는 dependencies를 지정하여 npm이 프로젝트의 다른 컴퓨터에서 동일한 환경을 설정하도록 도와준다.
    - ...
    - public
        - index.html : 앱을 시작하기 위해 시작 스크립트를 실행할 때 제공되는 템플릿 파일. 공용 폴더에 여러 html파일을 만들지 않는 것이 가장 좋다. 대신 이 파일을 사용하고 이 파일의 루트 div 컨테이너에 반응 구성 요소를 삽입한다. 다른 CSS 라이브러리 등이 파일에 정의될 수 있다.
        - ...
    - src
        - App.js : 이 파일에는 자체 루트 구성 요소를 대체할 수 있는 매우 기본적인 반응형 컴포넌트가 정의되어 있다.
        - index.js : 이 파일은 초기에 생성될 컴포넌트를 렌더링하고 서비스 워커를 등록한다.
        - ... : Contact.js, Form.js, Home.js, NoMatch.js 는 웹페이지를 작게 쪼개어 간편하게 rander하기 위해 만든 js파일

### npm 실행하기
react창을 열어보기 위해서는
1. cd my-app
2. npm start


# Bootstrap vs React-Bootstrap

react-bootstrap은 Jquery 기반의 Bootstrap 를 React 환경으로 이식한 프로젝트입니다. 

기존의 <div> 엘리먼트에 Class를 설정하여 컴포넌트를 구분하는 방식에서 

Bootstrap 컴포넌트별로 React 컴포넌트가 구현되어 더욱 리액트 환경에 맞는 개발이 가능합니다.

간단히 말해 react-bootstrap이 bootstrap에 비해 react에 더 최적화되어 빠르게 만들 수 있습니다.

또한, 이렇게 이해하셔도 됩니다.

- React: 웹사이트를 build하기 위해 사용되는 프레임워크
- Bootstrap: 웹의 반응형 UI를 만들기 위한 html/CSS 프레임워크
- React-bootstrap: 이 둘을 (따로 부트스트랩 설치 없이) 수행하기 위한 프레임워크

## React-Bootstrap 특징

- React-Bootstrap은 HTML 요소 정렬의 중복을 제거하고 대신 순수한 JavaScript를 사용하여 React가 페이지 렌더링을 완전히 인수하도록합니다.
- React Bootstrap은 Boostrap의 기능이 통합 된 React 프레임 워크이지만 표준 Boostrap 라이브러리 (특히 JQuery)에서 사용하는 모든 기본 구성 요소를 사용할 필요가 없습니다.
- React-Bootstrap은 React와 함께 진화하고 성장하여 UI 기반으로 탁월한 CSS Framework가 되었습니다.

간단한 드롭 다운 버튼을 만들때 Bootstrap과 React-Bootstrap의 차이를 알아보겠습니다.

1. Bootstrap:
```
<div class="btn-group"> 
 <button type="button" class="btn btn-default dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"> 
 Action <span class="caret"></span> 
 </button> 
 <ul class="dropdown-menu"> 
 <li><a href="#">Action</a></li> 
 <li><a href="#">Another action</a></li> 
 <li><a href="#">Something else here</a></li> 
 <li role="separator" class="divider"></li> 
 <li><a href="#">Separated link</a></li> 
 </ul> 
```
2. React-Bootstrap:
```
function renderDropdownButton(title, i) { 
 return ( 
 <DropdownButton bsStyle={title.toLowerCase()} title={title} key={i} id={`dropdown-basic-${i}`}> 
 <MenuItem eventKey="1">Action</MenuItem> 
 <MenuItem eventKey="2">Another action</MenuItem> 
 <MenuItem eventKey="3" active>Active Item</MenuItem> 
 <MenuItem divider /> 
 <MenuItem eventKey="4">Separated link</MenuItem> 
 </DropdownButton> 
 ); 
} 
const buttonsInstance = ( 
 <ButtonToolbar>{renderDropdownButton}</ButtonToolbar> 
); 

ReactDOM.render(buttonsInstance, mountNode); 
```

React-Bootstrap은 부트스트랩의 재사용 가능한 구성 요소로 캡슐화하여 반복되는 html 태그를 줄입니다.

또한, 코드 내비게이션을 원활하게하여 구조를 단순화고 앞으로 구현해야될 코드양이 적습니다.

## 로컬 환경에서 React-Bootstrap 시작하기

React-Bootstrap을 사용하는 가장 좋은 방법은 yarn(또는 npm)으로 설치할 수있는 npm 패키지를 사용하는 것입니다. 그러기 위해서는 npm 패키지를 먼저 설치해 주세요.

엘리스실습을 할 때는 설치를 할 필요 없습니다. 참고만 해주세요.

1. 리액트 부트스트랩 설치하기 (윈도우)
```
yarn add react-bootstrap bootstrap

//또는 npm으로 설치
npm install react-bootstrap bootstrap
```
    1-2. 리액트 부트스트랩 설치하기 (리눅스)
    ```
    npm install --save bootstrap
    ```

2.  프로젝트 만들고 프로젝트 폴더 이동
```
$ create-react-app react-boot1
$ cd react-boot1
```

3. 프로젝트 이동 후 실행
```
$ pip install yarn
$ yarn start
or $ npm start
```
리액트 로고가 뜬 화면이 나오면 성공입니다.
이제 간단한 예제로 버튼을 만들어 볼까요?

4. react-bootstrap을 설정해줍니다.
```
$ yarn add react-bootstrap
```
이렇게 윈도우나 리눅스에 리액트 부트스트랩을 어떻게 설치하는지 알아보았습니다. 그럼 이제 가장 간단한 방법도 알아봅시다.

### 가장 간편하게 리액트 부트스트랩 설치하는 방법

```
npx create-react-app my-app
cd my-app
npm start
npm install react-bootstrap bootstrap
```
이제부터 본격적으로 부트스트랩을 활용해봅시다.

1. 먼저 CSS stylesheet를 설정해줍니다.
```
최상단의 루트파일인 src/index.js 또는 App.js 파일에 다음 스타일을 추가해줍니다.

import 'bootstrap/dist/css/bootstrap.min.css';
```

또는 간단하게 상단에 CDN형태로 추가하면 쉽게 사용 할수 있습니다.
```
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
```

2. 컴포넌트 import하기

전체 라이브러리가 아닌 react-bootstrap / Button과 같은 사용해야 되는 개별 구성 요소를 가져와야 특정 구성 요소만 가져오므로 클라이언트로 보내는 코드의 양을 크게 줄일 수 있습니다.
```
import Button from 'react-bootstrap/Button';
import ButtonToolbar from 'react-bootstrap/Button';
// 또는
import { Button, ButtonToolbar } from 'react-bootstrap';
```

3. App.js 에서 버튼 예제 실행해보기
```
import React, { Component } from 'react';
import { ButtonToolbar, Button } from 'react-bootstrap';

// src/App.js

function App() {
  return (
    <div>
      <Button variant="primary">Click Me!</Button>
    </div>
  );
}
export default App;
```

버튼이 만들어 지면 성공입니다.

# Yarn 설치하기

1. yarn 윈도우에서 설치하기

윈도우 키 + R 를 누르시거나 실행 창에 cmd로 입력한 뒤 확인 버튼을 눌러서 command 프로그램을 실행합니다.

(mac 일 경우 ⌘ Command + Space > terminal을 눌러 실행합니다.)

검은색 창이뜨면 “yarn” 명령어를 실행하여 아래의 메시지가 나오면 설치 완료 된것입니다.
```
yarn install v0.24.6
[1/4] Resolving packages...
success Already up-to-date.
Done in 0.05s.
```

1-1. yarn 리눅스에서 설치하기
```
//yarn 설치
$ sudo apt-get update && sudo apt-get install yarn
//만약 설치가 안된다면 npm을 통해 설치
$ npm install -g yarn
```

2. package.json 설정
새 프로젝트를 시작할 때나 초기화 할 때 package.json을 생성합니다.
```
$ yarn init
yarn init v1.13.0
question name (react): aa
question version (1.0.0): 1.0.0
question description: test
question entry point (index.js): index.js
question repository url: localhost
question author: pss
question license (MIT): MIT
question private:
success Saved package.json
Done in 34.17s.

//아래와 같은 package.json파일 생성
{
  "name": "aa",
  "version": "1.0.0",
  "description": "test",
  "main": "index.js",
  "repository": "localhost",
  "author": "pss",
  "license": "MIT"
}
```

3. 패키지 설치하기
```
$ yarn install 
또는 (install은 생략가능)
$ yarn
```

4. bootstrap 라이브러리 설치하기
```
yarn add bootstrap
# npm을 쓴다면  
npm install --save bootstrap
```

5. bootstrap import 하기
```
import 'bootstrap/dist/css/bootstrap.css'
```
src/index.js와 같이 최상위에서 컴포넌트 호출하는 소스에 넣어주면 한 번만 입력해도 모든 컴포넌트에 적용됩니다.

