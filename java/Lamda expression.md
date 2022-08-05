# 람다식(Lambda expression)

- 자바 8부터 함수형 프로그래밍 방식을 지원하고 이를 람다식이라 함
- 함수의 구현과 호출 만으로 프로그래밍이 수행되는 방식



#### 람다식 문법

- 매개 변수와 매개변수를 이용한 실행문

```java
ind add(int x, int y) {
	return x+y;
}
```

- 람다식으로 표현

```java
(int x,int y) -> {return x+y;} 
```



- 매개 변수가 하나인 경우 자료형과 괄호 생략 가능

```java
str->{System.out.println(str);}
```



- 매개 변수가 두 개 이상인 경우 괄호를 생략할 수 없음

```java
x, y -> {System.out.println(x+y);} //오류
```



- 실행문이 한 문장인 경우 중괄호 생략 가능

```java
str-> System.out.println(str);
```



- 실행문이 한 문장이라도 return문(반환문)은 중괄호를 생략할 수 없음

```java
str-> return str.length();  //오류
```



- 실행문이 한 문장의 반환문인 경우엔 return과 중괄호를 모두 생략

```java
(x, y) -> x+y;
str -> str.length;
```



##### 함수적 인터페이스

- 람다식을 선언하기 위한 인터페이스
- 익명 함수와 매개 변수만으로 구현되므로 인터페이스는 단 하나의 메서드만을 선언해야함

- @FunctionalInterface 애노테이션(annotation)

```java
@FunctionalInterface
public interface MyFunctionalInterface {
    public void method();
    public void otherMethod(); // 컴파일 오류
}
```





































