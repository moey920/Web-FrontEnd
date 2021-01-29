Grid System이란?
그리드(Grid)는 Bootstrap이 가장 많이 사용되는 이유이자 반응형 웹페이지를 만들기 위해서 가장 많이 사용이 필요한 기능입니다.
Bootstrap을 시작할 때 가장 먼저 이해해야 할 것이 바로 모바일 친화적인 인터페이스를 담당하는 12열 그리드(Grid) 시스템입니다.

부트스트랩 그리드 시스템은 방문자가 사용하는 화면의 크기를 인식하고 이에 적응하는 웹 레이아웃을 만드는 데 사용되는 매우 일반적인 기술입니다. 그리드 시스템을 사용하면 와이드 스크린 모니터가있는 개인용 컴퓨터에서 웹 사이트를 만든 경우에도 웹 사이트가 휴대폰이나 태블릿에 잘못 표시 될 우려가 없습니다.

그리드 적용이 익숙해지면 다른 장치에서 볼 때 웹 사이트가 어떻게 확장 및 축소되는지 쉽게 상상할 수 있기 때문에 매우 유용합니다.

Bootstrap 4 열과 행의 작동 방식과이를 조작하여 최신 웹 사이트에 대한 반응 형 레이아웃을 만드는 방법을 알아봅시다.

Bootstrap에서 그리드 시스템은 flexbox로 제작됐으며 페이지 전체에 최대 12개의 열(Column)으로 나눌수 있습니다.





이를 테이블의 형식대로 row 클래스와 각종 col- 클래스들로 자유롭게 구성이 가능하며, 이렇게 구성한 페이지들은 Bootstrap에서 알아서 크기에 따라 반응형으로 동작하도록 만드는 것입니다.

Bootstrap에서는 아래의 규칙대로 이러한 그리드 시스템을 구축할 수 있습니다.

row 클래스는 container나 container-fluid 안에 있어야 정상적인 배열이나 패팅을 지원해줍니다.
row 클래스는 가로로 그룹 지을 칼럼들의 집합입니다.
내용은 col 클래스 안에 있어야 하며, row의 직속 자녀 요소로 배치해야 합니다.
칼럼은 총 12칼럼이 있는 것으로 정의하여 각 배치할 %에 따라서 클래스를 결정하면 된다. 예를 들어, 같은 넓이의 3개의 칼럼을 쓰고자 한다면 3개의 .col-xs-4 칼럼을 쓰면 됩니다.
12칼럼이 넘어가면 새로운 줄로 칼럼이 배치됩니다.
bootstrap 4 그리드의 기본 구조
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
보시다시피 행(Row)은 열(Col)를 감싸안는 래퍼(wrapper)입니다.
첫번째 row는 5길이의 col 2개, 두번째 row는 3길이의 col 4개로 완전히 채우고 마지막 row는 5길이의 col 3개를 채우려다 자리가 모자라서 3번째 col은 밑으로 내려간 것을 보실 수 있습니다.

image

그리드 사용하기 (1)

<section class = "row">처럼 행을 만들고
그 행에 원하는 수 만큼의 열을 <section class = "col-(1)-(2)> 와 같이 추가합니다.
(1)에는 기기의 크기로서 sm, md, lg 또는 xl을 기입합니다.
(2)에는 숫자를 적는 부분으로 각 행은 최대 12까지 사용할 수 있습니다.
참고표

Screen	Viewport Size	Class prefix
Extra small	< 576px	.col-*
Small	≥ 576px	.col-sm-*
Medium	≥ 768px	.col-md-*
Large	≥ 992px	.col-lg-*
Extra large	≥ 1200px	.col-xl-*
그리드 사용하기 (2)

각 열에 숫자를 추가하지 말고 Bootstrap 기본값을 사용하는 방식으로 자동으로 레이아웃을 처리하게 됩니다.
class = “col”
->2개의 열을 사용하면 각 열의 넓이는 50% 씩 늘어나고
3개의 열을 사용하면 33.33% 씩,
4개의 열은 25%씩 자동으로 늘어납니다.

이렇게 모든 화면 너비에 대해 열이 모두 같은 넓이가 되기 위해서는
<div class ="row>
        <div class = "col">.col</div>
        <div class = "col">.col</div>
        <div class = "col">.col</div>
</div>
이렇게 해주면 됩니다.
