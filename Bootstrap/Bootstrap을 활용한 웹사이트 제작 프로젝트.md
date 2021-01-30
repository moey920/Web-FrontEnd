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

## Bootstrap carousel(이미지 슬라이드쇼)

### Carousel 개념

Carousel (캐러샐)은 이미지 또는 텍스트 슬라이드를 순환하는 부트스트랩의 구성 요소입니다.

캐러셀은 CSS 3D 변환과 약간의 자바 스크립트로 제작 된 일련의 콘텐츠를 순환하는 슬라이드로 일련의 이미지, 텍스트 또는 사용자 정의 마크 업과 함께 작동합니다. 

또한 이전 / 다음 컨트롤 및 표시에 대한 지원도 포함합니다.

```
<!-- Masthead -->
  <header class="masthead text-white text-center">
    <div class="overlay"></div>
    <div class="container">
        
        <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
            <!-- carousel-indicators -->
            <ol class="carousel-indicators">
                <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
                <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
                <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
            </ol>
            <!-- The slideshow -->
            <div class="carousel-inner">
                <div class="carousel-item active">
                    <img class="d-block w-100" src="..." alt="First slide">
                </div>
                <div class="carousel-item">
                    <img class="d-block w-100" src="..." alt="Second slide">
                </div>
                <div class="carousel-item">
                    <img class="d-block w-100" src="..." alt="Third slide">
                </div>
            </div>
            <!-- prev,next botton -->
            <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="sr-only">Previous</span>
            </a>
            <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="sr-only">Next</span>
            </a>
        </div>
    </div>
  </header>
```

## Bootstrap Grid

### 그리드 시스템 규칙

- row 클래스는 container나 container-fluid 안에 있어야 정상적인 배열이나 패팅을 지원해줍니다
- row 클래스는 가로로 그룹 지을 칼럼들의 집합입니다
- 내용은 col-* 클래스 안에 있어야 하며, row의 직속 자녀 요소로 배치해야 합니다
- 칼럼은 총 12칼럼이 있는 것으로 정의하여 각 배치할 %에 따라서 클래스를 결정하면 된다. 예를 들어, 같은 넓이의 3개의 칼럼을 쓰고자 한다면 3개의 .col-xs-4 칼럼을 쓰면 됩니다
- 12칼럼이 넘어가면 새로운 줄로 칼럼이 배치됩니다

```
  <!-- Icons Grid -->
  <section class="features-icons bg-light text-center">
    <div class="container">
      <h2> 페이지 중간 grid 만들기 3(가로)*1(세로))</h2>
      <div class="row">
          <div class="col-lg-4">.col-lg-4</div>
          <div class="col-lg-4">.col-lg-4</div>
          <div class="col-lg-4">.col-lg-4</div>
      </div>
    </div>
  </section>
```

## typography 변형하기

```
<p> 마크 태그를 사용하여 텍스트를<mark> 강조 표시 </ mark> 할 수 있습니다.</p>
<p><del>이 문장은 삭제된 텍스트로 취급됩니다.</del></p>
<p><s>이 문장은 더 이상 정확하지 않은 것으로 간주됩니다. </s></p>
<p> <ins>이 문장은 문서에 추가된 것으로 취급됩니다. </ ins></ p>
<p><u>이 줄 밑줄로 표시됩니다. </u></p>
<p><small>이  문장은 작은 글씨로 처리됩니다. </small></p>
<p><strong>이 줄은 bold 텍스트로 렌더링되었습니다. </strong></p>
<p><em>이 줄은 italic 텍스트로 렌더링되었습니다. </em></p>
```

-  blockquote로 text alignment(텍스트 위치)를 바꾸어 보세요.
```
<div>
    <blockquote class="blockquote text-center">
        <p class="mb-0">>A well-known quote, contained in a blockquote element.</p>
        <footer class="blockquote-footer">Someone famous in <cite title="Source Title">Source Title</cite></footer>
    </blockquote>
    <blockquote class="blockquote text-left">
        <p class="mb-0">A well-known quote, contained in a blockquote element.</p>
        <footer class="blockquote-footer">Someone famous in <cite title="Source Title">Source Title</cite></footer>
    </blockquote>
</div>
```

```
<!-- Image Showcases -->
  <section class="showcase">
    <div class="container-fluid p-0">
      <div class="row no-gutters">
        <div class="col-lg-6 order-lg-2 text-white showcase-img" style="background-image: url('img/bg-showcase-1.jpg');"></div>
     <h2>페이지 중간 -  Typography - 폰트 굵기, 밑줄 등으로 다양하게 표현하기 </h2>
     <div class="col-lg-6 order-lg-1 my-auto showcase-text">
          <h2>Fully Responsive Design</h2>
          <p class="lead mb-0">When you use a theme <strong>created</strong> by <mark>Start Bootstrap</mark>, you know that the theme will look great on any device, whether it's a phone, tablet, or desktop the page will behave responsively!</p>
        </div>
      </div>
      <div class="row no-gutters">
        <div class="col-lg-6 text-white showcase-img" style="background-image: url('img/bg-showcase-2.jpg');"></div>
        <div class="col-lg-6 my-auto showcase-text">
          <h2>Updated For <em>Bootstrap 4</em></h2>
          <p class="lead mb-0">Newly <s>improved</s>, and full of great utility classes, Bootstrap 4 is leading the way in mobile responsive web development! All of the themes on Start Bootstrap are now using Bootstrap 4!</p>
        </div>
      </div>
      <div class="row no-gutters">
        <div class="col-lg-6 order-lg-2 text-white showcase-img" style="background-image: url('img/bg-showcase-3.jpg');"></div>
        <div class="col-lg-6 order-lg-1 my-auto showcase-text">
          <h2>Easy to Use &amp; Customize</h2>
          <p class="lead mb-0">Landing Page is just <u>HTML and CSS</u> with a splash of SCSS for users who demand some deeper customization options. Out of the box, just add your content and images, and your new landing page will be ready to go!</p>
        </div>
      </div>
    </div>
  </section>
```

## Form 활용

Bootstrap의 Form은 브라우저와 모바일에서 보다 일관된 렌더링을 위해 맞춤형 디스플레이를 선택할 수 있습니다.

이메일 확인, 번호 선택 등과 같은 새로운 입력 컨트롤을 활용하려면 모든 입력에 적절한 유형 속성 (예 : 이메일 주소의 이메일 또는 숫자 정보의 번호)을 사용해야합니다.

```
<!-- Call to Action -->
  <section class="call-to-action text-white text-center">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-xl-9 mx-auto">
          <h2 class="mb-4">Ready to get started? Sign up now!</h2>
        </div>
        <div class="col-md-10 col-lg-8 col-xl-7 mx-auto">
          <form>
            <div class="form-row">
              <div class="col-12 col-md-9 mb-2 mb-md-0">
                <input type="email" class="form-control form-control-lg" placeholder="Enter your email...">
              </div>
              <div class="col-12 col-md-3">
                <button type="submit" class="btn btn-block btn-lg btn-primary">Sign up!</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
```

## List를 활용한 Footer

기본 목록 그룹을 만들려면 .list-group 클래스가있는 ul 와 .list-group-item 클래스가있는 li 를 사용합니다. 

간단히 말해 리스트 아이템인 li 태그 그룹을 ul 태그로 묶는 것입니다.
```
  <!-- Footer -->
  <footer class="footer bg-light">
    <div class="container">
        <div class="row">
            <div class="col-lg-6 h-100 text-center text-lg-left my-auto">
                <ul class="list-group mb-2 list-group-horizontal">
                    <li list-inline-item><a href="#">About</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Contact</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Terms of Use</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Privacy Policy</a></li>
                </ul>
                <p class="text-muted small mb-4 mb-lg-0">© Your Website 2020. All Rights Reserved.<p>
            </div>
            <div class="col-lg-6 h-100 text-center text-lg-right my-auto">
                <ul class="list-inline mb-0">
                </ul>
            </div>
        </div>
    </div>
  </footer>
```

# Bootstrap을 활용한 UI 제작 프로젝트 전체 코드
```
<!DOCTYPE html>
<html lang="en">

<head>

  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="author" content="">

  <title>Landing Page - Start Bootstrap Theme</title>

  <!-- Bootstrap core CSS -->
  <link href="vendor/bootstrap/bootstrap.min.css" rel="stylesheet">

  <!-- Custom fonts for this template -->
  <link href="vendor/fontawesome-free/css/all.min.css" rel="stylesheet">
  <link href="vendor/simple-line-icons/css/simple-line-icons.css" rel="stylesheet" type="text/css">
  <link href="https://fonts.googleapis.com/css?family=Lato:300,400,700,300italic,400italic,700italic" rel="stylesheet" type="text/css">

  <!-- Custom styles for this template -->
  <link href="css/landing-page.min.css" rel="stylesheet">

</head>

<body>

  <!-- Navigation -->
  <nav class="navbar navbar-light bg-light static-top">
    <div class="container">
      <a class="navbar-brand" href="#">Start Bootstrap</a>
      <a class="btn btn-primary" href="#">Sign In</a>
    </div>
  </nav>

  <!-- Masthead -->
  <header class="masthead text-white text-center">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-xl-9 mx-auto">
          <h1 class="mb-5">Build a landing page for your business or project and generate more leads!</h1>
        </div>
        <div class="col-md-10 col-lg-8 col-xl-7 mx-auto">
          <form>
            <div class="form-row">
              <div class="col-12 col-md-9 mb-2 mb-md-0">
                <input type="email" class="form-control form-control-lg" placeholder="Enter your email...">
              </div>
              <div class="col-12 col-md-3">
                <button type="submit" class="btn btn-block btn-lg btn-primary">Sign up!</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </header>

  <!-- Icons Grid -->
  <section class="features-icons bg-light text-center">
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <div class="features-icons-item mx-auto mb-5 mb-lg-0 mb-lg-3">
            <div class="features-icons-icon d-flex">
              <i class="icon-screen-desktop m-auto text-primary"></i>
            </div>
            <h3>Fully Responsive</h3>
            <p class="lead mb-0">This theme will look great on any device, no matter the size!</p>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="features-icons-item mx-auto mb-5 mb-lg-0 mb-lg-3">
            <div class="features-icons-icon d-flex">
              <i class="icon-layers m-auto text-primary"></i>
            </div>
            <h3>Bootstrap 4 Ready</h3>
            <p class="lead mb-0">Featuring the latest build of the new Bootstrap 4 framework!</p>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="features-icons-item mx-auto mb-0 mb-lg-3">
            <div class="features-icons-icon d-flex">
              <i class="icon-check m-auto text-primary"></i>
            </div>
            <h3>Easy to Use</h3>
            <p class="lead mb-0">Ready to use with your own content, or customize the source files!</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Image Showcases -->
  <section class="showcase">
    <div class="container-fluid p-0">
      <div class="row no-gutters">

        <div class="col-lg-6 order-lg-2 text-white showcase-img" style="background-image: url('img/bg-showcase-1.jpg');"></div>
        <div class="col-lg-6 order-lg-1 my-auto showcase-text">
          <h2>Fully Responsive Design</h2>
          <p class="lead mb-0">When you use a theme created by Start Bootstrap, you know that the theme will look great on any device, whether it's a phone, tablet, or desktop the page will behave responsively!</p>
        </div>
      </div>
      <div class="row no-gutters">
        <div class="col-lg-6 text-white showcase-img" style="background-image: url('img/bg-showcase-2.jpg');"></div>
        <div class="col-lg-6 my-auto showcase-text">
          <h2>Updated For Bootstrap 4</h2>
          <p class="lead mb-0">Newly improved, and full of great utility classes, Bootstrap 4 is leading the way in mobile responsive web development! All of the themes on Start Bootstrap are now using Bootstrap 4!</p>
        </div>
      </div>
      <div class="row no-gutters">
        <div class="col-lg-6 order-lg-2 text-white showcase-img" style="background-image: url('img/bg-showcase-3.jpg');"></div>
        <div class="col-lg-6 order-lg-1 my-auto showcase-text">
          <h2>Easy to Use &amp; Customize</h2>
          <p class="lead mb-0">Landing Page is just HTML and CSS with a splash of SCSS for users who demand some deeper customization options. Out of the box, just add your content and images, and your new landing page will be ready to go!</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Testimonials -->
  <section class="testimonials text-center bg-light">
    <div class="container">
      <h2 class="mb-5">What people are saying...</h2>
      <div class="row">
        <div class="col-lg-4">
          <div class="testimonial-item mx-auto mb-5 mb-lg-0">
            <img class="img-fluid rounded-circle mb-3" src="img/testimonials-1.jpg" alt="">
            <h5>Margaret E.</h5>
            <p class="font-weight-light mb-0">"This is fantastic! Thanks so much guys!"</p>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="testimonial-item mx-auto mb-5 mb-lg-0">
            <img class="img-fluid rounded-circle mb-3" src="img/testimonials-2.jpg" alt="">
            <h5>Fred S.</h5>
            <p class="font-weight-light mb-0">"Bootstrap is amazing. I've been using it to create lots of super nice landing pages."</p>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="testimonial-item mx-auto mb-5 mb-lg-0">
            <img class="img-fluid rounded-circle mb-3" src="img/testimonials-3.jpg" alt="">
            <h5>Sarah W.</h5>
            <p class="font-weight-light mb-0">"Thanks so much for making these free resources available to us!"</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Call to Action -->
  <section class="call-to-action text-white text-center">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-xl-9 mx-auto">
          <h2 class="mb-4">Ready to get started? Sign up now!</h2>
        </div>
        <div class="col-md-10 col-lg-8 col-xl-7 mx-auto">
          <form>
            <div class="form-row">
              <div class="col-12 col-md-9 mb-2 mb-md-0">
                <input type="email" class="form-control form-control-lg" placeholder="Enter your email...">
              </div>
              <div class="col-12 col-md-3">
                <button type="submit" class="btn btn-block btn-lg btn-primary">Sign up!</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer class="footer bg-light">
    <div class="container">
        <div class="row">
            <div class="col-lg-6 h-100 text-center text-lg-left my-auto">
                <ul class="list-group mb-2 list-group-horizontal">
                    <li list-inline-item><a href="#">About</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Contact</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Terms of Use</a></li>
                    <li list-inline-item><a href="#"> ⋅ </a></li>
                    <li list-inline-item><a href="#">Privacy Policy</a></li>
                </ul>
                <p class="text-muted small mb-4 mb-lg-0">© Your Website 2020. All Rights Reserved.<p>
            </div>
            <div class="col-lg-6 h-100 text-center text-lg-right my-auto">
                <ul class="list-inline mb-0">
                </ul>
            </div>
        </div>
    </div>
  </footer>

  <!-- Bootstrap core JavaScript -->
  <script src="vendor/jquery/jquery.min.js"></script>
  <script src="vendor/bootstrap/bootstrap.bundle.min.js"></script>

</body>

</html>

```








