## 커밋 메시지를 의미 있게 작성한다
커밋 메시지에 해당 커밋에서 작업한 내용에 대한 이해가 가능하도록 작성한다.

## git을 통해 관리할 자원에 대해서도 고려한다
git에 코드를 추가할 때는 git을 통해 관리할 필요가 있는지를 고려한다.
- git을 통한 관리가 불필요한 것들
  - `.class` 파일 : java 코드가 있으면 생성 가능
  - IntelliJ IDEA의 `.idea`  폴더, Eclipse의 `.metadata` 폴더 : 개발 도구가 자동으로 생성하는 폴더

## 이름을 통해 의도를 드러낸다
나 자신, 다른 개발자와의 소통을 위해 가장 중요한 활동 중의 하나가 좋은 이름 짓기이다.
- 변수 이름, 함수(메서드) 이름, 클래스 이름 : **역할**에 대한 의도 포함

## 축약하지 않는다
```
객체 지향 생활 체조 원칙 5: 줄여쓰지 않는다 (축약 금지)
```
의도를 드러낼 수 있다면 이름이 길어져도 괜찮다.
- 클래스와 메서드 이름을 한 두 단어로 유지하려고 노력하고 문맥을 중복하는 이름을 자제
  - [ex] 클래스 이름이 Order라면 shipOrder보다는 ship이라고 하면 클라이언트에서는 order.ship()라고 호출하며, 간결한 호출의 표현이 가능 

## 공백도 코딩 컨벤션이다
if, for, while문 사이의 공백도 코딩 컨벤션이다.

## 공백 라인을 의미 있게 사용한다
문맥을 분리하는 부분에 사용하는 것이 좋다. 과도한 공백은 다른 개발자에게 의문을 줄 수 있다.

## space와 tab을 혼용하지 않는다
둘 중에 하나만 사용한다.

## 의미 없는 주석을 달지 않는다
가능하면 이름을 통해 의도를 드러내고, 의도를 드러내기 힘든 경우 주석을 다는 연습을 한다.

## IDE의 코드 자동 정렬 기능을 활용한다
IDE의 코드 자동 정렬 기능을 사용하면 더 깔끔한 코드를 볼 수 있다.
- IntelliJ IDEA: ⌥⌘L, Ctrl+Alt+L
- Eclipse: ⇧⌘F, Ctrl+Shift+F

## Java에서 제공하는 API를 적극 활용한다
함수(메서드)를 직접 구현하기 전에 Java API에서 제공하는 기능인지 검색을 먼저 해본다.
Java API에서 제공하지 않을 경우 직접 구현한다.
- 예를 들어 사용자를 출력할 때 사용자가 2명 이상이면 쉼표(,) 기준으로 출력을 위한 문자열은 다음과 같이 구현 가능하다.
  ```
  List<String> members = Arrays.asList("pobi", "jason");
  String result = String.join(",", members); // "pobi,jason"
  ```

## 배열 대신 Java Collection을 사용한다
Java Collection 자료구조(List, Set, Map 등)를 사용하면 데이터를 조작할 때 다양한 API를 사용할 수 있다.

## README.md를 상세히 작성한다
미션 저장소의 README.md는 소스코드에 앞서 해당 프로젝트가 어떠한 프로젝트인지 마크다운으로 작성하여 소개하는 문서이다.
해당 프로젝트가 어떠한 프로젝트이며, 어떤 기능을 담고 있는지 기술한다.'

## 기능 목록을 재검토한다
클래스/함수(메서드) 설계와 구현과 같이 너무 상세하게 작성하지 않는다. 구현해야 할 기능 목록을 정리하는 데 집중한다.
- 정상적인 경우 뿐만 아니라 예외적인 상황도 기능 목록에 정리 (기능을 구현하면서 계속해서 추가)

## 기능 목록을 업데이트한다
기능 목록은 기능 구현을 하면서 변경될 수 있다.

## 값을 하드 코딩하지 않는다
상수(`static final`)를 만들고 이름을 부여해 이 변수의 역할이 무엇인지 의도를 드러내라.

## 구현 순서도 코딩 컨벤션이다
클래스는 상수, 멤버 변수, 생성자, 메서드 순으로 작성한다.
```
class ClassName {
  상수(static final) 또는 클래스 변수
  인스턴스 변수
  생성자
  메소드
}
```
## 변수 이름에 자료형은 사용하지 않는다
변수 이름에 자료형, 자료 구조 등을 사용하지 않는다.

## 한 함수가 한 가지 기능만 담당하게 한다
함수 길이가 길어진다면 한 함수에서 여러 일을 하려고 하는 경우일 가능성이 높다.

## 함수가 한 가지 기능을 하는지 확인하는 기준을 세운다
- 여러 함수에서 중복되어 사용되는 코드가 있는 경우
- 함수의 길이를 15라인을 넘어가는 경우
  - `main()` 함수에도 해당
  - 공백 라인도 한 라인에 해당

## 테스트를 작성하는 이유에 대해 본인의 경험을 토대로 정리해본다
단지 기능을 점검하기 위한 목적으로 테스트를 작성하는 것은 아니다
- 테스트를 작성하는 과정을 통한 빠른 피드백 가능
- 학습 도구로도 활용 ([학습테스트를 통해 JUnit 학습하기.pdf](https://techcourse-storage.s3.ap-northeast-2.amazonaws.com/9b82d8a360c548fcadd14c551dbcbe06))

## 처음부터 큰 단위의 테스트를 만들지 않는다
테스트의 중요한 목적 중 하나는 내가 작성하는 코드에 대해 빠르게 피드백을 받는 것이다.
- 문제를 작게 나누고, 그 중 핵심 기능에 가까운 부분부터 작게 테스트

## 발생할 수 있는 예외 상황에 대해 고민한다
예외 상황을 고려해 프로그래밍하는 습관을 들인다. 예외 상황을 고민해 보고 해당 예외에 대해 처리를 할 수 있어야 한다.

## 비즈니스 로직과 UI 로직을 분리한다
비즈니스 로직과 UI 로직을 한 클래스가 담당하지 않도록 한다. 단일 책임의 원칙에도 위배된다.
- 로그 메시지 성격이 강한 경우 (현재 객체의 상태) : `toString()` 활용
- View에서 사용할 데이터 : `getter` 메서드를 통해 데이터를 전달

## 연관성이 있는 상수는 static final 대신 enum을 활용한다

## final 키워드를 사용해 값의 변경을 막는다

## 객체의 상태 접근을 제한한다
인스턴스 변수의 접근 제어자는 `private`으로 구현한다.

## 객체는 객체스럽게 사용한다
로직에 대한 구현이 필요하다.
- Lotto에서 데이터를 꺼내지(get) 말고 메시지를 던지도록 구조를 변경하여 데이터를 가지는 객체가 일하도록 설계
  ```
  public class Lotto {
      private final List<Integer> numbers;

      public boolean contains(int number) {
          // 숫자가 포함되어 있는지 확인한다.
          ...
      }
    
      public int matchCount(Lotto other) {
          // 당첨 번호와 몇 개가 일치하는지 확인한다.
          ...
      }
  }

  public class LottoGame {
      public void play() {
          Lotto lotto = new Lotto(...);
          lotto.contains(number);
          lotto.matchCount(...); 
      }
  }
  ```
- 참고 : [getter를 사용하는 대신 객체에 메시지를 보내자](https://tecoble.techcourse.co.kr/post/2020-04-28-ask-instead-of-getter/)

## 필드(인스턴스 변수)의 수를 줄이기 위해 노력한다
필드(인스턴스 변수)의 수가 많은 것은 객체의 복잡도를 높이고, 버그 발생 가능성을 높일 수 있다.
필드에 중복이 있거나, 불필요한 필드가 없는지 확인해 필드의 수를 최소화한다.
- 예를 들어 총상금 및 수익률을 구하는 다음 객체를 보자.
  ```
  public class LottoResult {
      private Map<Rank, Integer> result = new HashMap<>();
      private double profitRate;
      private int totalPrize;
  }
  ```
  위 객체의 profitRate와 totalPrize는 등수 별 당첨 내역(result)만 있어도 모두 구할 수 있는 값이다. 따라서 위 객체는 다음과 같이 하나의 필드만으로 구현할 수 있다.
  ```
  public class LottoResult {
      private Map<Rank, Integer> result = new HashMap<>();

      public double calculateProfitRate() { ... }
    
      public int calculateTotalPrize() { ... }
  }
  ```

## 성공하는 케이스 뿐만 아니라 예외에 대한 케이스도 테스트한다
예외에 대한 부분 또한 처리해야 한다. 특히 프로그램에서 결함이 자주 발생하는 부분 중 하나는 경계값이므로 이 부분을 꼼꼼하게 확인해야 한다.

## 테스트 코드도 코드다
테스트 코드도 코드이므로 리팩터링을 통해 개선해 나가야 한다. 특히 반복적으로 하는 부분을 중복되지 않게 만들어야 한다.
- 예를 들어 단순히 파라미터의 값만 바뀌는 경우라면 아래와 같이 테스트할 수 있다.
  ```
  @DisplayName("천원 미만의 금액에 대한 예외 처리")
  @ValueSource(strings = {"999", "0", "-123"})
  @ParameterizedTest
  void underLottoPrice(Integer input) {
      assertThatThrownBy(() -> new Money(input))
              .isInstanceOf(IllegalArgumentException.class);
  }
  ```

## 테스트를 위한 코드는 구현 코드에서 분리되어야 한다
테스트를 위한 편의 메서드를 구현 코드에 구현하지 마라. 테스트를 통과하기 위해 구현 코드를 변경하거나 테스트에서만 사용되는 로직을 만들지 않는다.
- 테스트를 위해 접근 제어자를 바꾸는 경우
- 테스트 코드에서만 사용되는 메서드

## 단위 테스트하기 어려운 코드를 단위 테스트하기
- 아래 코드는 Random 때문에 Lotto에 대한 단위 테스트를 하기 힘들다. 단위 테스트가 가능하도록 리팩터링한다면 어떻게 하는 것이 좋을까?
  ```
  import camp.nextstep.edu.missionutils.Randoms;

  public class Lotto {
      private List<Integer> numbers;

      public Lotto() {
          this.numbers = Randoms.pickUniqueNumbersInRange(1, 45, 6);
      }
  }
  
  ——————
  
  public class LottoMachine {
      public void execute() {
          Lotto lotto = new Lotto();
      }
  }
  ```
  올바른 로또 번호가 생성되는 것을 테스트하기 어렵다. 테스트하기 어려운 것을 클래스 내부가 아닌 외부로 분리하는 시도를 해 본다.
  ```
  public class Lotto {
      private List<Integer> numbers;

      public Lotto(List<Integer> numbers) {
          this.numbers = numbers;
      }
  }
  
  ——————

  import camp.nextstep.edu.missionutils.Randoms;

  public class LottoMachine {
      public void execute() {
          List<Integer> numbers = Randoms
              .pickUniqueNumbersInRange(1, 45, 6);
          Lotto lotto = new Lotto(numbers);
      }
  }
  ```
  이처럼 단위 테스트를 할 때 테스트하기 어려운 부분은 분리하고 테스트 가능한 부분을 단위 테스트한다.
  테스트하기 어려운 부분은 단위 테스트하지 않아도 된다. 남은 LottoMachine은 어떻게 테스트하기 쉽게 바꿀 수 있을지 고민해 본다.
- 참고 : [메서드 시그니처를 수정하여 테스트하기 좋은 메서드로 만들기](https://tecoble.techcourse.co.kr/post/2020-05-07-appropriate_method_for_test_by_parameter/)
 
## private 함수를 테스트 하고 싶다면 클래스(객체) 분리를 고려한다
가독성의 이유만으로 분리한 private 함수의 경우 public으로도 검증 가능하다고 여겨질 수 있다.
public 함수가 private 함수를 사용하고 있기 때문에 자연스럽게 테스트 범위에 포함된다.

하지만 가독성 이상의 역할을 하는 경우, 테스트하기 쉽게 구현하기 위해서는 해당 역할을 수행하는 다른 객체를 만들 타이밍이 아닐지 고민해 볼 수 있다.
다음 단계를 진행할 때에는 너무 많은 역할을 하고 있는 함수나 객체를 어떻게 의미 있는 단위로 분할할지에 초점을 맞춰 진행한다.
