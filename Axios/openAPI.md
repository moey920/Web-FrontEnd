# API

OpenAPI에 대해 알아보기 전에 API에 대해 먼저 알아봅시다. API는 **Application Programming Interface**의 줄임말로 **다양한 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스**를 말합니다.

만약 여러분이 밥을 먹기 위해 식당을 갔다고 해봅시다. 손님인 여러분은 요리사에게 음식 주문을 해야 밥을 먹을 수 있습니다. 하지만 직접 요리사에게 말하지는 않죠. 일반적인 경우 점원을 통해 주문을 할 텐데요. 이때 점원 역할이 바로 API라고 생각하시면 됩니다. 즉, 프로그램과 프로그램을 연결해 주는 다리 역할을 하는 것이 API입니다.

## OpenAPI

그렇다면 OpenAPI는 무엇인지 알아보겠습니다. OpenAPI(Open Application Programming Interface, Open API, 공개 API)는 누구나 사용할 수 있도록 공개되어 개발자에게 사유 응용 소프트웨어나 웹 서비스에 프로그래밍적인 권한을 제공하는 API입니다. 말 그대로 누구에게나 공개된 API가 OpenAPI입니다.

즉, 누구나 음식점에 들어와서 주문을 하고 음식을 먹을 수 있다는 의미입니다! OpenAPI의 예시로는 국가에서 제공하는 데이터인 공공데이터 포털 또는 네이버의 데이터 등 다양하게 있습니다.

### OpenAPI를 사용하는 이유

위의 예시에 등장한 것처럼 다양한 OpenAPI들이 있습니다. 이러한 데이터들로 자신만의 서비스를 만들고 싶다면 OpenAPI를 활용해야 합니다. OpenAPI를 이용하여 개발하는 방법은 어느 정도 획일화되어 있기 때문에 다른 사람들과 협업하기가 편리합니다. 

또한 코드를 작성하는 시간이 절약되어 개발 비용이 절감되는 장점이 있습니다. OpenAPI를 사용하지 않고 스스로 모든 풀스택 개발을 하는 것은 정말 어렵습니다. 또한 OpenAPI를 사용하면 API 테스트를 통한 품질 보장이 가능하고 사용자와의 상호작용을 중요시하는 서비스를 개발할 수 있습니다.

### OpenAPI를 제공하는 이유

이번에는 기업들이 왜 OpenAPI를 제공하는지 알아보겠습니다. 기업들은 다양한 서비스나 기술을 제공하지만 사용자가 원하는 모든 것을 충족하기는 것은 쉽지 않습니다. 따라서 기업들은 OpenAPI를 고객들에게 제공함으로써 사용자가 기업의 서비스나 기술을 유연하게 이용할 수 있도록 합니다. 즉, **고객이 자신의 요구에 적합한 방식으로 서비스를 이용할 수 있다는 것을 의미하며 기업은 고객과의 관계를 강화**할 수 있게 됩니다.

이렇게 고객이 원하는 방식으로 만들어진 인터페이스는 다른 사람들에게도 공유됩니다. 공유된 방식은 좀 더 확장되어 API를 제공한 기업에서 자사의 서비스에 통합할 수 있습니다. 개발자들이 기업의 API를 연구하고 통찰하여 새로운 서비스를 만들어내면, 기업은 그것을 참고하여 고객이 진정으로 원하는 서비스가 무엇인지 더 고민할 수 있는 계기가 됩니다.

### 애플리케이션 등록

네이버에서 제공하는 OpenAPI를 사용하기 위해 애플리케이션 등록을 진행하는 방법을 알아보겠습니다. 네이버 OpenAPI를 이용하기 위해서는 네이버에 로그인이 필요합니다. 아래 순서에 따라 애플리케이션 등록을 진행해봅시다. 자세한 설명은 링크에도 소개되어 있으니 참고 바랍니다!

1. 링크<https://developers.naver.com/apps/#/register?defaultScope=search>에 접속합니다.
2. 해당 화면에서 애플리케이션 이름은 자유롭게 채워주세요. 그리고 사용 API에는 검색을 선택하고 비로그인 오픈 API 서비스 환경에는 http://localhost를 입력하세요.

- 애플리케이션 이름: 자신이 신청한 OpenAPI의 이름입니다.
- 사용 API: 사용할 OpenAPI를 선택합니다. 앞으로의 실습에서는 검색 API를 활용할 것이기 때문에 검색을 선택해줍니다.
- 비로그인 오픈 API 서비스 환경: 네이버 OpenAPI에 로그인을 하고 사용해야 하는 것과 그렇지 않은 것이 있는데, 비로그인 환경에서 사용할 도메인 주소를 입력합니다. 일반적으로 http://localhost를 입력해주면 됩니다.

3. 애플리케이션 등록이 완료되면 아래와 같은 Client ID와 Client Secret을 얻을 수 있습니다. 해당 키를 가지고 OpenAPI에 접근할 수 있습니다. 부여되는 키는 개인의 것이므로 공유되지 않도록 유의해야 합니다.

- Client ID: OpenAPI 사용에 대한 인증 및 권한 부여에 사용되는 사용자의 ID입니다.
- Client Secret: OpenAPI 사용에 대한 인증 및 권한 부여에 사용되는 사용자의 비밀번호입니다.

> API를 호출할 수 있는 횟수가 일별로 제한되어 있음을 참고 바랍니다. 더불어 네이버 OpenAPI 외에도 다양한 OpenAPI가 존재하기 때문에 이번에 익힌 사용법을 바탕으로 구현하고 싶은 기능에 맞는 데이터를 찾아 사용하면 됩니다!


#### Postman

앞서 생성한 OpenAPI 애플리케이션이 잘 생성되었는지 Postman을 이용해서 확인해봅시다. Postman은 API를 테스트하기 위한 도구로 사용되며, 링크에서 다운로드를 받을 수 있으며 크롬 확장 프로그램으로 설치하여 이용할 수도 있습니다. Postman 설치 후 아래 과정에 따라 API 테스트를 진행해봅시다.

##### API 테스트

1. Collections를 선택한 후 + 버튼을 눌러 새로운 Collection을 만드세요.

2. Collection의 이름을 자유롭게 설정한 후 Add a request를 클릭하여 새로운 request를 만드세요.

3. HTTP 요청 상태를 GET으로 설정하고 API 주소 https://openapi.naver.com/v1/search/shop를 입력하세요. 그리고 ?query=컴퓨터와 같은 형태로 검색하고 싶은 단어를 넘겨주시면 됩니다. Params에 KEY와 VALUE 값을 직접 입력해도 괜찮습니다! 즉, query에 입력된 것이 검색어입니다. 다른 요청 변수에 대한 설명은 링크를 참조하시면 됩니다.

4. 다음으로 Headers에서 OpenAPI를 생성했을 때 받은 키를 넘겨줍니다. KEY X-Naver-Client-Id에 VALUE는 생성한 애플리케이션에서 얻은 Client ID를 넘겨주고, KEY X-Naver-Client-Secret에 VALUE는 생성한 애플리케이션에서 얻은 Client Secret을 넘겨줍니다.

5. 마지막으로 Send 버튼을 클릭하고 요청 결과를 확인하세요!

6. GET 이외의 요청 : 
만약 GET 이외의 다른 API 요청을 하고 싶으면 아래 사진처럼 GET 이외에 다른 요청으로 설정해주면 됩니다. 단, 요청을 할 API가 다른 요청을 허용하는지 확인해야 합니다!