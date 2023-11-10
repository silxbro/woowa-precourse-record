# 🗃️ 학습테스트를 통해 JUnit 학습하기
테스트 도구를 학습하고, 개발공부의 학습 도구로서 사용하고자 실습한 내용을 기록하였습니다.
<br/>

## 📌 학습 테스트 진행 방식
- import한 저장소의 `src/test/java` 학습 테스트를 위한 패키지를 생성한다. (ex: study)
- 단위 테스트를 위한 클래스 명명 규칙("테스트 대상 클래스명 + Test")에 따라 클래스를 생성한다.
- 다음 요구사항을 구현하면서 **JUnit**과 **AssertJ** 사용법을 익힌다.
- JUnit의 `@DisplayName`을 활용해 테스트 메소드의 의도를 드러낸다.
<br/>

---
# String 클래스에 대한 학습 테스트
## 1. split()
- "1,2"을 `,` 로 split 했을 때 1과 2로 잘 분리되는지 확인하는 학습 테스트
  
  ```java
  @DisplayName("\"1,2\"을 ,로 split 했을 때 1과 2로 잘 분리되는지 확인")
  @Test
  void split_메소드로_주어진_값을_구분() {
      String input = "1,2";
      String[] result = input.split(",");

      assertThat(result).contains("2", "1");
      assertThat(result).containsExactly("1", "2");
  }
  ```
- "1"을 `,` 로 split 했을 때 1만을 포함하는 배열이 반환되는지에 대한 학습 테스트

  ```java
  @DisplayName("메소드 사용시 구분자가 포함되지 않은 경우 값을 그대로 반환")
  @Test
  void split_메소드_사용시_구분자가_포함되지_않은_경우_값을_그대로_반환() {
      String input = "1";
      String[] result = input.split(",");

      assertThat(result).contains("1");
  }
  ```

## 2. substring()
- "(1,2)" 값이 주어졌을 때 String의 substring() 메소드를 활용해 () 을 제거하고 "1,2"를 반환하는지에 대한 학습 테스트

  ```java
  @DisplayName("substring 메서드로 특정 구간 값을 반환")
  @Test
  void substring_메서드로_특정_구간_값을_반환() {
      String input = "(1,2)";
      String result = input.substring(1, 4);

      assertThat(result).isEqualTo("1,2");
  }
  ```

## 3. charAt()
- "abc" 값이 주어졌을 때 String의 charAt() 메소드를 활용해 특정 위치의 문자를 가져오는 학습 테스트

  ```java
  @DisplayName("charAt 메서드로 특정 위치의 문자 찾기")
  @Test
  void charAt_메서드로_특정_위치의_문자_찾기() {
      String input = "abc";
      char result = input.charAt(0);

      assertThat(result).isEqualTo('a');
  }
  ```
- String의 charAt() 메소드를 활용해 특정 위치의 문자를 가져올 때 위치 값을 벗어나면 `StringIndexOutOfBoundsException`이 발생하는 부분에 대한 학습 테스트

  ```java
  @DisplayName("charAt 메서드 사용시 문자열의 길이보다 큰 숫자 위치의 문자를 찾을 때 예외 발생")
  @Test
  void charAt_메서드_사용시_문자열의_길이보다_큰_숫자_위치의_문자를_찾을_때_예외_발생() {
      String input = "abc";

      assertThatThrownBy(() -> input.charAt(5))
              .isInstanceOf(StringIndexOutOfBoundsException.class)
              .hasMessageContaining("String index out of range: 5");
  }
  ```
  ```java
  @DisplayName("charAt 메서드 사용시 문자열의 길이보다 큰 숫자 위치의 문자를 찾을 때 예외 발생")
  @Test
  void charAt_메서드_사용시_문자열의_길이보다_큰_숫자_위치의_문자를_찾을_때_예외_발생_2() {
  String input = "abc";

  assertThatExceptionOfType(StringIndexOutOfBoundsException.class).isThrownBy(() -> input.charAt(5))
              .withMessageContaining("String index out of range: 5");
  }
  ```
  - #### 자주 발생하는 Exception의 경우 Exception별 메서드 제공하고 있음
    - assertThatIllegalArgumentException()
    - assertThatIllegalStateException()
    - assertThatIOException()
    - assertThatNullPointerException()
<br/>

# Set Collection에 대한 학습 테스트
## 1. size()
- Set의 size() 메소드를 활용해 Set의 크기를 확인하는 학습테스트

  ```java
  @DisplayName("size 메소드 사용시 Set의 크기를 반환")
  @Test
  void size_메소드_사용시_Set의_크기를_반환() {
      int result = numbers.size();

      assertThat(result).isEqualTo(3);
  }
  ```
- Set의 contains() 메소드를 활용해 1, 2, 3의 값이 존재하는지를 확인하는 학습테스트
  - JUnit의 `ParameterizedTest`를 활용해 중복 코드를 제거해 본다.
 
    ```java
    @DisplayName("contains 메소드 사용시 해당 원소의 존재 여부를 반환")
    @ParameterizedTest
    @ValueSource(ints = {1,2,3})
    void contains_메소드_사용시_해당_원소의_존재_여부를_반환(int number) {
        assertTrue(numbers.contains(number));
    }
    ```
- Set의 contains() 메소드를 활용해 1, 2, 3 값은 존재, 4, 5의 값은 존재하지 않는지를 확인하는 학습테스트 (입력 값에 따라 결과 값이 다른 경우에 대한 테스트)
  - `@CsvSource`를 활용해 본다.

    ```java
    @DisplayName("contains 메소드 사용시 해당 원소가 존재할 경우 존재, 존재하지 않을 경우 존재하지 않음을 반환")
    @CsvSource(value = {"1:true", "2:true", "3:true", "4:false", "5:false"}, delimiter = ':')
    void contains_메소드_사용시_해당_원소의_존재_여부에_따른_결과를_반환(int input, boolean expected) {
        boolean actualValue = numbers.contains(input);
        assertEquals(expected, actualValue);
    }
    ```
