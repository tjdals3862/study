# Java 용어정리



##### 함수(fuction)

- 하나의 기능을 수행하는 일련의 코드
- 구현된(정의된) 함수는 호출하여 사용하고 호출된 함수는 기능이 끝나면 제어가 반환됨
- 함수로 구현된 하나의 기능은 여러 곳에서 동일한 방식으로 호출되어 사용될 수 있음

```java
int add(int num1, int num2) {		
	int result;
	result = num1 + num2;
	return result;
}
```



##### 메서드(method)

- 객체의 기능을 구현하기 위해 클래스 내부에 구현되는 함수

- 멤버 함수(member function)이라고도 함

- 메서드를 구현함으로써 객체의 기능이 구현 됨

- 메서드의 이름은 그 객체를 사용하는 객체(클라이언트)에 맞게 짓는것이 좋음

  예) getStudentName()



##### 인스턴스(instance)

- 클래스는 객체의 속성을 정의 하고, 기능을 구현하여 만들어 놓은 코드 상태
- 실제 클래스 기반으로 생성된 객체(인스턴스)는 각각 다른 멤버 변수 값을 가지게 됨
- new 키워드를 사용하여 인스턴스 생성



##### 힙 메모리

- 생성된 인스턴스는 동적 메모리(heap memory)에 할당 됨
- 자바에서 Gabage Collector가 주기 적으로 사용하지 않는 메모리를 수거
- 하나의 클래스로 부터 여러개의 인스턴스가 생성되고 각각 다른 메모리 주소를 가지게 됨



##### 용어정리

| 용어      | 설명                                                |
| --------- | --------------------------------------------------- |
| 객체      | 객체 지향 프로그램의 대상, 생성된 인스턴스          |
| 클래스    | 객체를 프로그래밍 하기위해 코드로 정의해 놓은 상태  |
| 인스턴스  | new 키워드를 사용하여 클래스를 메모리에 생성한 상태 |
| 멤버 변수 | 클래스의 속성, 특성                                 |
| 메서드    | 멤버 변수를 이용하여 클래스의 기능을 구현한 함수    |
| 참조 변수 | 메모리에 생성된 인스턴스를 가리키는 변수            |
| 참조 값   | 생성된 인스턴스의 메모리 주소 값                    |



##### 생성자(constructor)

- 생성자 기본 문법 <class_name>([<argument_list]) { [<statements] }
- 객체를 생성할 때 new 키워드와 함께 사용   - new Student();
- 생성자는 일반 함수처럼 기능을 호출하는 것이 아니고 객체를 생성하기 위해 new 와 함께 호출 됨
- 객체가 생성될 때 변수나 상수를 초기화 하거나 다른 초기화 기능을 수행하는 메서드를 호출 함
- 생성자는 반환 값이 없고, 클래스의 이름과 동일
- 대부분의 생성자는 외부에서 접근 가능하지만, 필요에 의해 private 으로 선언되는 경우도 있음



##### 기본 생성자(default constructor)

- 클래스에는 반드시 적어도 하나 이상의 생성자가 존재

- 클래스에 생성자를 구현하지 않아도 new 키워드와 함께 생성자를 호출할 수 있음

- 클래스에 생성자가 하나도 없는 경우 컴파일러가 생성자 코드를 넣어 줌

  public Student(){}

- 매개 변수가 없음, 구현부가 없음





##### 접근 제어 지시자(access modifier)

- 클래스 외부에서 클래스의 멤버 변수, 메서드, 생성자를 사용할 수 있는지 여부를 지정하는 키워드
- private : 같은 클래스 내부에서만 접근 가능 ( 외부 클래스, 상속 관계의 클래스에서도 접근 불가)
- 아무것도 없음 (default) : 같은 패키지 내부에서만 접근 가능 ( 상속 관계라도 패키지가 다르면 접근 불가)
- protected : 같은 패키지나 상속관계의 클래스에서 접근 가능하고 그 외 외부에서는 접근 할 수 없음
- public : 클래스의 외부 어디서나 접근 할 수 있음



##### get() / set() 메서드

- private 으로 선언된 멤버 변수 (필드)에 대해 접근, 수정할 수 있는 메서드를 public으로 제공
- get() 메서드만 제공 되는 경우 read-only 필드
- 이클립스에서 자동으로 생성됨

 

##### 상속

##### IS-A 관계(is a relationship : inheritance)

- 일반적인(general) 개념과 구체적인(specific) 개념과의 관계
- 상위 클래스 : 하위 클래스보다 일반적인 개념
- 하위 클래스 : 상위 클래스보다 구체적인 개념들이 더해짐
- 상속은 클래스간의 결합도가 높은 설계
- 계층구조가 복잡하거나 hierarchy가 높으면 좋지 않음



##### HAS-A 관계(composition)

- 클래스가 다른 클래스를 포함하는 관계(변수로 선언)
- 코드 재사용의 가장 일반적인 방법
- Student가 Subject를 포함하는
- Library를 구현할 때 ArrayList 생성하여 사용
- 상속하지 않음



##### 추상클래스란?

- 구현 코드 없이 메서드의 선언만 있는 추상 메서드(abstract method)를 포함한 클래스
- 메서드 선언(declaration) : 반환타입, 메서드 이름, 매개변수로 구성
- 메서드 정의(definition) : 메서드 구현(implementation)과 동일한 구현부를 가짐({})
- abstract 예약어를 사용
- 추상 클래스는 new 할 수 없음(인스턴스화 할 수 없음)



##### 추상 클래스 구현하기

- 메서드에 구현 코드가 없으면 abstract 로 선언
- abstract로 선언된 메서드를 가진 클래스는 abstract로 선언
- 모든 메서드가 구현 된 클래스라도 abstract로 선언되면 추상 클래스로 인스턴스화 할 수 없음
- 추상 클래스의 추상 메서드는 하위 클래스가 상속 하여 구현
- 추상 클래스 내의 추상 메서드 : 하위 클래스가 구현해야 하는 메서드
- 추상 클래스 내의 구현 된 메서드 : 하위 클래스가 공통으로 사용하는 메서드 ( 필요에 따라 하위 클래스에서 재정의 함 )



##### 인터페이스가 하는 일

- 클래스나 프로그램이 제공하는 기능을 명시적으로 선언
- 일종의 클라이언트 코드와의 약속이며 클래스나 프로그램이 제공하는 명세(specification)
- 클라이언트 프로그램은 인터페이스에 선언된 메서드 명세만 보고 이를 구현한 클래스를 사용할 수 있음
- 어떤 객체가 하나의 인터페이스 타입이라는 것은 그 인터페이스가 제공하는 모든 메서드를 구현했다는 의미임
- 인터페이스를 구현한 다양한 객체를 사용함 - 다형성













