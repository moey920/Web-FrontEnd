# Grid System이란?

그리드(Grid)는 Bootstrap이 가장 많이 사용되는 이유이자 반응형 웹페이지를 만들기 위해서 가장 많이 사용이 필요한 기능입니다.

Bootstrap을 시작할 때 가장 먼저 이해해야 할 것이 바로 모바일 친화적인 인터페이스를 담당하는 **12열 그리드(Grid) 시스템**입니다.

부트스트랩 그리드 시스템은 방문자가 사용하는 **화면의 크기를 인식하고 이에 적응하는 웹 레이아웃을 만드는 데 사용되는** 매우 일반적인 기술입니다. 

그리드 시스템을 사용하면 와이드 스크린 모니터가있는 개인용 컴퓨터에서 웹 사이트를 만든 경우에도 웹 사이트가 휴대폰이나 태블릿에 잘못 표시 될 우려가 없습니다.

그리드 적용이 익숙해지면 다른 장치에서 볼 때 웹 사이트가 어떻게 확장 및 축소되는지 쉽게 상상할 수 있기 때문에 매우 유용합니다.

Bootstrap 4 열과 행의 작동 방식과이를 조작하여 최신 웹 사이트에 대한 반응 형 레이아웃을 만드는 방법을 알아봅시다.

Bootstrap에서 그리드 시스템은 flexbox로 제작됐으며 **페이지 전체에 최대 12개의 열(Column)**으로 나눌수 있습니다.

![image.png](./image.png)


이를 테이블의 형식대로 row 클래스와 각종 col- 클래스들로 자유롭게 구성이 가능하며, 이렇게 구성한 페이지들은 Bootstrap에서 알아서 크기에 따라 반응형으로 동작하도록 만드는 것입니다.

Bootstrap에서는 아래의 규칙대로 이러한 그리드 시스템을 구축할 수 있습니다.

- row 클래스는 container나 container-fluid 안에 있어야 정상적인 배열이나 패팅을 지원해줍니다.
- row 클래스는 가로로 그룹 지을 칼럼들의 집합입니다.
- 내용은 col 클래스 안에 있어야 하며, row의 직속 자녀 요소로 배치해야 합니다.
- 칼럼은 총 12칼럼이 있는 것으로 정의하여 각 배치할 %에 따라서 클래스를 결정하면 됩니다. 예를 들어, 같은 넓이의 3개의 칼럼을 쓰고자 한다면 3개의 .col-xs-4 칼럼을 쓰면 됩니다.
- 12칼럼이 넘어가면 새로운 줄로 칼럼이 배치됩니다.

## bootstrap 4 그리드의 기본 구조
```
<div class="container-fluid" >
    <div class="row"> 
        <div class="col-xs-3">.col-xs-5</div> 
        <div class="col-xs-3">.col-xs-5</div> 
    </div> 
    <div class="row"> 
        <div class="col-sm-3">.col-sm-3</div>
        <div class="col-sm-3">.col-sm-3</div> 
        <div class="col-sm-3">.col-sm-3</div>
        <div class="col-sm-3">.col-sm-3</div> 
    </div> 
    <div class="row">
        <div class="col-md-3">.col-md-5</div> 
        <div class="col-md-3">.col-md-5</div> 
        <div class="col-md-3">.col-md-5</div> 
    </div> 
</div>
```

보시다시피 행(Row)은 열(Col)를 감싸안는 래퍼(wrapper)입니다.

첫번째 row는 5길이의 col 2개, 두번째 row는 3길이의 col 4개로 완전히 채우고 마지막 row는 5길이의 col 3개를 채우려다 자리가 모자라서 3번째 col은 밑으로 내려간 것을 보실 수 있습니다.

![image-1.png](./image-1.png)

### 그리드 사용하기 (1)

1. ```<section class = "row">```처럼 행을 만들고
2. 그 행에 원하는 수 만큼의 열을 ```<section class = "col-(1)-(2)>``` 와 같이 추가합니다.
    - (1)에는 기기의 크기로서 sm, md, lg 또는 xl을 기입합니다.
    - (2)에는 숫자를 적는 부분으로 각 행은 최대 12까지 사용할 수 있습니다.

참고표

| Screen | Viewport Size | Class prefix |
|:---:|:---:|:---:|
| Extra small | < 576px | .col-* |
| Small | ≥ 576px | .col-sm-* |
| Medium | ≥ 768px | .col-md-* |
| Large | ≥ 992px | .col-lg-* |
| Extra large | ≥ 1200px | .col-xl-* |
	
### 그리드 사용하기 (2)

1. 각 열에 숫자를 추가하지 말고 Bootstrap 기본값을 사용하는 방식으로 자동으로 레이아웃을 처리하게 됩니다.
    class = “col”
-> 2개의 열을 사용하면 각 열의 넓이는 50% 씩 늘어나고
3개의 열을 사용하면 33.33% 씩,
4개의 열은 25%씩 자동으로 늘어납니다.

2. 이렇게 모든 화면 너비에 대해 열이 모두 같은 넓이가 되기 위해서는
```
<div class ="row>
        <div class = "col">.col</div>
        <div class = "col">.col</div>
        <div class = "col">.col</div>
</div>
```
이렇게 해주면 됩니다.

#### 그리드 실습

grid 시스템으로 동일 간격의 레이아웃 만들기를 해봅시다.

다음 표에서 부트 스트랩 그리드 시스템의 xs에서 xl까지 여러 장치에서 작동하는 방식을 확인해봅시다.

|  | small | medium | large | extra-large |
|:---:|:---:|:---:|:---:|:---:|
| Max container width | 540px | 720px | 960px | 1140px |
| Class prefix | .col-sm- | .col-md- | .col-lg- | .col-xl- |
| # of columns | 12 |
| Gutter width | 30px (15px on each side of a column) |
| Nestable | Yes |

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
    <button type="button" className="btn btn-primary">
        Bootstrap Button!
    </button>
    <div class = "padd">컨테이터를 같은 간격(1:1:1)의 3개의 기둥으로 나눠보세요. </div>
    <div class="container">
        <div class="row">
            <div class="col">1 of 3</div>
            <div class="col">2 of 3</div>
            <div class="col">3 of 3</div>
        </div>
    </div>

    <div class = "padd"> 2.  다음은 2줄(row)를 같은간격으로 2등분, 3등분 해봅시다 </div>
    <div class="container">
        <div class="row">
            <div class="col-md-4">1 of 2</div>
            <div class="col-md-4">2 of 2</div>
        </div>
        <div class="row">
            <div class="col-md-4">1 of 3</div>
            <div class="col-md-4">2 of 3</div>
            <div class="col-md-4">3 of 3</div>
        </div>
    </div>

    <div class = "padd"> 3. 다음은 4개의 같은간격의 기둥 한줄(row)와 2:1의 길이의 기둥 한 줄을 만들어봅시다</div>
    <div class="container">
        <div class="row">
                <div class="col-md-4">1 of 4</div>
                <div class="col-md-4">2 of 4</div>
                <div class="col-md-4">3 of 4</div>
                <div class="col-md-4">4 of 4</div>
            </div>
            <div class="row">
                <div class="col-md-8">1 of 2</div>
                <div class="col-md-4">2 of 2</div>
            </div>
        </div>

    </div> // className="App" 닫는 div

    ); // return 닫는 괄호
    } // render 닫는 괄호
} // 클래스 컴포넌트 닫는 괄호

export default App;
```
-----

# Container에 컴포넌트 추가하기

Bootstrap에서 사용할 수 있는 컴포넌트는 Alerts, Badge, Button, Card, Dropdown, Forms, Input group, List group, Navbar, Navs 등 매우 다양합니다.

그 중에 Navbar로 예를 들어보겠습니다. Navbar는 애플리케이션 또는 사이트에 대한 탐색 헤더를 제공합니다. 

Navbar는 모바일 보기에서 축소되고 사용 가능한 뷰포트 너비가 증가함에 따라 수평이 되어 편리합니다.

- 아주 간단한 navbar를 생성하려면 반응형 축소 클래스 .navbar-expand-xl | lg | md | sm (초대형, 대형, 중형 또는 소형 화면)이 있는 .navbar 클래스를 추가하세요.
- navbar에 링크를 추가하려면 .navbar-nav 클래스를 사용하여 정렬되지 않은 목록을 추가하면됩니다.
- 각 개별 목록 항목을 정의하려면 ```<li>```태그 클래스에 .nav-item 클래스를 추가하고 개별 링크의 ```<a>``` 태그 클래스에 .nav-link 클래스를 사용합니다.

## Navbar 예시
```
      <div class="container">
         <h2>Basic Navbar</h2>
         <nav class="navbar navbar-expand-sm navbar-dark bg-secondary">
            <a class="navbar-brand" href="#">Navbar</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
               <ul class="navbar-nav mr-auto">
                  <li class="nav-item active">
                     <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
                  </li>
                  <li class="nav-item">
                     <a class="nav-link" href="#">About Us</a>
                  </li>
                  <li class="nav-item">
                     <a class="nav-link" href="#">Contact</a>
                  </li>
               </ul>
            </div>
         </nav>
      </div>
```

결과 화면

![image-2.png](./image-2.png)

Bootstrap4의 더 많은 컴포넌트들의 응용방법 확인하기 → <https://getbootstrap.com/docs/4.0/components/buttons/>


# Bootstrap 레이아웃 - Container

Container는 레이아웃을 만드는 가장 상위 요소에 들어갑니다.

앞서 이론1에서 배운 그리드 시스템이 레이아웃을 결정짓는 큰 범주 였다면 그 외에 모든 컴포넌트와 웹을 구성하는 모든 컨텐츠들을 배치할수 있게 도와주는 것이 레이아웃 시스템입니다. 

부트스트랩의 수십개의 유틸리티 클래스가 콘텐츠 표시, 숨기기, 정렬 및 간격 조정을 할수 있습니다.

**container 클래스**는 **고정 된 너비로 페이지 콘텐츠를 감싸는 데 사용**되며 아래와 같이 .container 클래스를 사용하여 콘텐츠를 중앙에 쉽게 배치 할 수 있습니다.
```
<div class = "container">
   ...
</div>
```

Bootstrap 4는 컨테이너 클래스를 사용하여 페이지의 내용을 래핑합니다. 그 종류에는 fixed와 fluid 2가지가 있습니다.

```.container``` : 고정된 너비 컨테이너를 나타냅니다.
```.container-fluid``` : 뷰포트의 전체 너비에 걸쳐 컨테이너를 나타냅니다.

1. container는 Media query에 의해 반응형을 동작합니다.

   가로 해상도 767px 이하에서는 100%

   768px 이상에서는 750px

   992px 이상에서는 970px

   1200px 이상에서는 1170px의 가로폭을 가집니다.

2. container-fluid는 가로 해상도에 상관없이 100%의 width를 가집니다.
```
<body>
  <div class="container">
    <div class="fixed">fixed width (.container)</div>
  </div>
  <br>
  <div class="container-fluid">
    <div class="fluid">full width (.container-fluid)</div>
  </div>
</body>
```

```
<!DOCTYPE HTML>
<html>
    <head>
        <title>.container vs .container-fluid</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="style.css">
         <link rel = "stylesheet" 
         href = "https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" 
         integrity = "sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" 
         crossorigin = "anonymous">
    </head>
    <body>
        <div class="container">
            <div class="fixed">fixed width(.container)</div>
            <h2>Fixed Width Container</h2>
            <code>.container</code> class로 고정된 컨테이너를 만들어봅시다
        </div>
      <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    </body>
 
 
    <body>
    <div class="container-fluid">
        <div class="fluid">fixed width(.container-fluid)</div>
        <h2>Full Width Container</h2>
        <code></code> class로 늘어날 수 있는 컨테이너입니다.
    </div>
      <!-- jQuery first, then Popper.js, then Bootstrap JS -->
      <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
      <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
   </body>
</html>
```
![image-3.png](./image-3.png)

# Grid 레이아웃시스템

Bootstrap 4부터 Grid 레이아웃시스템이 더 정교하고 세밀하게 발전했습니다.

- 화면의 너비를 12 분할하는 것은 동일하지만 반응하는 화면의 기준너비는 4가지 에서 5가지로 세분화되었습니다.
- 숫자 명시없이 ```<div classs="col">```의 갯수에 따라 자동 분할합니다.

예를들어 아래와 같이 입력하면 2등분이 되는 것 입니다.
```
<div class="col">

      1 of 2

</div>

<div class="col">

      2 of 2

</div>
```

다음과 같이 페이지를 만들어 봅시다
```
<div class="container">
  <div class="row">
    <div class="col">

      1 of 3

    </div>

    <div class="col">

      2 of 3

    </div>

    <div class="col">

      3 of 3

    </div>
  </div>
</div>
```

이렇게 하면 576px 미만의 브라우저 너비부터 최대너비크기까지 3등분이 되겠죠?

어떤 브라우저 너비로 보던 모두 3등분되는 것입니다.

Container 안에 여러 개의 row가 들어갈 수도 있습니다.
```
<div class="container">
    <div class="row">
        <div class="col-md-4">

          1 of 3

        </div>
        <div class="col-md-4">

          2 of 3

        </div>
        <div class="col-md-4">

          3 of 3

        </div>
    </div>
    <div class="row">
        <div class="col-md-6">

          1 of 2

        </div>
        <div class="col-md-6">

          2 of 2

        </div>
    </div>
 </div> 
 ```

## Bootstrap의 Navbar 와 Dropdown 만들기 실습

Bootstrap의 반응형 컴포넌트 중 하나면서 헤더에서 많이 사용되는 Navbar는 드롭다운 메뉴와 검색창(search bar)등의 기능이 포함됩니다. 

Navbar는 반응형이면서도 쉽게 수정할 수 있습니다. 

큰 화면에서는 가로로 표시되고 소형 및 모바일 화면 (768px 이하)에서는 “햄버거” 드롭다운 메뉴로 변환됩니다. 

내부적으로 navbar는 메뉴 항목의 정렬되지 않은 인라인 목록이며 원하는대로 추가 된 HTML 요소가 추가됩니다. 

추가 가능한 항목 중에는 브랜딩 (텍스트 또는 로고), 검색 창과 같은 양식 항목 및 메뉴 드롭다운이 있습니다.

### 지시사항

1. Navbar 의 우선순위는 이렇게 됩니다.

먼저 navbar-brand 내비게이션에 가장 크게 찍힐 회사, 제품 또는 프로젝트 이름 등 을 넣으세요.

2. 그 다음 아래 코드 처럼 navbar-nav 로 전체 높이를 정한 다음 toggler동작을 ```<body></body>```안에 추가해보세요.
```
<nav class="navbar navbar-expand-lg navbar-light bg-light">
<a class="navbar-brand" href="#">회사, 제품 또는 프로젝트 이름</a>
<button class="navbar-toggler" type="button" data-toggle="collapse" label="Toggle navigation">  </button>
<div class="collapse navbar-collapse" id="navbarNavDropdown">
<ul class="navbar-nav">
<li class="nav-item active">
<a class="nav-link" href="#">Home</a>
</li>
</ul>
</div>
</nav>
```

navbar nav에서 드롭 다운을 사용할 수도 있습니다. 

드롭 다운 메뉴에는 배치를위한 래핑 요소가 필요하므로 아래와 같이 .nav-item 및 .nav-link에 대해 별도의 중첩 요소를 사용해야합니다.

드랍다운 버튼을 이런식으로 추가해보세요.
```
<li class="nav-item dropdown">
<a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
Dropdown link
</a>
<div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
<a class="dropdown-item" href="#">Action</a>
<a class="dropdown-item" href="#">Another action</a>
<a class="dropdown-item" href="#">Something else here</a>
</div>
</li>
```

> Tips : Navbar에는 몇 가지 하위 구성 요소에 대한 지원이 내장되어 있습니다. 필요에 따라 다음 중에서 선택하세요.

- ```.navbar-brand``` : 회사, 제품 또는 프로젝트 이름 등
- ```.navbar-nav``` : 전체 높이 및 내비게이션 (드롭 다운 지원 포함)
- ```.navbar-toggler``` : 축소 플러그인 및 기타 내비게이션 토글 동작
- ```.form-inline``` : 모든 form 양식 컨트롤 및 작업
- ```.navbar-text``` : 가운데 세로로 정렬된 텍스트 문자열을 추가

### 실습 코드
```
<!DOCTYPE HTML>
<html>
    <head>
        <title>.container vs .container-fluid</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="style.css">
        <link rel = "stylesheet" 
         href = "https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" 
         integrity = "sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" 
         crossorigin = "anonymous">
        <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
    </head>
    <body>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#">노하람 부트스트랩</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" label="Toggle navigation">
            </button>
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
            <ul class="navbar-nav">
                <li class="nav-item active">
                    <a class="nav-link" href="#">Home</a>
                </li>
                <li class="nav-item active">
                    <a class="nav-link" href="#">게시판 1</a>
                </li>
                <li class="nav-item active">
                    <a class="nav-link" href="#">게시판 2</a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    메뉴</a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
                        <a class="dropdown-item" href="#">액션1</a>
                        <a class="dropdown-item" href="#">액션2</a>
                        <a class="dropdown-item" href="#">액션3</a>
                    </div>
                </li>
            </ul>
            </div>
        </nav>   
      <!-- jQuery first, then Popper.js, then Bootstrap JS -->
 
    </body>
 
 
    <body>

      <!-- jQuery first, then Popper.js, then Bootstrap JS -->
        <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
   </body>
</html>
```

# React bootstrap의 Carousel 만들기 실습(슬라이드 기능)

## Carousel 개념

Carousel (캐러샐)은 이미지 또는 텍스트 슬라이드를 순환하는 부트스트랩의 구성 요소입니다.

캐러셀은 CSS 3D 변환과 약간의 자바 스크립트로 제작 된 일련의 콘텐츠를 순환하는 슬라이드로 일련의 이미지, 텍스트 또는 사용자 정의 마크 업과 함께 작동합니다. 

또한 이전 / 다음 컨트롤 및 표시에 대한 지원도 포함합니다.

## Carousel 사용하기

Carousel은 제품을 홍보하거나 포트폴리오를 보여주는 웹페이지 등에 유용하게 쓰입니다.

대체로 다음 상황에 해당될 때 유용합니다.

- 여러 항목의 이미지를 슬라이드 처럼 나타낼 때
- 슬라이더를 한 번에 하나씩 만 진행할 때
- 비교적 작은 화면에 단일 항목만 나타날 때

### 지시사항

가장 기본적인 형태의 carousel 슬라이드쇼를 만드세요.
```
 <!-- The slideshow -->
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="portugal.jpeg" alt="Los Angeles" width="1100" height="500">
    </div>
    <div class="carousel-item">
      <img src="paris2.jpeg" alt="Chicago" width="1100" height="500">
    </div>
    <div class="carousel-item">
      <img src="nyc.jpeg" alt="New York" width="1100" height="500">
    </div>
  </div>
```

그 다음은 이전과 다음 버튼을 만들어보세요.
```
 <a class="carousel-control-prev" href="#demo" data-slide="prev">
    <span class="carousel-control-prev-icon"></span>
  </a>
  <a class="carousel-control-next" href="#demo" data-slide="next">
    <span class="carousel-control-next-icon"></span>
  </a>
```

몇번째 페이지인지 암시하는 page indicator를 추가해 보세요.
```
  <ul class="carousel-indicators">
    <li data-target="#demo" data-slide-to="0" class="active"></li>
    <li data-target="#demo" data-slide-to="1"></li>
    <li data-target="#demo" data-slide-to="2"></li>
  </ul>
```

슬라이드쇼 아이템에 대한 간단한 설명을 caption으로 추가하세요.
```
<div class="carousel-inner">
    <div class="carousel-item active">
      <img src="..." class="d-block w-100" alt="...">
      <div class="carousel-caption d-none d-md-block">
        <h5>First slide label</h5>
        <p>Nulla vitae elit libero, a pharetra augue mollis interdum.</p>
      </div>
    </div>
```

### 실습 코드
```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Bootstrap Example</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <style>
    /* Make the image fully responsive */
    .carousel-inner img {
        width: 100%;
        height: 100%;
    }
    </style>
</head>
<body>

    <div id="demo" class="carousel slide" data-ride="carousel">

        <!-- Indicators -->
        <ul class="carousel-indicators">
            <li data-target="#demo" data-slide-to="0" class="active"></li>
            <li data-target="#demo" data-slide-to="1" class="active"></li>
            <li data-target="#demo" data-slide-to="2" class="active"></li>
        </ul>
        
        <!-- Carousel 슬라이드쇼를 만드세요 -->
        <!-- The slideshow -->
        <div class="carousel-inner">
            <div class="carousel-item active">
                <img src="portugal.jpeg" class="d-block w-100" alt="Los Angeles" width="1100" height="500">
                <div class="carousel-caption d-none d-md-block">
                    <h5>First slide label</h5>
                    <p>Nulla vitae elit libero, a pharetra augue mollis interdum.</p>
                </div>
            </div>
            <div class="carousel-item">
                <img src="paris2.jpeg" alt="Chicago" width="1100" height="500">
            </div>
            <div class="carousel-item">
                <img src="nyc.jpeg" alt="New York" width="1100" height="500">
            </div>
        </div>

        
        <!-- 이전 다음 버튼을 만드세요 -->
         <a class="carousel-control-prev" href="#demo" data-slide="prev">
            <span class="carousel-control-prev-icon"></span>
        </a>
        <a class="carousel-control-next" href="#demo" data-slide="next">
            <span class="carousel-control-next-icon"></span>
        </a>
    </div>

</body>
</html>
```
