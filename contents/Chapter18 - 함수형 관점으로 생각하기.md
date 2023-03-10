# 함수형 관점으로 생각하라

# 왜 함수형 프로그래밍을 사용하는가?

함수형 프로그래밍은 `부작용 없음`과 `불변성` 을 제공한다. 

## 공유된 가변 데이터

변수가 예상하지 못한 값을 갖는 이유는 결국 우리가 유지보수하는 시스템의 여러 메서드에서 공유된 가변 데이터 구조를 읽고 갱신하기 때문이다. 
하지만 어떤 자료구조도 바꾸지 않는 시스템이 있다고 가정해본다면 예상하지 못하게 자료구조의 값이 바뀔일이 없으니 유지보수하기 쉬울것이다!

이렇게 자신을 포함하는 `클래스의 상태`, 그리고 `객체의 상태`를 바꾸지 않으며 `return` 문을 통해서만 자신의 결과를 반환하는 메서드를 `순수메서드` 또는 `부작용 없는 메서드`라고 부른다

- 부작용 예시 (부작용이란 함수내에 포함되지 못한 기능을 말한다)
    - 자료구조를 고치거나 필드에 값을 할당
        - 생성자 이외의 초기화 동작(Setter 메서드 같은 것)
    - 예외 발생
    - 파일에 쓰기 등의 I/O 동작 실행

### 불변객체

부작용을 없애는 방법에는 불변객체의 이용이 있다.
불변 객체는 인스턴스화 한 다음에는 객체의 `상태를 바꿀 수 없는` 객체이므로 함수 동작에 영향을 받지 않는다. 
(즉 예상하지 못한 상태로 바뀌지 않는다)

따라서 불변객체는 `복사하지 않고 공유`할 수 있으며, 객체의 상태를 바꿀 수 없으므로 `스레드 안전성`을 제공한다.
부작용 없는 시스템 컴포넌트에서는 메서드가 서로 간섭하는 일이 없으므로 잠금(Lock)을 사용하지 않고도 멀티코어 병렬성을 사용할 수 있다. 또한 프로그램의 어떤 부분이 독립적인지 바로 이해할 수 있다. 

## 선언형 프로그래밍

프로그램을 시스템으로 구현하는 방식은 크게 두가지로 구분할 수 있다

- 고전의 객체지향 프로그래밍(명령형 프로그래밍 방식)
    - `어떻게` 에 집중하는 프로그래밍 형식
- 선언형 프로그래밍
    - `무엇을`에 집중하는 방식
    - 문제 자체가 코드로 명확하게 드러난다는 강점이 있다.

## 왜 함수형 프로그래밍인가?

함수형 프로그래밍은 선언형 프로그래밍을 따르는 대표적인 방식이며 `부작용이 없는` 계산을 지향한다. 
선언형 프로그래밍과 부작용을 멀리한다는 두 가지 개념은 좀 더 쉽게 시스템을 구현하고 유지보수 하는데 도움을 준다. 

함수형 프로그래밍을 이용하면 부작용이 없는 복잡하고 어려운 기능을 수행하는 프로그래밍을 구현할 수 있다

### 함수형 프로그래밍이란 무엇인가?

함수형이라는 말은 ‘수학의 함수처럼 부작용이 없는’을 의미한다. 
결론적으로 `함수 그리고 If-then-else 등의 수학적 표현만 사용` 하는 방식을 `순수 함수형 프로그래밍`이라고 하며 `시스템의 다른 부분에 영향을 미치지 않는다면 내부적으로는 함수형이 아닌 기능도 사용` 하는 방식을 `함수형 프로그래밍`이라고 한다

### 함수형 자바

실질적으로 자바로는 완벽한 순수 함수형 프로그래밍을 구현하기 어렵기 때문에 순수함수형이 아니라 함수형 프로그램을 구현한다.(실제 부작용이 있지만 아무도 이를 보지 못하게 함으로써 함수형을 달성한다)

- 함수나 메서드는 지역 변수만을 변경해야 함수형이라고 할 수 있다.
- 함수나 메서드에서 참조하는 객체는 불변객체여야 한다
- 예외적으로 `메서드 내`에서 생성한 객체의 필드는 갱신할수 있지만, 새로 생성한 객체의 필드 갱신이 외부에 노출되지 않아야하고 다음에 다시 메서드를 호출한 결과에 영향을 미치지 않아야한다.
- 함수나 메서드가 어떤 예외도 일으키지 않아야 한다.
    - 예외가 발생하면 retrun으로 결과를 반환할 수 없게 되기 때문
- 예외를 사용하지말고 Optional을 사용(모든 코드가 Optional을 사용하도록 반드시 고쳐야된다는 것은 아니다)
    - Optional을 이용하면 예외 없이도 결과값으로 연산의 성공여부를 확인할 수 있다
    - 비정상적인 입력값이 있을 때 자바에서는 예외를 일으키는 것이 자연스러운 방식이지만, 예외를 처리하는 과정에서 함수형에 위배되는 제어흐름이 발생한다면 결국 인수를 전달해서 결과를 받는다는 수학적 함수의 모델이 깨진다.
- 함수형에서는 비함수형 동작을 감출 수 있는 상황에서만 부작용을 포함하는 라이브러리 함수를 사용해야한다.
    - 즉, 먼저 자료구조를 복사한다든가 발생할 수 있는 예제를 적절하게 내부적으로 처리함으로써 자료구조의 변경을 호출자가 알 수 없도록 감춰야 한다.

## 참조 투명성

`부작용을 감춰야한다` 는 제약은 `참조 투명성` 개념으로 귀결된다. 즉, 같은 인수로 함수를 호출했을 때 항상 같은 결과를 반환한다면 참조적으로 투명한 함수라고 표현한다. 

- 참조 투명성의 장점
    - 프로그램 이해에 큰 도움을 준다
    - 비싸거나 오랜 시간이 걸리는 연산을 기억화, 또는 캐싱을 통해 다시 계산하지 않고 저장하는 최적화 기능도 제공한다

List를 반환하는 메서드를 두 번 호출한다고 가정했을 때, 결과 리스트가 `가변 객체`라면 반환된 두 리스트는 같은 객체라 할 수 없다. ( = 참조적으로 투명한 메서드가 아니다.)

하지만 결과 리스트를 `불변 값`으로 사용할 것이라면 두 리스트는 같은 객체라 볼 수 있으므로 참조적으로 투명한 것으로 간주할 수 있다. 

출처 : 모던자바 인 액션 

<aside>
🐬  책에서 인상 깊었던 내용

: 애초부터 끔찍한 디버깅 문제가 발생할 가능성이 없도록 구현된 코드를 선호하라 !
</aside>
