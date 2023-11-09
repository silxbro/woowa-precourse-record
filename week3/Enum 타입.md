이전에 Enum 타입에 대해 학습했지만 ([Enum 타입](https://github.com/silxbro/java/blob/main/contents/thisisjava/ch05_%EC%B0%B8%EC%A1%B0-%ED%83%80%EC%9E%85/512_%EC%97%B4%EA%B1%B0(Enum)-%ED%83%80%EC%9E%85.md))<br/>
이번 미션에 적용하는 데 부족함을 느껴 좀 더 자세한 내용을 학습한 후 정리해 보았습니다.
<br/>

# Enum 타입
Enumeration(열거)의 앞 글자로, **서로 관련있는 한정된 상수들의 집합**을 말한다.

일반적으로 상수(constant)를 정의할 때는 static final을 사용하여 정의하지만 클래스 내에서 선언하는 부분은 네이밍이 겹칠 수 있고 불필요하게 상수가 많아진다는 단점이 발생한다.
또한 인터페이스로 관리하는 경우 이런 부분은 줄어들지만 여전히 IDE의 지원을 적극적으로 받을 수 없고 타입 안정성이 떨어지는 단점을 가지고 있다. 이를 보완하며 나온 것이 Enum이다.
<br/>
<br/>
## Enum 타입의 특징
### 1. 클래스를 상수처럼 사용할 수 있다. (동일한 문법 체계)
Default 생성자는 **`private`** 로 되어 있으며 `public`으로 변경하는 경우 컴파일 에러가 발생한다.<br/>
즉 Enum은 생성자가 존재하지만 상수와 같이 **클래스가 로드되는 시점에서 생성**되기 때문에 임의로 생성하여 사용할 수 없다.
`열거타입.열거상수`와 같은 형태로 이를 사용하면 된다.
### 2. 상수 값과 같이 유일하게 하나의 인스턴스로 사용된다.
클래스가 로드될 때 하나의 인스턴스로 생성되어 `싱글톤` 패턴을 간단하게 구현하는 데 사용된다.
따라서 각각의 Enum 인스턴스에 변수를 추가하여 사용하는 것은 Multi Thread 환경에서 위험할 수 있다.
### 3. 상속을 지원하지 않는다.
Enum 클래스는 내부적으로 `java.lang.enum` 클래스에 의해 상속되기 때문에 다른 클래스를 상속받을 수 없다. (다중상속 불가)
<br/>
<br/>
## Enum 타입의 메소드

|리턴 타입|메소드|설명|
|:---|:---|:---|
|String|**name**()|열거형 상수의 이름을 문자열로 반환|
|int|**ordinal**()|열거형 상수의 순서(0부터 시작)를 반환|
|<T extends Enum<T>>[]|**values**()|열거형 상수의 배열을 반환|
|<T extends Enum<T>>|**valueOf**(String name)|주어진 이름에 해당하는 열거형 상수를 반환|
|String|**toString**()|열거형 상수의 이름을 문자열로 반환<br/>name() 메소드와 동일한 결과를 반환|
|boolean|**equals**(Object obj)|열거형 상수를 비교하여 두 개의 열거형 상수가 동일한지 여부를 반환<br/>열거형은 보통 `==` 연산자를 사용하여 비교|
|int|**compareTo**(EnumType o)|다른 열거형 상수와 비교하여 순서를 반환<br/>일반적으로 ordinal() 값을 비교하는 방식으로 작동|
|int|**hashCode**()|열거형 상수의 해시 코드를 반환|
|Class<E>|**getDeclaringClass**()|열거형 상수가 속한 열거형 클래스를 반환|
<br/>

## Enum 타입의 장점
- 코드가 단순해지며, 가독성이 좋아진다.
- 인스턴스 생성과 상속을 방지하고 허용 가능한 값들을 제한할 수 있어 타입 안정성(type safe)이 보장된다.
- switch문에서도 사용할 수 있다.
- 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 나타낼 수 있다.
- IDE의 적극적인 지원을 받을 수 있다. (자동완성, 오타검증, 텍스트 리팩토링 등등)
- 데이터의 그룹화 및 관리에 용이하고 리팩토링 시 변경 범위가 최소화된다. (Enum에서 한번에 관리)
- 본질적으로 Thread safe인 싱글톤 객체이므로 싱글톤 클래스를 생성하는데에도 사용된다.
<br/>

## Java Enum과 다른 언어의 enum
각 언어에서 enum을 표현하는 방법은 각각 다르다. C/C++의 경우 enum이 int값이다.
- C
  - struct나 union과 같은 형태로 enum 정의
  - 상수가 내부에서 int형으로 저장되므로 산술 연산 가능
- C++
  - C와 비슷한 특징을 가지나, C++에서는 그 자체가 실제 타입으로 다루어짐
  - C++11부터 타입 안정성(type safe)을 더욱 강력하게 보장

Java의 Enum은 완전한 기능을 갖춘 클래스이다.
- 데이터들 간의 연관관계 표현
- 상태와 행위를 한곳에서 관리
- 데이터 그룹관리
- 관리 주체를 DB에서 객체로
<br/>

# Reference
> [Java Enum 공식 문서](https://docs.oracle.com/javase/7/docs/api/java/lang/Enum.html)
> 
> [Java Enum 기본 및 활용](https://velog.io/@kyle/%EC%9E%90%EB%B0%94-Enum-%EA%B8%B0%EB%B3%B8-%EB%B0%8F-%ED%99%9C%EC%9A%A9)
> 
> [Java enum 이란?](https://limkydev.tistory.com/50)
>
> [열거형Enum-타입-문법-활용-정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%97%B4%EA%B1%B0%ED%98%95Enum-%ED%83%80%EC%9E%85-%EB%AC%B8%EB%B2%95-%ED%99%9C%EC%9A%A9-%EC%A0%95%EB%A6%AC)
>
> [Java Enum 활용기](https://techblog.woowahan.com/2527/)
