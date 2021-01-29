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
