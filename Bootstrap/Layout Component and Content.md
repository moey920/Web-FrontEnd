# 레이아웃 컴포넌트 및 컨텐츠

부트스트랩 컴포넌트, 객체 및 컨텐츠 활용 방법에 대해 배우고 적용할 수 있습니다.

## Bootstrap의 Card

Card 개념
카드는 부트스트랩이 지원하는 유연하고 확장 가능한 콘텐츠 컨테이너입니다. 여기에는 머리글 및 바닥 글 옵션, 다양한 콘텐츠, 상황 별 배경색 및 강력한 표시 옵션이 포함됩니다.

예시)
image

지시사항
App.js 파일 내 App 클래스 내 card를 만드는 코드를 아래처럼 추가하세요.
 <div class="card">
  <img class="card-img-top" src='rabbit04.png' alt="elice"/>

  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="/" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
