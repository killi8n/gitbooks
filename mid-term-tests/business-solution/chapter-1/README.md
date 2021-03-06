# OpenAPI 란 무엇인가?

> ### 먼저 나의 생각을 써보자.

OpenAPI 라면, 쉽게 말해서 구글에서 제공하는 구글 맵을 예시로 들수 있을것 같다.
구글도 구글맵 Application 을 개발하면서 처음부터 모든 API 를 제공하지는 않았을것이다.
허나, 사용자들의 편리에 의해서 API 를 제공하였을 것이다. 이것이 바로 Open API 이지 않을까?
쉽게말해 개발한 API 를 Open 시킨 것이다.
<br />

> ### 이렇게 되면 무슨 현상이 일어날까..?

쉽게 말해서 구글과 같은 대기업의 기술력을 내가 갖다가 무료 혹은 유료로 쓸수 있는 것이다.
나와 같은 학생 개발자 혹은 1 인 개발자들이 어떻게 지도 길찾기 서비스를 제공하겠는가..? 절대 네버 할수 없을것이라고 생각한다.
그러나 이런 구글 Map API 를 사용하므로써, 길찾기 기능을 제공할수 있게 되는것이다.
또한, 다른 견해로써는 데이터 제공의 측면에서 볼수 있을것 같다.

> ### 개발자 관점의 API

개발자의 관점에서 API 라면, 서버, 즉 백엔드에서 제공하는 API 가 가장 먼저 떠오른다. (내입장에서.)
<br />
먼저 API 는 무슨 약자인가에 대해 알아보면, Application Programming Interface 라고 나와있다.
어플리케이션 (소프트웨어) 프로그래밍 인터페이스.. 어렵군, 뭐 상용하는 소프트웨어의 프로그래밍 인터페이스 혹은 도구? 정도로 직역할수 있을것 같다.
실무적으로 다가간다면, 서버가 제 역할을 하려면 그 기능을 수행해야 서버다. 그렇다면 여기서 나오는 그 기능이 API 라고 할수 있다.
내가 만약 애니메이션 스트리밍을 하는 서비스를 제공하는 웹을 개발한다고 치자. 그렇다면 애니메이션에도 카테고리들이 있을것이고, 그 카테고리별로 개개의 애니메이션 정보들이 있을것이다. 이렇게 카테고리별로 데이터를 전달해주고, 그 애니메이션을 하나 클릭했을 때, 특정 애니메이션에 대한 정보들을 제공해 주는것이 모두 API 통신을 통해 이루어진다. (정적페이지가 아니라면..)

뭐 이정도로 내가 가지고 있는 API 에 대한 개념들을 나열할수 있을것 같다. 그렇다면 사전적 지식에 대해 한번 알아보자.

> ### 사전적 의미

> 오픈 API(Open Application Programming Interface, Open API, 공개 API)는 누구나 사용할 수 있도록 공개된 API 를 말하며, 개발자에게 사유 응용 소프트웨어나 웹 서비스에 프로그래밍적인 권한을 제공한다.

> 오픈스트리트맵의 오픈 API 는 무료이지만 구글은 단계적인 유료화를 통해 2018 년 구글 맵스 API 를 무료사용권 제도를 사용한 전면 유료화 방침을 확정했다. 이처럼 공개된 오픈 API 일지라도 데이타 사용 용량에 따라 비용을 지불해야 하는 경우가 있거나 완전히 무료일지라도 사용자가 회원가입을 통한 신원확인후 서비스제공자로부터 공개키(또는 사용권한 토큰)을 별도로 발급받아 오픈 API 를 사용토록 장려함으로서 무분별한 데이터 남용을 막는 사례가 늘고 있다.
> <br />
> 출처: [https://ko.wikipedia.org/wiki/%EC%98%A4%ED%94%88_API]

맞다. 요즘에는 토큰을 사용하여 Open API 를 제공하지.. 뭐 이유는 간단하다, 위에서도 나와있듯이 무분별한 API 통신을 막기 위해서이다.
Unsplash 라는 사진 제공 웹 서비스가 있는데, 이쪽 API 를 사용해서 사진 정보들을 가져올수 있는데, 이것도 무료로 사용하기 위해서는 따로 앱을 등록시켜야 하며, 등록후에도 무료는 1 시간당 50 번의 요청만 가능하게 되어있다. 요청시에는 무조건 AppID 와 SecretID 를 사용하여야 한다.

이런식으로 Token 혹은 Key 를 이용하여 요즘에는 무분별한 OpenAPI 호출 방지를 하고있다.
