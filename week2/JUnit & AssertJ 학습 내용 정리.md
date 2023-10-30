# JUnit & AssertJ 학습 내용 정리
<br/>

## 1. 테스트 코드 개념 익히기
테스트 코드는 작성한 코드가 의도대로 잘 동작하고 예상치 못한 문제가 없는지 확인할 목적으로 작성하는 코드이다.<br/>
유지보수에도 좋고 코드 수정 시 기존 기능이 제대로 작동하지 않을까 봐 걱정하지 않아도 된다는 장점이 있다.

### 📌 테스트 코드란?
테스트 코드는 test 디렉터리에서 작업한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/fe22aab4-5b15-488d-84fe-c8798a72a7cc" width="330" height="300"/><br/>

### 📌 `given-when-then` 패턴
given-when-then 패턴은 테스트 코드를 세 단계로 구분해 작성하는 방식을 말한다.

1️⃣ **given**은 테스트 실행을 **준비**하는 단계, 2️⃣ **when**은 테스트를 **진행**하는 단계, 3️⃣ **then**은 테스트 결과를 **검증**하는 단계이다.

- 예를 들어 새로운 메뉴를 저장하는 코드를 테스트한다고 가정했을 때 테스트 코드를 다음과 같이 given, when, then을 적용해 구현한다.
  ```
  @DisplayName("새로운 메뉴를 저장한다.")
  @Test
  public void saveMenuTest() {
    // given : 메뉴를 저장하기 위한 준비 과정
    final String name = "아메리카노";
    final int price = 2000;

    final Menu americano = new Menu(name, price);

    // when : 실제로 메뉴를 저장
    final long savedId = menuService.save(americano);

    // then : 메뉴가 잘 추가되었는지 검증
    final Menu savedMenu = menuService.findById(savedId).get();
    assertThat(savedMenu.getName()).isEqualTo(name);
    assertThat(savedMenu.getPrice()).isEqualTo(price);
  }
  ```
  코드를 보면 세 부분으로 나누어져 있다. 메뉴를 저장하기 위해 준비하는 과정인 given 절, 실제로 메뉴를 저장하는 when절, 메뉴가 잘 추가되었는지 검증하는 then절로 나누어져 있다.

<br/>

## 2. 테스트 도구
스프링 부트는 애플리케이션을 테스트하기 위한 도구와 어노테이션을 제공한다.<br/>
spring-boot-starter-test 스타터에 테스트를 위한 도구가 모여 있다.
#### [spring-boot-starter-test 목록]
|테스트 도구명|설명|
|:---|:---|
|**[JUnit](###-📌-JUnit이란?)** 📌|자바 프로그래밍 언어용 **단위 테스트** 프레임워크|
|Spring Test<br/>& Spring Boot Test|스프링 부트 애플리케이션을 위한 통합 테스트 지원|
|**[AssertJ](###-📌-AssertJ로-검증문-가독성-높이기)** 📌|**검증문**인 `Assertion`을 작성하는 데 사용되는 라이브러리|
|Hamcrest|표현식을 이해하기 쉽게 만드는 데 사용되는 Matcher 라이브러리|
|Mockito|테스트에 사용할 가짜 객체인 목 객체를 쉽게 만들고, 관리하고, 검증할 수 있게<br/>지원하는 테스트 프레임워크|
|JSONassert|JSON용 어설션 라이브러리|
|JsonPath|JSON 데이터에서 특정 데이터를 선택하고 검색하기 위한 라이브러리|

### 📌 `JUnit`이란?
JUnit은 **자바 언어를 위한 단위 테스트 프레임워크**이다.
- 단위 테스트 : 작성한 코드가 의도대로 작동하는지 작은 단위로 검증하는 것을 의미한다. 이때 단위는 보통 **메소드**가 된다.

#### [JUnit의 특징]
- 테스트 방식을 구분할 수 있는 어노테이션을 제공
- @Test 어노테이션으로 메소드를 호출할 때마다 새 인스턴스를 생성, 독립 테스트 가능
- 예상 결과를 검증하는 Assertion 메소드 제공
- 사용 방법이 단순하고 테스트 코드 작성 시간이 적음
- 자동 실행, 자체 결과를 확인하고 즉각적인 피드백을 제공
- 테스트 결과가 직관적임

#### [JUnit으로 단위 테스트 코드 만들기]
**1️⃣ JUnitTest 파일을 만든다. [src → test → java] 폴더에 JUnitTest.java 파일을 생성하고 코드를 작성한다.**

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/d18a869d-2e8b-41f4-97f5-e1c3c61c2363" width="300" height="70"/><br/>

```java
public class JUnitTest {
  @DisplayName("1 + 2는 3이다")  // 테스트 이름
  @Test // 테스트
  public void junitTest() {
    int a = 1;
    int b = 2;
    int sum = 3;

    Assertions.assertEquals(sum, a + b);  // 값이 같은지 확인
  }
}
```
- `@DisplayName` 어노테이션은 **테스트 이름을 명시**한다.
- `@Test` 어노테이션을 붙인 메소드는 **테스트를 수행**하는 메소드가 된다.
- JUnit은 테스트끼리 영향을 주지 않도록 **각 테스트를 실행할 때마다 테스트를 위한 실행 객체를 만들고 테스트가 종료되면 실행 객체를 삭제**한다.
- JUnit에서 제공하는 검증 메소드인 `assertEquals()` 의 첫 번째 인수에는 **기대하는 값**, 두 번째 인수에는 **실제로 검증할 값**을 넣어준다.
  - 이 테스트에서는 assertEquals()로 a + b와 sum의 값이 같은지 확인한다.

**2️⃣ 실제로 테스트 코드가 잘 동작하는지 확인한다. [▶] 버튼을 클릭하고 [Run 'JUnitTest']를 클릭해서 테스트를 실행한다.**

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/3e84ba13-f896-4451-aa12-9c95f9895b15" width="500" height="300"/><br/>

테스트가 끝나면 콘솔창에 테스트 결과가 출력된다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/fe892be9-7dd3-4a54-9296-2a1a73445d87" width="450" height="200"/>

- 한글이 깨지는 경우 [Settings → Build, Execution, Deployment → Gradle]에서 Build and run using과 Run tests using을 Gradle에서 intelliJ IDEA로 바꾸면 된다.

**3️⃣ 실패를 위한 테스트 케이스를 하나 더 추가해본다. junitTest() 메소드 바로 아래에 다음 코드를 추가해보자.**

```java
public class JUnitTest {
  ... 생략 ...
  @DisplayName("1 + 3은 4이다.")
  @Test
  public void junitFailedTest() {
    int a = 1;
    int b = 3;
    int sum = 3;

    Assertions.assertEquals(sum, a + b);  // 실패하는 케이스
  }
}
```
실패용 테스트 케이스를 실행하면 테스트가 실패했다는 표시와 함께 기댓값과 실제로 받은 값을 비교해서 알려준다.<br/>
이렇게 JUnit은 테스트 케이스가 하나라도 실패하면 전체 테스트를 실패한 것으로 보여준다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/6cd53d6f-a2e1-42a4-8393-ef32107937b5" width="450" height="200"/><br/>
<br/>
**4️⃣ 자주 사용하는 JUnit의 어노테이션을 알아보자.**

앞서 JUnit은 각 테스트에 대해 객체를 만들어 독립적으로 실행한다고 했는데 그 내용을 확인할 수 있다. (테스트용 메소드가 많음)

또, 테스트는 어노테이션에 따라 실행 순서가 정해진다.

```java
import org.junit.jupiter.api.*;

public class JUitCycleTest {
  @BeforeAll  // 전체 테스트를 시작하기 전에 1회 실행하므로 메소드는 static으로 선언
  static void beforeAll() {
    System.out.println("@BeforeAll");
  }

  @BeforeEach // 테스트 케이스를 시작하기 전마다 실행
  static void beforeEach() {
    System.out.println("@BeforeEach");
  }

  @Test
  public void test1() {
    System.out.println("test1");
  }

  @Test
  public void test2() {
    System.out.println("test2");
  }

  @Test
  public void test3() {
    System.out.println("test3");
  }

  @AfterAll  // 전체 테스트를 마치고 종료하기 전에 1회 실행하므로 메소드는 static으로 선언
  static void afterAll() {
    System.out.println("@AfterAll");
  }

  @AfterEach // 테스트 케이스를 종료하기 전마다 실행
  public void afterEach() {
    System.out.println("@AfterEach");
  }
}
```
#### [@`BeforeAll`]
- 전체 테스트를 시작하기 전에 처음으로 한 번만 실행된다.
  - 예를 들어 데이터베이스를 연결해야 하거나 테스트 환경을 초기화할 때 사용된다.
- 전체 테스트 실행 주기에서 한 번만 호출되어야 하기 때문에 메소드를 static으로 선언해야 한다.

#### [@`BeforeEach`]
- 테스트 케이스를 시작하기 전에 매번 실행된다.
  - 예를 들어 테스트 메소드에서 사용하는 객체를 초기화하거나 테스트에 필요한 값을 미리 넣을 때 사용할 수 있다.
- 각 인스턴스에 대해 메소드를 호출해야 하므로 메소드는 static이 아니어야 한다.

#### [@`AfterAll`]
- 전체 테스트를 마치고 종료하기 전에 한 번만 실행한다.
  - 예를 들어 데이터베이스 연결을 종료할 때나 공통적으로 사용하는 자원을 해제할 때 사용할 수 있다.
- 전체 테스트 실행 주기에서 한 번만 호출되어야 하기 때문에 메소드를 static으로 선언해야 한다.

#### [@`AfterEach`]
- 각 테스트 케이스를 종료하기 전 매번 실행한다.
  - 예를 들어 테스트 이후에 특정 데이터를 삭제해야 하는 경우 사용한다.
- @BeforeEach 어노테이션과 마찬가지로 메소드는 static이 아니어야 한다.

어노테이션을 중심으로 JUnit의 실행 흐름을 살펴보면 다음과 같다.

@BeforeEach부터 @AfterEach까지 테스트 개수만큼 반복된 결과물을 볼 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/a04adb08-04ed-4de8-8296-31412c5f2751" width="300" height="400"/><br/>

**5️⃣ 테스트 코드를 실행해서 출력 결과를 살펴본다.**

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/db5dfff9-5794-4da0-98cc-c9eb6b549581" width="450" height="190"/><br/>

결과를 보면 `@BeforeAll` 어노테이션으로 설정한 메소드가 실행되고, 그 이후에는 테스트 케이스 개수만큼 `@BeforeEach` → `@Test` → `@AfterEach`의 생명주기로 테스트가 진행된다.
모든 테스트 케이스가 끝나면 `@AfterAll` 어노테이션으로 설정한 메소드를 실행하고 종료한다.

### 📌 `AssertJ`로 검증문 가독성 높이기
AssertJ는 JUnit과 함께 사용해 **검증문의 가독성을 높여주는 라이브러리**이다.<br/>
이를테면 앞서 작성한 테스트 코드의 Assertion은 기댓값과 실제 비교값을 명시하지 않으므로 비교 대상이 헷갈린다.
- 예를 들어 다음 코드를 보면 기댓값과 비교값이 잘 구분되지 않는다.
  ```java
  Assertions.assertEquals(sum, a + b);
  ```
큰 문제라고 생각하지 않을 수 있겠지만 대규모 프로젝트에서는 조금 더 명확한 모습의 코드가 실수를 줄일 수 있어 이런 가독성은 꽤 중요한 문제이다.

다음은 AssertJ를 적용한 코드이다.
- ```java
  assertThat(a + b).isEquals(sum);
  ```
  이 경우 a와 b를 더한 값이 sum과 같아야 한다는 의미로 명확하게 읽히기 때문에 코드를 읽는 사람이 헷갈리지 않는다.

AssertJ에는 값이 같은지 비교하는 isEqualTo(), isNotEqualTo() 외에도 다양한 메소드를 제공한다.

|메소드 이름|설명|
|:---|:---|
|isEqualTo(A)|A 값과 같은지 검증|
|isNotEqualsTo(A)|A 값과 다른지 검증|
|contains(A)|A 값을 포함하는지 검증|
|doesNotContain(A)|A 값을 포함하지 않는지 검증|
|startsWith(A)|접두사가 A인지 검증|
|endsWith(A)|접미사가 A인지 검증|
|isEmpty()|비어 있는 값인지 검증|
|isNotEmpty()|비어 있지 않은 값인지 검증|
|isPositive()|양수인지 검증|
|isNegative()|음수인지 검증|
|isGreaterThan(1)|1보다 큰 값인지 검증|
|isLessThan(1)|1보다 작은 값인지 검증|
