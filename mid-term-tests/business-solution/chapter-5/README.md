# UNSAFE CODE / 안전하지 않은 코드 허용의 의미 ?

안전하지 않은 코드를 설정하게 되면 다음이 가능하다.

- 배열 범위를 검사하지 않아서 성능은 향상되고 신뢰성은 떨어질 수 있다.

- 네이티브 어셈블리를 사용하는 경우 필요하다.

- unsafe 한 코드를 포함하고 있는 인스턴스는 fixed 로 고정시키지 않으면 gc 에 의해 인스턴스의 할당 위치가 바뀌면서 unsafe 한 형식의 내용이 엉뚱하게 되어 버릴 수 있다.

- unsafe 한 코드를 포함하고 있는 형식에는 소멸자를 정의를 하여 gc 에 의해 수집되기전에 unsafe 한 형식 인스턴스에 대한 자원 해제를 하지 않으면 메모리 누수가 생길수 있다.

- 소스 및 대상 배열의 메모리 내 위치가 고정되어 가비지 수집에 의해 이동하지 않는다.

> 안전하지 않은 코드

C# 프로그래밍 언어는 기본적으로 포인터를 다루게 하지 않는다. 안전하지 않은 컨텍스트를 정의하거나 포인터를 사용하는 코드를 쓰려면 unsafe 키워드를 사용해야 한다. 안전하지 않은 코드는 CLR 의 실행 환경을 실행할때에 다루어 지지않는 코드들을 쓸수 있게 한다.

그렇다면 unsafe code 란 무엇인가?

안전하지 않은 코드를 사용하게 되면 CLR 으로 코드의 안정성을 보장할수 없다. 다시말해, 안전하지 않거나 관리되지 않은 코드는 CLR 의 컨텍스트 범위 밖에서 실행된다. 안전하지 않은 코드는 포인터를 사용하는 네이티브 함수를 사용하게 한다. 따라서 안전하지 않은 코드를 사용할때에는 프로그램이 어떠한 보안적 위험이나, 메모리 누수와 같은 사항을 나타나지 않게 보장해야 한다. 안전하지 않은 코드를 쓰기 위해서, unsafe 키워드를 사용해야 한다. unsafe 키워드를 사용하여 메서드, 타입 그리고 코드 블럭들을 정의할수 있다.

포인터

포인터는 다른 변수의 주소를 나타내는 변수이다. 다시말해, 포인터는 다른 변수의 메모리 주소나 메모리의 위치를 가지고 있다.
데이터 타입의 포인터는 가리키는 변수의 데이터 타입과 동일해야 한다. 인티저 형식의 변수를 가리키는 포인터는 인티저 형식이어야 한다.
다음과 같은 3 가지의 연산자를 사용하여 포인터를 사용할 것이다.

\*
&
->

다음 코드는 포인터를 정의하고 포인터가 변수의 주소를 가리키게 하는 코드이다.

```C
int i = 100;
int *ptr = & i;
```

위의 코드를 살펴보면, i 라는 변수에 100 을 할당 시킨다. 다음으로, integer 포인터를 정의하고 & 연산자를 사용하여 주소를 가리키게 한다.

아래의 코드는 unsafe 키워드를 사용하여 변수의 메모리 주소를 보여주게하는 코드이다.

```C
static void Main(string[] args)
{
    unsafe
    {
        int i = 100;
        // 변수 할당

        int* ptr = &i;
        // integer 포인터를 만들어 int 변수의 주소를 가리킨다.

        Console.WriteLine("The value of i is : " + i);
        // The value of i is : 100

        Console.WriteLine("The memory address of i is : " + (int)ptr);
        // The memory address of i is : int형으로 변환된 주소
    }
    Console.ReadKey();
}
```

만약 unsafe 를 빠뜨리고 위의 코드를 빌드시킨다면 다음과 같은 에러를 볼수 있을것이다.

"포인터는 안전하지 않은 컨텍스트에서만 사용 할 수 있습니다."

위의 에러는 안전하지 않은 코드는 무조건 unsafe context 범위 내에서만 써야 한다는 이야기를 해주고있다.
-- unsafe 가 하는 일이다.

만약 unsafe 한 코드를 빌드하고 컴파일 하기 위해 Visual Studio 를 사용한다면, 다음과 같은 스텝을 진행하여 unsafe 코드를 허용해주어야 한다.

- Project 를 우클릭한다.
- 프로젝트 속성 창에서 빌드 탭을 누른다.
- 안전하지 않은 코드 허용에 체크한다.

또한, 아래와 같은 csc 커맨드 라인 컴파일러를 사용하여 안전하지 않은 코드를 포함하고 있는 프로그램을 컴파일 시킬수 있다.

```bash
csc /unsafe myprogram.cs
```

위의 프로그램이 실행되면 i 의 값과, 주소를 볼수 있을것이다.

또한, 메서드를 unsafe 를 사용하여 표시할수 있다. 아래의 코드는 그 예제 이다.

```c
public unsafe void Compute(int* ptr)
{
    *ptr = (*ptr) * 10;
}
```

그리고 아래와 같이 Compute 함수를 사용할수 있다.

```c
unsafe {
    int i = 100;

    int* ptr = &i;

    Compute(&i);

    Console.WriteLine("The value of the variable i is : " + i);
}
```

위의 코드를 실행하면, i 변수의 값이 100 에서 1000 으로 바뀌는 것을 볼수있다. Compute 메서드가 포인터를 인자로 받아 포인터가 가리키는 주소의 변수를 10 배 곱해준다. \*ptr 은 ptr 포인터가 가르키는 주소의 변수의 값이다. (당시 100 을 가지고 있다.). 이 값은 10 배 곱해져서 결과로 나타나게 된다.

만약 안전하지 않은 코드를 managed environment 에서 사용 할시, 이론적으로 메모리를 변수에 위치시키기 위해 fixed 키워드를 사용하여야 한다.
그렇게 해야 런타임이 heap fragmentation 때문에 메모리를 compacting 하는 동안 변수를 움직이지 않게 할수 있다.

기본적으로, fixed 키워드를 사용하여 불가능한 포인터 문제와 연관된 이슈들을 해결할수 있다. 또한 fixed 키워드를 사용하여 배열을 고정할수 있으며 포인터를 배열 형식의 데이터에 할당할수 있다.

fixed 키워드를 사용해야 포인터를 설정하고 해당 코드를 실행하는동안 해당 변수를 고정한다.
fixed 키워드가 없다면 가비지 수집에서 예기치 않게 변수를 재배치 할 가능성이 있다.

unsafe 키워드를 사용한다면 가비지 수집을 하지 않아 고정할 필요가 없는 스택에서 메모리를 할당할 수 있다.
