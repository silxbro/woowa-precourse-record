# Test코드 - StringTest
<br/>

`test/java/study/StringTest` 클래스 학습 내용을 정리한 자료입니다.

---
## 1. assertThat() - contains(), containsOnly(), containsExactly()
- String, Array, Set, List 모두 사용 가능
- `assertThat(비교대상 자료구조).containsXXX(원소1, 원소2, 원소3, ..)` 형식으로 사용
```java
@Test
void split_메서드로_주어진_값을_구분() {
  String input = "1,2";
  String[] result = input.split(",");

  assertThat(result).contains("2", "1");
  assertThat(result).containsExactly("1", "2");
}

@Test
void split_메서드_사용시_구분자가_포함되지_않은_경우_값을 그대로 반환() {
  String input = "1";
  String[] result = input.split(",");

  assertThat(result).contains("1");
}
```
➡️ split() 함수가 매개값으로 주어진 구분자로 문자열을 구분하였을 때 올바른 값으로 구분하는지 검증하는 테스트 코드이다.

### [contains()]
원소의 중복여부, 순서에 관계 없이 값만 일치하면 테스트가 성공한다.
- ```java
  void containsTest() {
    List<Integer> list = Arrays.asList(1, 2, 3);

    // Success: 모든 원소를 입력하지 않아도 성공
    assertThat(list).contains(1, 2);

    // Success: 중복된 값이 있어도 포함만 되어 있으면 성공
    assertThat(list).contains(1, 2, 2);

    // Success: 순서가 바뀌어도 값만 맞으면 성공
    assertThat(list).contains(3, 2);

    // Fail: List 에 없는 값을 입력하면 실패
    assertThat(list).contains(1, 2, 3, 4);
  }
  ```
### [containsExactly()]
원소가 정확히 일치해야 테스트가 성공한다. 값과 그 순서가 모두 일치해야 하며, 중복을 허용하지 않는다.<br/>
특정 자료구조의 정확한 값을 테스트 하고 싶은 경우에 사용한다.
- ```java
  /*
   * containsExactly 실패 케이스
   *
   * assertThat(list).containsExactly(1, 2);       -> 원소 3 이 일치하지 않아서
   * assertThat(list).containsExactly(3, 2, 1);    -> list 의 순서가 달라서 실패
   * assertThat(list).containsExactly(1, 2, 3, 3); -> list 에 중복된 원소가 있어서 실패
   */
  @Test
  void containsExactlyTest() {
      List<Integer> list = Arrays.asList(1, 2, 3);

      assertThat(list).containsExactly(1, 2, 3);
  }
  ```
### [containsOnly()]
contains()와 동일하게 원소의 중복여부, 순서를 무시하나, 원소값과 갯수가 정확히 일치해야 테스트가 성공한다.
- ```java
  /*
   * containsOnly 실패 케이스
   *
   * assertThat(list).containsOnly(1, 2);       -> 원소 3 이 일치하지 않아서 실패
   * assertThat(list).containsOnly(1, 2, 3, 4); -> 원소 4 가 일치하지 않아서 실패
   */
  @Test
  void containsOnlyTest() {
      List<Integer> list = Arrays.asList(1, 2, 3);

      assertThat(list).containsOnly(1, 2, 3);
      assertThat(list).containsOnly(3, 2, 1);
      assertThat(list).containsOnly(1, 2, 3, 3);
  }
  ```
---
## 2. isEqualTo(), isSameTo()
- `assertThat(비교값).isEqualTo(기댓값) / assertThat(비교대상).isSameTo(기대대상)` 형식으로 사용
```java
@Test
void charAt_메서드로_특정_위치의_문자_찾기() {
  String input = "abc";
  char charAtElement = input.charAt(0);
  assertThat(charAtElement).isEqualTo('a');
}
```
➡️ charAt() 함수가 매개값으로 주어진 위치의 문자를 올바른 값으로 반환하는지 검증하는 테스트 코드이다.

### [isEqualTo()]
isEqualTo()는 java의 `==` 연산과 같은 방식으로 이루어지며, 기댓값이 상수일 때 동일한 값(value)인지 확인한다.

### [isSameTo()]
isSameTo()는 비교대상과 기대대상이 같은 대상인지 주소값을 통해 확인한다.

- ```java
  @Test
  void test(){
      Member member1 = new Member(1L, "a", Grade.VIP);
      Member member2 = new Member(1L, "a", Grade.VIP);

      // isEqualTo는 ==, isSameAs는 ref 비교
      Assertions.assertThat(member1).isEqualTo(member2);
  }
  ```
---
## 3. assertThatThrownBy()
Exception이 발생하는 케이스를 테스트할 때 사용
```java
@Test
void charAt_메서드_사용시_문자열의_길이보다_큰_숫자_위치의_문자를_찾을_때_예외_발생() {
  String input = "abc";

  assertThatThrownBy(() -> input.charAt(5))
          .isInstanceOf(StringIndexOfOutOfBoundsException.class)
          .hasMessageContaining("String index out of range: 5");
}
```
➡️ charAt() 함수가 문자열의 길이보다 큰 숫자(위치)가 매개값으로 주어졌을 때 Exception(예외)을 알맞게 발생시키는지 검증하는 테스트 코드이다.

- parameter: Exception이 발생하는 메서드를 람다식으로 입력
- chaining
  - `isInstanceOf`: 예상되는 Exception을 .class 형태로 입력
  - `hasMessageContaining`: Exception 메시지에 입력되는 문자열이 포함되는지 확인
