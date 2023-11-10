# Introduction to AssertJ
[Introduction to AssertJ](https://www.baeldung.com/introduction-to-assertj) 문서를 읽고 정리한 내용입니다.
<br/>
<br/>
## Introduction
AssertJ는 다음을 사용할 때 쉽고 가독성 있게 Assertion을 작성할 수 있도록 해주는 클래스 및 유틸리티 메서드 집합을 제공한다.
- Standard Java (표준 자바)
- Java 8 (자바 8)
- Guava
- Joda Time
- Neo4J
- Swing 구성 요소
모든 모듈의 자세한 목록은 [프로젝트 웹사이트](https://joel-costigliola.github.io/assertj/)에서 확인할 수 있다.

다음은 AssertJ 문서의 일부 예제이다.
```java
assertThat(frodo)
  .isNotEqualTo(sauron)
  .isIn(fellowshipOfTheRing);

assertThat(frodo.getName())
  .startsWith("Fro")
  .endsWith("do")
  .isEqualToIgnoringCase("frodo");

assertThat(fellowshipOfTheRing)
  .hasSize(9)
  .contains(frodo, sam)
  .doesNotContain(sauron);
```
위의 예제는 일부에 불과하지만, 이 라이브러리를 사용하여 어떻게 검증문을 작성할 수 있는지에 대한 개요를 제공한다.
<br/>
<br/>
## AssertJ in Action
### 1. Getting Started
라이브러리의 JAR 파일이 classpath에 있는 경우, 다음 import문으로 AssertJ를 적용할 수 있다.
```java
import static org.assertj.core.api.Assertions.*;
```
### 2. Writing Assertions
Assertion을 작성하려면 항상 객체를 `Assertions.assertThat()` 메서드에 전달해야 한다.

다른 일부 라이브러리와는 달리 아래 코드는 실제로 아무것도 검증하지 않으며 fail이 발생하지 않는다.
```java
assertThat(anyReferenceOrValue);
```
IDE의 코드 완성 기능을 활용하면 AssertJ 검증문을 작성하는 것이 매우 쉽다.
- IDE(통합 개발 환경)의 코드 완성 기능
  
  <img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/f8da4030-03c4-4aaf-a684-28ee9d94965a" width="600" height="250"/><br/>
  - 컨텍스트 메서드 중 수십 가지를 확인할 수 있다. 이 중 일부는 문자열 유형에만 사용 가능하다. 이 API의 일부를 자세히 살펴보고 특정 Assertion을 살펴보자.
### 3. Object Assertions
객체는 두 객체의 동등성을 결정하거나 객체의 필드를 검사하는 여러 가지 방법으로 비교할 수 있다.

- 다음은 두 개의 Dog 객체 fido와 fidosClone이 주어졌을 때 두 객체의 동등성을 비교하는 두 가지 방법이다.

  ```java
  public class Dog { 
      private String name; 
      private Float weight;
    
      // standard getters and setters
  }

  Dog fido = new Dog("Fido", 5.25);

  Dog fidosClone = new Dog("Fido", 5.25);
  ```
  다음과 같은 Assertion을 사용하여 동등성을 비교할 수 있다
  ```java
  assertThat(fido).isEqualTo(fidosClone);
  ```
  이 Assertion은 false를 반환한다. `isEqualTo()`는 객체 참조를 비교하기 때문이다.
  ```
  assertThat(fido).isEqualToComparingFieldByFieldRecursively(fidosClone);
  ```
객체의 내용(모든 필드의 값)을 비교하려면 `isEqualToComparingFieldByFieldRecursively()`를 사용해야 한다.<br/>
- Fido와 fidosClone은 재귀적인 필드 비교를 수행할 때 동일하다. 이는 한 객체의 각 필드가 다른 객체의 해당 필드와 비교하는 것을 말한다.
  즉, 두 객체의 필드뿐만 아니라 필요한 경우 중첩된 객체의 필드까지 모두 동일한지 확인한다.

이 외에도 객체를 비교하고 대조하며 필드를 검사하고 검증하는 다양한 방법을 제공하는 많은 Assertion 메소드가 있다.
- [공식 AbstractObjectAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractObjectAssert.html) 참조
## 4. Boolean Assertions
true/false 테스트를 위한 메소드는 다음과 같다.
```java
isTrue()
isFalse()
```
다음과 같이 사용한다.
```java
assertThat("".isEmpty()).isTrue();
```
## 5. Iterable/Array Assertions
Iterable 또는 배열에 원소가 존재하는지 확인하는 여러 가지 방법이 있는데, 가장 일반적인 Assertion 중 하나는 Iterable이나 배열이 특정 요소를 포함하는지 확인하는 것이다.
```java
List<String> list = Arrays.asList("1", "2", "3");

assertThat(list).contains("1");
```
또는 List의 원소가 없는지(비어있지 않은지) 확인할 수 있다.
```java
assertThat(list).isNotEmpty();
```
또는 List가 특정 문자로 시작하는지 확인하는 경우도 있다.
```java
assertThat(list).startsWith("1");  // "1"로 시작하는 경우
```
동일한 객체에 대해 여러 Assertion을 생성하려면 다음과 같이 쉽게 결합할 수 있습니다.
```java
// 주어진 목록이 비어 있지 않으며 "1" 요소를 포함하며 null이 포함되지 않으며 요소 "2", "3"의 sequence를 포함하는지 확인
assertThat(list)
  .isNotEmpty()
  .contains("1")
  .doesNotContainNull()
  .containsSequence("2", "3");
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractIterableAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractIterableAssert.html)
## 6. Character Assertions
문자에 대한 Assertion은 주로 다른 문자와 비교하거나 해당 문자가 Unicode 테이블에서 온 것인지 확인하는 작업이다.
```java
// 주어진 문자가 'a'가 아니며 Unicode 테이블에 있으며 'b'보다 크며 소문자인지 확인
assertThat(someCharacter)
  .isNotEqualTo('a')
  .inUnicode()
  .isGreaterThanOrEqualTo('b')
  .isLowerCase();
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractCharacterAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractCharacterAssert.html)
## 7. Class Assertions
Class에 대한 Assertion은 대부분 해당 필드, Class 유형, 어노테이션의 존재 및 클래스의 최종 여부를 확인하는 작업이다.
```java
// Runnable 클래스가 인터페이스인지 확인
assertThat(Runnable.class).isInterface();
```
또는 한 클래스가 다른 클래스로부터 할당 가능한지 확인하려면 다음과 같이 작성한다.
```java
assertThat(Exception.class).isAssignableFrom(NoSuchElementException.class);
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractClassAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractClassAssert.html)
## 8. File Assertions
File에 대한 Assertion은 주어진 File 인스턴스가 존재하고 디렉터리인지 파일인지, 특정 내용이 있는지, 읽기 가능한지, 특정 확장자를 가지는지를 확인한다.
```java
// 주어진 파일이 존재하며 파일이며 디렉터리가 아니며 읽기 및 쓰기 가능한지를 확인
assertThat(someFile)
   .exists()
   .isFile()
   .canRead()
   .canWrite();
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractFileAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractFileAssert.html)
## 9. Double/Float/Integer Assertions
### [Double/Float/Integer and Other Number Types]
숫자에 대한 Assertion은 주어진 offset 내외에서 숫자 값을 비교하는 작업과 관련이 있다.
```java
assertThat(5.1).isEqualTo(5, withPrecision(1d));
```
주목해야 할 점은 `withPrecision(Double offset)` 메서드를 사용하여 이미 가져온 Offset 객체를 생성하는 helper 메서드를 사용한다는 것이다.<br/>
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractDoubleAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractDoubleAssert.html)
## 10. InputStream Assertions
InputStream에 대한 Assertion은 하나뿐이다. : `hasSameContentAs(InputStream expected)`
```java
assertThat(given).hasSameContentAs(expected);
```
## 11. Map Assertions
Map Assertion을 사용하면 Map이 특정 항목, 항목 집합 또는 키/값을 개별적으로 포함하는지 확인할 수 있다.
```java
// 주어진 Map이 비어 있지 않고 숫자 키 "2"를 포함하며 숫자 키 "10"을 포함하지 않으며 (2,"a") Map.Entry를 포함하는지 확인
assertThat(map)
  .isNotEmpty()
  .containsKey(2)
  .doesNotContainKeys(10)
  .contains(entry(2, "a"));
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractMapAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractMapAssert.html)
## 12. Throwable Assertions
Throwable Assertion을 사용하면 예외(Exception) 메시지, stacktrace 검사, 원인 확인 또는 이미 예외가 발생했는지 확인하는 등의 작업이 가능하다.
```java
// 주어진 예외가 발생한 후 메시지가 "c"로 끝나는지 확인
assertThat(ex).hasNoCause().hasMessageEndingWith("c");
```
이 외에도 다양한 Assertion이 있다.
- [공식 AbstractThrowableAssert 문서](https://joel-costigliola.github.io/assertj/core-8/api/org/assertj/core/api/AbstractThrowableAssert.html)
<br/>

# Describing Assertions
더 정교한 검증을 위해서는 Assertion에 대해 동적으로 사용자 정의 설명을 생성할 수 있다. : `as(String description, Object… args)` 메소드
만약 다음과 같이 Assertion을 정의한다면:
```java
assertThat(person.getAge())
  .as("%s's age should be equal to 100", person.getName())
  .isEqualTo(100);
```
테스트를 실행할 때 다음과 같은 결과를 얻게 된다.
```java
[Alex's age should be equal to 100] expected:<100> but was:<34>
```
<br/>

# Java 8
AssertJ는 Java 8의 함수형 프로그래밍 기능을 최대한 활용한다.
```java
[Hobbit 종족을 기준으로 Collection을 필터링]

// Java 7
assertThat(fellowshipOfTheRing)
  .filteredOn("race", HOBBIT)
  .containsOnly(sam, frodo, pippin, merry);

// Java 8
assertThat(fellowshipOfTheRing)
  .filteredOn(character -> character.getRace().equals(HOBBIT))
  .containsOnly(sam, frodo, pippin, merry);
```
- reference : [https://joel-costigliola.github.io/assertj/](https://joel-costigliola.github.io/assertj/)
<br/>

# Conclusion
AssertJ가 제공하는 여러 기능과 핵심 Java 타입에 대한 가장 인기 있는 Assertion을 간략하게 살펴보았다.<br/>
모든 예제 및 코드 스니펫의 구현은 GitHub 프로젝트에서 찾을 수 있다.
