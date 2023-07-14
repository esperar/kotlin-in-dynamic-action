# 함수, 변수, 클래스, enum, 프로퍼티를 선언하는 방법

## 기본 요소: 함수와 변수

### Hello World

이제는 고전이 된 예제인 Hello World를 찍는 프로그램으로 싲가을 해본다.

```kt
fun main(args: Array<String>) {
    println("Hello World")
}
```

이렇게 간단한 코드에서 어떤 코틀린 문법이나 특성을 발견할 수 있을까?

- 함수를 선언할 때 `fun` 키워드를 사용한다. 실제로 코틀린에서 함수를 만드는 일은 신나는(fun)일이다.

- 파라미터 이름 뒤에 그 파라미터 타입을 작성한다.
- 함수를 최상위 수준에 정의할 수 있다. (자바와 달리 꼭 클래스 안에 함수를 넣어야 할 필요가 없다.)
- 배열도 일반적인 클래스와 마찬가지다. 코틀린에는 자바와 달리 배열 처리를 위한 문법이 따로 존재하지 않는다.
- System.out.println 대신에 println이라고 쓴다. (코틀린의 표준 라이브러리는 여러 가지 표준 자바 라이브러리 함수를 간결하게 사용할 수 있게 감싼 래퍼wrapper를 제공한다.)
- 최신 프로그래밍 언어 경향과 마찬가지로 줄 끝에 새미콜론을 붙이지 않아도 된다.

<br>

### 함수

코틀린에서 함수를 작성할 때 반환 타입을 어디에 지정해야 할 까?

```kt
fun max(a: Int, b: Int): Int {
    return if (a > b) a else b
}

fun main() {
    println(max(1,2)) // 2
}
```

함수 선언은 fun 키워드로 시작하고, fun 다음에는 함수 이름이 온다.
  
함수 이름 뒤에는 괄호 괄호 안에는 파라미터 목록이 오고, 함수의 반환 타입은 파라미터 목록의 다는 괄호 다음에 오는데 괄호와 반환 타입 사이에 콜론(:)이 있다.
  
코틀린은 if는(값을 만들어내지 못하는) 문장이 아니고 결과를 만드는 식(expression)이라는 점이 흥미롭다.
  
이 예제의 코틀린 if 식은 자바 3항 연산자로 작성한 (a > b) ? a : b 식과 비슷하다.

<br>

### 문(statement)와 식(expression)의 구분

- 문(statement)
  - 문은 자신을 둘러싸고 있는 가장 안쪽 블록의 최상위 요소로 존재하며 아무런 값을 만들어내지 않는다.
- 식(expression)
  - 식은 값을 만들어 내며 다른 식의 하위 요소로 계산에 참여할 수 있다.

<br>

### 식이 본문인 함수

방금 작성한 max 함수는 return대신 = 하나로만 표현할 수 있다.

```kt
fun max(a: Int, b: Int): Int = if (a > b) a else b
```

본문이 중괄호로 둘러싸인 함수를 **블록이 본문인 함수**라고 부르고, 등호와 식으로 이뤄진 함수를 **식이 본문인 함수**라고 부른다.
  
반환 타입을 생략하면 max 함수를 더욱 간략하게 만들 수 있다.

```kt
fun max(a: Int, b: Int) = if (a > b) a else b
```

여기서 반환 타입을 생략할 수 있는 이유는?   
  
코틀린은 정적 타입 지정 언어이므로 컴파일 시점에 모든 식의 타입을 지정해야 한다.
  
실제로 모든 변수나 모든 식에는 타입이 있으며, 모든 함수는 반환 타입이 정해여쟈 한다. 
  
하지만 식이 본문인 함수의 경우 굳이 사용자가 반환 타입을 적지 않아도 컴파일러가 함수 본문 식을 분석해 식의 결과 타입을 함수 반환 타입으로 정해준다.   
`타입 추론`
  
그러나 블록이 본문인 함수가 값을 반환한다면 반드시 반환 타입을 지정하고 return 문을 사용해야한다.

<br>

### 변수
자바에서 변수를 선언할 때 타입이 맨 앞에 온다. 코틀린에서는 타입 지정을 생략하는 경우가 흔하다.
  
타입으로 변수 선언을 시작하면 타입을 생략할 경우 변수 선언을 구별할 수 없다.
  
그런 이유로 코틀린에서는 키워드로 변수 선언을 시작하는 대신 변수 이름 뒤에 타입을 명시하거나 생략하게 허용한다.

```kt
val question = "삶, 우주, 그리고 모든 것에 대한 궁극적인 질문"
val answer: Int = 42
```

식이 본문인 함수와 마찬가지로 여러분이 타입을 지정하지 않으면 컴파일러가 초기화 식을 분석해서 초기화 식의 타입을 변수 타입으로 지정한다.
  
초기화 식이 없다면 변수에 저장될 값에 대해 아무 정보가 없기 때문에 컴파일러가 타입을 추론할 수 없다. 따라서 그런 경우 타입을 반드시 지정해야 한다.

```kt
val answer: Int
answer = 42
```

<br>

### 변경 가능한 변수와 변경 불가능한 변수

변수 선언 시 사용하는 키워드는 `val`, `var` 다음과 같이 2가지가 있다.

```kt
val a = 3 // 값 변경이 불가능한 참조를 저장하는 변수 
var b = 4 // 값 변경이 가능한 참조, 변수의 값은 바뀔 수 있다.
```

val 변수의 초기화는 무조건 한 번만 초기화 돼야한다.
  
하지만 어떤 블록에 실행될 때 오직 한 초기화 문장만 실행됨을 컴파일러가 확인할 수 있다면 조건에 따라 val 값을 다른 여러 값으로 초기화할 수도 있다.

```kt
val message: String

if(canPerformOperation()) {
    message = "Success"
    // .. 연산을 수행
} else {
    message = "Failed
}
```

val 키워드는 참조 자체는 불변이라도 그 참조가 가리키는 객체의 내부 값은 변경될 수 있다는 사실을 기억하자.

```kt
val languages = arrayListOf("Java") // 불변 참조를 선언한다.
languages.add("Kotlin") // 참조가 가리키는 객체 내부를 변경한다.
```

### 더 쉽게 문자열 형식 지정: 문자열 템플릿

```kt
fun main(args: Array<String>) {
    val name = if (args.,size > 0) args[0] else "Kotlin"
    println("Hello, $name!")
}
```

이 예제는 문자열 템플릿이라는 기능을 보여준다. 이 코드는 name이라는 변수를 선언하고 그 다음 줄에 있는 문자열 리터럴 안에서 그 변수를 사용했다.
  
여러 스크립트 언어와 비슷하게 코틀린에서도 변수를 문자열 안에 사용할 수 있다.
  
문자열 리터럴의 필요한 곳에 변수를 넣되 변수 앞에 &를 추가해야 한다.

```kt
fun main(args: Array<String>) {
    val name = if (args.,size > 0) args[0] else "Kotlin"
    println("Hello, ${args[0]}!")
}
```

<br>

## 클래스와 프로퍼티

시작하기 위해 간단한 자바빈 클래스인 Person을 정의하자

```java
public class Person {

    private final String name;

    public Person(String name ){
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

필드가 둘 이상으로 늘어나면 생성자인 Person의 본문에서 파라미터 이름이 같은 필드에 대입하는 대입문의 수도 늘어난다.
  
코틀린에서는 그런 필드 대입 로직을 훨씬 더 적은 코드로 작성할 수 있다.

```kt
class Person(val name: String)
```

멋지다. 다른 최신 JVM 언어에서 이와 비슷한 클래스 정의를 이미 본 독자도 있을 것이다.
  
이런 유형의 클래스를 값 객체라 부르며 다양한 언어가 값 객체를 간결하게 기술할 수 있는 구문을 제공한다.
  
> public 가시성 변경자가 사라졌음을 확인하라. 코틀린의 기본 가시성 public이므로 이런 경우 변경자를 생략해도 된다.

<br>

### 프로퍼티

클래스라는 개념의 목적은 데이터를 캡슐화하고 캡슐화한 데이터를 다루는 코드를 한 주체 아래 가두는 것이다.
  
자바에서는 데이터를 필드에 저장하며, 멤버 필드의 가시성을 보통 비공개다.
  
클래스는 자신을 사용하는 클라이언트가 그 데이터를 읽기 위한 게터를 제공하고 필드를 변경하게 허용해야할 경우 세터를 추가 제공할 수도 있다.
  
이런 예를 Person 클래스에서도 볼 수 있다.
  
세터는 자신이 받은 값을 검증하거나 필드 변경을 다른 곳에 통지하는 등의 로직을 더 가질 수 있다.
  
자바에서는 필드와 접근자를 한데 묶어 프로퍼티라고 부르며 프로퍼티라는 개념을 활용하는 프레임워크가 많다.
  
코틀린은 프로퍼티 언어 기비본 기능을 제공하며, 코틀린 프로퍼티는 자바의 필드와 접근자 메서드를 완전히 대신한다.
  
클래스에서 프로퍼티를 선언할 때는 앞에서 살펴본 변수를 선언하는 방법과 마찬가지로 var, var를 사용한다.

```kt
class Person(
    val name: String, // 읽기 전용 프로퍼티로 코틀린은 (비공개) 필드와 필드를 읽는 단순한 (공개) 게터를 만들어낸다.
    var isMarried: Boolean // 쓸 수 잇는 프로퍼티로, 코틀린은 (비공개) 필드, (공개) 게터, (공개) 세터를 만들어낸다.
)
```

기본적으로 코틀린에서 프로퍼티를 선언하는 방식은 프로퍼티와 관련 잇는 접근자를 선언하는 것이다.
  
코틀린은 값을 저장하기 위한 비공개 필드와 그 필드에 값을 저장하기 위한 세터, 필드의 값을 읽기 위한 게터로 이뤄진 간단한 디폴트 접근자 구현을 제공한다.

```kt
val person = Person("Bob", true)
println(person.name) // Bob
```

위에서 알 수 있듯 코틀린에서 객체를 생성할때는 new 키워드를 사용하지 않아도 되며 프로퍼티 이름을 직접 사용해도 코틀린이 자동으로 게터를 호출해준다.

> 자바에서 선언한 클래스에 대해 코틀린 문법을 사용해도 된다.  
> 코틀린에서는 자바 클래스의 게터를 val 프로퍼티처럼 사용할 수 있고, 게터/세터 쌍이 있는 경우에는 var 프로퍼티처럼 사용할 수 있다.  

대부분의 프로퍼티에는 그 프로퍼티의 값을 저장하기 위한 필드가 있다. 이를 ㅍ ㅡ로퍼티를 뒷받침하는 필드라고 부른다.
  
하지만 원한다면 프로퍼티 값을 그때그때 계산할 수도 있다.
  
커스텀 게터를 작성하면 그런 프로퍼티를 만들 수 있다.

<br>

### 커스텀 접근자

직사각형 클래스 Rectangle을 정의하면서 자신이 정사각형인지 알려주는 기능을 만들어보자.
  
직사각형이 정사각형인지를 별도의 필드에 저장할 필요 없다.
  
사각형의 너비와 높이가 같은지 검사하면 정사각형의 여부를 그때그때 알 수 있다.

```kt
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {
            return height == width
        }
}
```

isSqaure에 자체 값을 저장하는 필드가 필요 없고, 이 프로퍼티에는 자체 구현을 제공하는 게터만 존재한다.
  
클라이언트가 프로퍼티에 접근할 때마다 게터가 프로퍼티의 값을 매번 다시 계산한다.

```kt
val rectangle = Rectangle(41, 43)
println(rectangle.isSquare) // false
```

커스텀 게터를 사용하는 방법과 필드를 추가해서 관리하는 방법중에 성능상에 차이는 딱히 없다 가독성의 측면에서만 차이가 난다.

<br>

### 코틀린 소스코드 구조: 디렉터리와 패키지

코틀린에서도 package라는 단위로 소스코드를 구성한다.
  
다른 패키지에서 클래스를 불러오려면 임포트문은 파일의 맨 앞에 와야 하며 import 키워드를 사용해야한다.

```kt
package geometry.shapes

import java.util.Random

class Rectangle(val width: Int, val width: Int) {
    val isSquare: Boolean
        get() = height == width
}

```

코틀린에서 클래스 임포트와 함수 임포트에 차이가 없으며, 모든 선언을 import 키워드로 가져올 수 있다.
  
최상위 함수는 그 이름을 써서 임포트할 수 있다.

```kt
package geometry.example

import geometry.shapes.createRandomRectangle

fun main(args: Array<String>) {
    println(createRandomRectangle().isSquare)
}

```

패키지 이름 뒤에 .*를 추가하면 패키지 안에 모든 선언을 임포트할 수 있다.
  
스타(*) 임포트를 사용하면 패키지 안에 모든 클래스 뿐만 아니라 최상위에 정의된 함수나 프로퍼티까지 모두 불러온다는 점을 유의하자.
  
<br>

## 선택 표현과 처리: enum과 when

### enum 클래스의 정의

enum 클래스를 사용해서 다채로운 색을 추가해보자.

```kt
enum class Color {
    RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```

enum은 자바 선언보다 코틀린 선언에 더 많은 키워드를 써야하는 흔치 않은 예다,
  
코틀린에서는 enum class를 사용하지만 자바에서는 enum을 사용한다.
  
코틀린에서 enum 키워드는 `소프트 키워드`라고 부르는 존재다.
  
enum은 class 앞에 있을 때는 특별한 의미를 지니지만 다른 곳에서는 이름에 사용할 수 있다. 반면 class는 키워드다.
  
따라서 class라는 이름을 사용할 수 없으므로 클래스를 표현하는 변수 등을 정의할 때는 clazz나 aClass와 같은 이름으로 사용해야한다.
  
자바와 마찬가지로 enum 안에서 값만 열거하는 것이 아닌 프로퍼티와 메서드를 정의할 수 있다.

```kt
enum class Color(
    val r: Int, val g: Int, val b: Int
) {
    RED(255, 0, 0), ORANGE(255, 165, 0),
    YELLOW(255,255,0);

    fun rgb() = (r * 256 + g) * 256 + b

}

fun main() {
    println(Color.BLUE.rgb()) // 255
}
```

enum에서도 일반적인 클래스와 마찬가지로 생성자와 프로퍼티를 선언한다.
  
각 enum 상수를 정의할 때는 그 상수에 해당하는 프로퍼티 값을 지정해야만 한다.
  
이 예제에서는 코틀린에서 유일하게 세미콜론이 필수인 부분을 볼 수 있다.
  
enum은 클래스 안에 메서드를 정의하는 경우 반드시 enum 상수 목록과 메서드 정의 사이에 세미콜론을 붙여야한다.

<br>

### when으로 enum 클래스 다루기

무지개의 색을 기억하기 위해 연상법을 적용한 문장을 외우는 아이를 본 적이 있을 것이다.
  
그런 문장의 예로는 "Richard Of York Gave Battle In Vain!"을 들 수 있다,
  
무지개의 각 색에 대해 그와 상응하는 연상 단어를 짝지어주는 함수가 필요하다고 상상해보자.
  
자바라면 switch를 사용해서 그런 함수를 작성할 수 있다.
  
switch에 해당하는 코틀린 구성 요소는 when이다.
  
if와 마찬가지로 when도 값을 만들어내는 식(expression)이다.

```kt

fun getMnemonic(color: Color) =
    when(color) {
        Color.RED -> "Richard"
        Color.ORANGE -> "Of"
        Color.YELLOW -> "York"
        Color.GREEN -> "Gave"
        Color.BLUE -> "Battle"
        Color.INDIGO -> "In"
        Color.VIOLET -> "Vain"
    }

fun main() {
    println(getMnemonic(Color.BLUE))
}
```

앞의 코드는 color로 전달된 값과 같은 분기를 찾는다.
  
자바와 달리 각 분기의 끝에 break를 넣지 않아도 된다.
  
성공적으로 매치되는 분기를 찾으면 switch는 그 분기를 실행한다. 
  
한 분기 안에서 여러 값을 매치 패턴으로 사용할 수도 있다. 그럴 경우 값 사이를 콤마,로 분리한다.

```kt

fun getWarmth(color: Color) =
    when(color) {
        Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
        Color.GREEN -> "neutral"
        Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
    }

fun main() {
    println(getWarmth(Color.BLUE))
}
```

상수값을 임포트하면 더욱 간결하게 사용할 수도 있다.

```kt
import ch02.colors.Color
import ch02.colors.Color.*

fun getWarmth(color: Color) =
    when(color) {
        RED, ORANGE, YELLOW -> "warm"
        GREEN -> "neutral"
        BLUE, INDIGO, VIOLET -> "cold"
    }

```

<br>

### when과 임의의 객체를 함께 사용

자바 switch와 달리 코틀린 when은 분기 조건은 임의의 객체를 허용한다.
  
두 색을 혼합했을 때 미리 정해진 팔레트에 들어있는 색이 임의의 객체를 허용한다. 두 색을 혼합했을 때 미리 정해진 팔레트에 들어있는 색이 될 수 있는지 알려주는 함수를 작성하자.
  
팔레트에 있는 색을 조합할 수 있는 방법이 많지 않기 때문에 모든 경우를 쉽게 열거할 수 있다.

```kt
fun mix(c1: Color, c2: Color) =
    when(setOf(c1, c2)) {
        setOf(RED, YELLOW) -> ORANGE
        setOf(YELLOW, BLUE) -> GREEN
        setOf(BLUE, VIOLET) -> INDIGO
        else -> throw Exception("Dirty color") // 매치되는 분기 조건이 없으면 이 문장을 실행한다.
    }

fun main() {
    println(mix(RED, YELLOW)) // ORANGE
}
```

setOf(c1, c2)와 조건에 있는 값과 비교를 할때 `동등성`을 사용한다.
  
그러므로 앞의 코드는 처음에 setOf(c1, c2)와 setOf(RED, YELLOW)를 비교하고 그 둘이 같지 않으면 계속 다음 분기의 조건 객체와 setOf(c1, c2)를 차례로 비교하는 식으로 작동한다.
  
모든 분기 식에서 만족하는 조건을 찾을 수 없다면 else 분기의 문장을 계산한다.
  
<br>

### 인자 없는 when의 사용

위의 예제에서 색깔의 조합을 비교할 때마다 setOf를 사용해 Set 인스턴스를 생성한다.
  
이는 역시 비효율적으로 이어질 수 있다.
   
물론 이러한 비효율성이 크게 문제가 되지 않긴하지만 이 함수가 자주 호출된다면 불필요한 가비지 객체가 늘어나기 때문에 비효율적이다.

코드는 약간 읽기 어려워지만 인자가 없는 when 식을 사용해 성능을 더 향상시켜볼 수 있다.

```kt
fun mixOptimized(c1: Color, c2: Color) =
    when {
        (c1 == RED && c2 == YELLOW) ||
        (c1 == YELLOW && c2 == RED) 
        -> ORANGE

        (c1 == YELLOW && c2 == BLUE) ||
        (c1 == BLUE && c2 == YELLOW) 
        -> GREEN

        (c1 == BLUE && c2 == VIOLET) ||
        (c1 == VIOLET && c2 == BLUE) 
        -> INDIGO

        else -> throw Exception("Dirty Color")
    }

fun main() {
    println(mixOptimized(RED, YELLOW)) // ORANGE
}
```

<br>

### 스마트 캐스트: 타입 검사와 타입 캐스트를 조합

예제로 (1 + 2) + 4와 같은 간단한 산술식을 계산하는 함수를 만들어보자.
  
함수가 받을 산술식에서는 오직 두 수를 더하는 연산만 가능하다.
  
다른 연산도 비슷한 방식으로 구현할 수 있다.

우선 식을 인코딩하는 방법을 생각해야 한다. 식을 트리 구조로 저장하자.
  
노드는 합계나 수중 하나다. Num은 항상 말단 노드지, Sum은 자식이 둘 잇는 중간 노드다.
  
Sum 노드의 두 자식은 덧셈의 두 인자다.
  
다음 리스트는 식을 표현하는 간단한 클래스를 보여준다.
  
식을 위한 Expr 인터페이스가 있고, Sum, Num 클래스는 그 Expr 인터페이스를 구현한다.
  
Expr은 아무런 메서드도 선언하지 않으며ㅡ 단지 여러 타입의 식 객체를 아우르는 공통 타입 역할만 수행한다.
  
클래스가 구현하는 인터페이스를 지정하기 위해서 콜론 뒤에 인터페이스 이름을 사용한다.

```kt
interface Expr
class Num(val value: Int): Expr
class Sum(val left: Expr, val right: Expr): Expr
```

Sum은 Expr의 왼쪽과 오른쪽 인자에 대한 참조를 LEFt, right 프로퍼티로 저장한다.
  
이 예제에서 left, right는 각각의 Num이나 Sum일 수 있다. (1 + 2) + 4라는 식을 저장하면 Sum(Sum(Num(1), Num(2)), Num(4)) 라는 구조의 객체가 생긴다.
  
이제 이 식의 값을 어떻게 계산하는지 살펴보자, 앞에서 살펴본 예를 평가한 값은 7이어야 한다.

```kt
println(eval(Sum(Sum(Num(1), Num(2))), Num(4))) // 7
```

Expr 인터페이스는 두 가지 구현 클래스가 존재한다. 따라서 식을 평가하려면 두 가지 경우를 고려해야한다.

- 어떤 식이 수라면 그 값을 반환한다
- 어떤 식이 합계라면 좌항과 우항의 값을 계산한 다음에 그 두 값을 합한 값을 반환한다.

자바 스타일로 작성한 함수를 먼저 살펴본 다음 코틀린 스타일로 만든 함수를 살펴보자. 
  
자바였다면 조건을 검사하기 위해 if문을 사용했을 것이다.
  
따라서 코틀린에서 if를 써서 자바 스타일로 함수를 작성해보자

```kt
fun eval(e: Expr): Int {
    if(e is Num) {
        val n = e as Num // 불필요한 중복
        return n.value
    }

    if(e is Sum) {
        return eval(e.right) + eval(e.left) // e에 대한 스마트 캐스트
    }
    throw IllegalArgumentException("Unknown expression")
}
```

코틀린에서는 is를 사용해 변수 타입을 검사한다. 자바의 instanceof랑 비슷하다.
  
하지만 자바에서는 instanceof로 확인한 다음에 그 타입에 속한 멤버에 접근하기 위해서는 명시적으롤 캐스팅한 결과를 저장한 후 사용해야한다.
  
코틀린에서는 프로그래머 대신 컴파일러가 원하는 타입으로 캐스팅하지 않아도 마치 처음부터 그 변수가 원하는 타입으로 선언된 것처럼 사용할 수 있다.
  
하지만 실제로는 컴파일러가 캐스팅을 수행해준다. 이를 `스마트 캐스트`라고 부른다.

eval 함수에서 e의 타입이 Num인지 검사한 다음 부분에서 컴파일러는 e의 타입을 Num으로 해석한다. 

그렇기에 Num의 프로퍼티인 value를 명시적 캐스팅 없이 e.value로 사용할 수 있다.
  
Sum의 프로퍼티인 right, left도 마찬가지다. 

> 스마트 캐스트는 is로 변수에 든 값의 타입을 검사한 다음에 그 값이 바뀔 수 없는 경우에만 작동한다.  
> 그렇기에 스마트캐스트를 사용한다면 그 프로퍼티는 반드시 val 이어야 하며 커스텀 접근자를 사용하는 것이어도 안 된다. (항상 같은 값을 리턴한다는 보장이 없기 때문이다)   
> 원하는 타입으로 명시적을 타입캐스팅을 하려면 as 키워드를 사용한다.

### 리팩토링: if를 when으로 변경

이제 eval 함수를 더욱 코틀린스럽게 리팩터링해보겠다.

```kt
fun eval(e: Expr): Int =
    if(e is Num) {
        e.value
    } else if (e is Sum) {
        eval(e.right) + eval(e.left)
    } else {
        throw IllegalArugmentException("Unknown expression")
    }

```
if의 분기에 식이 하나밖에 없다면 중괄호를 생략해도 된다.  
if 분기에 블록을 사용하는 경우 그 블록의 마지막 식이 그 분기의 결과 값이다.

이 코드를 when으로 더욱 다듬을 수도 있다.

```kt
fun eval(e: Expr): Int =
    when(e) {
        is Num -> e.value
        is Sum -> eval(e.right) + eval(e.left)
        else -> throw IllegalArgumentException("Unknown expression")
    }
```

<br>

### if와 when의 분기에서 블록 사용

if나 when 모두 분기에 블록을 사용할 수 있다. 
  
그런 경우 블록의 마지막 문장이 블록 전체의 결과가 된다.
  
예제로 봤던 eval 함수에 로그를 추가하고 싶다면 각 분기를 블록으로 만들고 블록의 맨 마지막에 그 분기의 결과 값을 위치시키면 된다.

```kt
fun eval(e: Expr): Int =
    when(e) {
        is Num -> { 
            println("num: ${e.value}")
            e.value
        }
        is Sum -> { 
            val left = evalWithLogging(e.left)
            val right = evalWithLogging(e.right)
            println("sum: $left + $right")
            left + right
        }
        else -> throw IllegalArgumentException("Unknown expression")
    }
```

이제 evalWithLogging 함수가 출력하는 로그를 보면 연산이 이뤄진 순서를 알 수 있다.

```
num: 1
num: 2
sum: 1 + 2
num: 4
sum : 3 + 4
7
```

<br>

## 대상을 이터레이션: while과 for 루프

### while 루프
코틀린에서는 while, do-while 루프가 있다. 두 루프의 문법은 자바와 다르지 않다.

<br>

### 수에 대한 이터레이션: 범위와 수열

코틀린에서는 루프의 가장 흔한 용례인 초깃값, 증가 값, 최종 값을 사용하는 것 대신에 코틀렌이서는 범위를 사용한다.
  
.. 연산자로 사용해 시작 값과 끝 값을 연결해서 범위를 만든다.

```kt
val oneToTen = 1..10
```

정수 범위로 수행할 수 있는 가장 단순한 작업은 범위에 속한 모든 값에 대한 이터레이션이다.
  
이런 식으로 어떤 범위에 속한 값을 일정한 순서로 이터레이션하는 경우를 **수열(Progression)**이라고 부른다.

피즈버즈 예제를 작성해보자 3으로 나눠떨어지는 수는 피즈, 5로 나눠떨어지는 수는 버즈 15로 나눠떨어지는 수는 피즈 버즈를 같이 출력한다.

```kt
fun fizzBuzz(i: Int) = when {
    i % 15 == 0 -> "FizzBuzz"
    i % 3 == 0 -> "Fizz"
    i % 5 == 0 -> "Buzz"
    else -> "$i"
}   

fun main() {
    for(i in 1..100){
        println(fizzBuzz(i))
    }

    for(i in 100 downTo 1 step 2){
        println(fizzBuzz(i))
    }
}

```