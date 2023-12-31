# Kotlin Dynamic Action

> Kotlin In Action을 읽고 더욱 Dynamic하게 기록합니다.

<img src ="https://velog.velcdn.com/images/haero_kim/post/212f9167-e32d-41f1-be80-0e6bc12c6cf8/general.png" width = 700px height = 350px></img>

## 타임라인

1. [코틀린 기초](./1.Kotlin-Basic/함수,%20변수,%20클래스,%20enum,%20프로퍼티를%20선언하는%20방법.md)

2. [함수 정의와 호출](./2.Functional/)
3. [클래스, 객체, 인터페이스](./3.Object/)
4. [람다로 프로그래밍](./4.Lambda/)
5. [코틀린 타입 시스템](./5.Nullable/)
6. [연산자 오버로딩과 기타 관계](./6.Operator/)
7. [고차 함수: 파라미터와 반환 값으로 람다 사용](./7.High-Level-Function/)
8. [제네릭스](./8.Generics/)
9. [어노테이션과 리플렉션](./9.Annotation-Reflection/)

<br>

## 코틀린 개요

코틀린은 자바 플랫폼에서 돌아가는 새로운 프로그래밍 언어다.
  
간결하고 실용적이며, 자바 코드와의 `상호운용성(interoperablity)`를 중시한다.
  
현재 자바가 사용 중인 곳이라면 거의 대부분 코틀린을 활용할 수 있다.

<br>

## 코틀린의 특징

### 정적 타입 지정 언어
모든 프로그램 구성 요소의 타입을 컴파일 시점에 알 수 있고 프로그램 안에서 객체의 필드나 메서드를 사용할 때마다 컴파일러가 타입을 검증해준다는 뜻
  
장점으로는
- **성능**: 실행 시점에 어떤 메서드를 호출할지 알아내는 과정이 필요 없으므로 메서드 호출이 더 빠르다.

- **신뢰성**: 컴파일러가 프로그램의 정확성을 검증하기 때문에 실행 시 플고그램이 오류로 중단될 가능성이 더 적어진다.
- **유지 보수성**: 코드에서 다루는 객체가 어떤 타입에 속하는지 알 수 있기 때문에 처음 보는 코드를 다룰 때도 더 쉽다.
- **도구 지원**: 정적 타입 지정을 활용하면 더 안전하게 리팩터링을 할 수 있고, 도구는 더 정확한 코드 완성 기능을 제공할 수 있으며, IDE의 다른 지원 기능도 더 잘 만들 수 있다.

### 함수형 프로그래밍과 객체지향 프로그래밍

- **일급 시민인 함수**: 함수를 일반 값처럼 다룰 수 있다. 변수에 저장할 수 있고, 인자로도 전달할 수 있고, 함수에서 새로운 함수를 만들어서 반환할 수 있다.

- **불변성**: 일단 만들어지고 나면 내부 상태가 절대로 바뀌지 않는 불변 객체를 사용해 프로그램을 작성한다.
- **부수 효과 없음**: 입력이 같으면 항상 같은 출력을 내놓고 다른 객체의 상태를 변경하지 않으며, 함수 외부나 다른 바깥 환경과 상호작용하지 않는 순수 함수를 사용한다.


<br>

### Ref
[Kotlin In Action](https://www.yes24.com/Product/Goods/55148593)
