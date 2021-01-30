# Bootstrap을 활용한 웹사이트 제작 프로젝트

앞서 2장과 3장에서 Bootstrap에서 가장 많이 쓰이는 컴포넌트 몇 가지를 응용해 보았습니다.
컴포넌트를 사용하는 것이 익숙해지면 세련된 프론트엔드를 빠르고, 쉽게 구현할 수 있을 것입니다.

마지막 4장에서는 부트스트랩 무료 템플릿을 활용하여 반응형 웹사이트를 제작해보겠습니다.

반응형 대시보드나 게시판 등이 포함된 게시판을 스스로 만들 수 있게 되면 앞으로 큰 프로젝트나 스타트업에서 많은 프로젝트들을 마스터 하는데 한 걸을 전진하신 겁니다!

## Bootstrap navbar와 sign-in button

- 페이지 상단 에 만드세요
- navbar는 dropdown버튼이 포함되어야 합니다

> Tips : Navbar에는 몇 가지 하위 구성 요소에 대한 지원이 내장되어 있습니다. 필요에 따라 다음 중에서 선택하세요.

- ```.navbar-brand``` : 회사, 제품 또는 프로젝트 이름 등
- ```.navbar-nav``` : 전체 높이 및 내비게이션 (드롭 다운 지원 포함)
- ```.navbar-toggler``` : 축소 플러그인 및 기타 내비게이션 토글 동작
- ```.form-inline``` : 모든 form 양식 컨트롤 및 작업
- ```.navbar-text``` : 가운데 세로로 정렬된 텍스트 문자열을 추가

``` 
body 태그 내에 입력하세요
    <div class="container">
        <h2 class="mb-5">페이지 상단.</h2>
        <nav class="navbar navbar-expand-lg navbar-light gb-light">
            <a class="navbar-brand" href="#">하람 부트스트랩</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" label="Toggle navigation"></button>
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
                <ul class="navbar-nav">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Home</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Dropdown link</a>
                        <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                            <a class="dropdown-item" href="#">Action</a>
                            <a class="dropdown-item" href="#">Action2</a>
                            <a class="dropdown-item" href="#">Action3</a>
                        </div>
                    </li>
                </ul>
            </div>
        </nav>
    </div>
```










