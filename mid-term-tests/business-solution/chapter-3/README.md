# 지연 메서드 사용하는 이유

여기서 나오는 지연메서드는 두가지로 범위를 분류할수 있을것 같다.

1. 책에서 나오는 지연메서드의 이유
2. 실무에서 쓰이는 지연메서드의 이유

일단 2 번부터 설명하는것이 좀더 이해에 도움이 되므로, (혹은 좀더 포괄적이므로) 2 번부터 설명을 시작하겠다.

### 실무에서 쓰이는 지연메서드의 이유

예를 들어보자, 내가 메모를 작성하는 앱을 쓰고 있는데, 메모를 작성하고 저장하려면 확인 버튼을 눌러야 한다고 가정하자.
근데 나는 성격이 좀 급해서 확인버튼을 여러번 누르는 것이 습관이라고 가정한다면, 만약 작성을 하고 여러번 누르는 것이 모두 입력되는 식으로 앱이 만들어 졌다면 어떨까?
생각만 해도 끔찍한 일이 벌어진다. 같은 노트가 여러번 저장이 될뿐더러, 그것을 처리하는 서버의 트래픽 (서버를 거친다면) 이 증가하게 되어, 자연스레 렉이 걸리게 될것이다.

이럴 때 사용하는것이 지연 메서드 이다.
뭐 UI 측면에서 지연을 시키는 것이 가장 일반적인 방법일것이다. 메모를 등록하기 위한 확인 버튼을 한번 눌렀을때 Disabled 로 만들어서 두번째부터는 입력이 먹지 않게 하는것이 가장 쉬운 방법일 것이다.

만약 이렇게 UI 를 거치지 않는 형식이라면 어떨까? 바로 API 요청을 실시하는 방식이라고 가정해보자.
이 가정이 바로 1 번경우를 설명할수 있을것이다.

### 책에서 나오는 지연메서드의 이유

위와같은 가정에서, API 를 여러번 호출할수 있을것이다. 컴퓨터 사양만 좋다면 매크로 같은것을 돌려서 1 초에 몇백 혹은 몇천번도 날릴수 있지 않을까 싶다. 이렇게 되면 OpenAPI 를 제공하는 서버 측에서는 과부하가 걸리게된다. 매우좋지 않은, 있어서는 안될 현상이다.
이럴때 사용자를 구분할수 있는 Key 혹은 특정 flag 를 만들어서 여러번 요청하지 못하게 하는 방법이 있을것이다. 혹은 한번 요청한 후, 바로 일정시간의 지연을 두는 것이다. 이러한 지연을 둠으로써 불필요한 API 요청 트래픽을 막을수 있다.
