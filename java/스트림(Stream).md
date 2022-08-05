# 스트림(Stream)

- 자바 8부터 추가된 컬렉션(배열 포함)의 저장 요소를 하나씩 참조해서 람다식으로 처리할 수 있도록 해주는 반복자

- 스트림은 외부 반복을 통해 작업하는 컬렉션과는 달리 내부 반복(internal iteration)을 통해 작업을 수행합니다.
- 스트림은 재사용이 가능한 컬렉션과는 달리 단 한 번만 사용할 수 있습니다.

- 스트림은 원본 데이터를 변경하지 않습니다.
- 스트림의 연산은 필터-맵(filter-map) 기반의 API를 사용하여 지연(lazy) 연산을 통해 성능을 최적화 합니다.
- 스트림은 parallelStream() 메소드를 통한 손쉬운 병렬 처리를 지원합니다. 



##### 스트림 API의 동작 흐름

1. 스트림의 생성
2. 스트림의 중개 연산(스트림의 변환)
3. 스트림의 최종 연산(스트림의 사용)



### 스트림 중개 연산(itermediate operation)

- 스트림 필터링 :filter(), distinct()
- 스트림 변환 : map(), flatMap()
- 스트림 제한 : limit(), skip()
- 스트림 정렬 : sorted()
- 스트림 연산 결과 확인 : peek()



#### 필터링(distinct(), filter())

- 중간 처리  기능으로 요소를 걸러내는 역할

| 리턴 타입                                  | 메소드(매개 변수)       | 설명        |
| ------------------------------------------ | ----------------------- | ----------- |
| Stream, InStream, LongStream, DoubleStream | distinct()              | 중복 제거   |
|                                            | filter(Predicate)       | 조건 필터링 |
|                                            | filter(IntPredicate)    |             |
|                                            | filter(LongPredicate)   |             |
|                                            | filter(DoublePredicate) |             |



예제)

```java
public class FilteringExample {

	public static void main(String[] args) {

		List<String> names = Arrays.asList("홍길동","신용권","감자바","신용권", "신민철");
		
		names.stream()
            .distinct() // 중복 제거
            .forEach(n -> System.out.println(n));
		System.out.println();
		
		names.stream()
            .filter(n -> n.startsWith("신")) // 필터링
            .forEach(n -> System.out.println(n));
		System.out.println();
		
		names.stream()
            .distinct() // 중복 제거
            .filter(n->n.startsWith("신")) // 필터링
            .forEach(n->System.out.println(n));       
			
	}

}
```



#### 매핑(flatMap, map, asStream, boxed)

- 중간 처리 기능으로 스트림의 요소를 다른 요소로 대체하는 작업



##### flatMap 메소드

- 요소를 대체하는 복수 개의 요소들로 구성된 새로운 스트림을 리턴 한다.

```java
	public static void main(String[] args) {

		List<String> inputList1 = Arrays.asList("java8 lambda","Stream mapping");
		inputList1.stream()
		.flatMap(data -> Arrays.stream(data.split(" ")))
		.forEach(word -> System.out.println(word));
	}

// 결과
java8
lambda
Stream
mapping
```

| 리턴 타입    | 메소드(매개 변수)                         | 요소 -> 대체 요소     |
| ------------ | ----------------------------------------- | --------------------- |
| Stream<R>    | flatMap(Function<T.Stream<R>>)            | T -> Stream<R>        |
| DoubleStream | flatMap(DoubleFunction<DoubleStream>)     | double -> DoubleSteam |
| IntStream    | flatMap(IntFuction<IntStream>)            | int -> IntStream      |
| LongStream   | flatMap(LongFuction<LongStream>)          | long -> LongStream    |
| DoubleStream | flatMapToDouble(Function<T.DoubleStream>) | T -> DoubleStream     |
| IntStream    | flatMapToInt(Function<T.IntStream>)       | T -> IntStream        |
| LongStream   | flatMapToLong(Fuction<T.LongStream>)      | T -> LongStream       |



##### map 메소드

- 요소를 대체하는 요소로 구성된 새로운 스트림을 리턴 한다.

| 리턴 타입    | 메소드(매개 변수)                  | 요소 -> 대체 요소 |
| ------------ | ---------------------------------- | ----------------- |
| Stream<R>    | map(Fuction<T,R>)                  | T -> R            |
| DoubleStream | mapToDouble(ToDoubleFuction<T>)    | T -> Double       |
| IntStream    | mapToInt(ToIntFution<T>)           | T -> int          |
| LongStream   | mapToLong(ToLongFuction<T>)        | T -> long         |
| DoubleStream | map(DoubleUnaryOperator)           | double -> double  |
| IntStream    | mapToInt(DoubleToIntFuction)       | double -> int     |
| LongStream   | mapToLong(DoubleToLongFuction)     | double -> long    |
| Stream<U>    | mapToOjb(DoubleFuction<U>)         | double -> U       |
| IntStream    | map(IntUnaryOperator mapper)       | int -> int        |
| DoubleStream | mapToDouble(IntToDoubleFuction)    | int -> double     |
| LongStream   | mapToLong(IntToLongFuction mapper) | int -> long       |
| Stream<U>    | mapToObject(IntFuction<U>)         | int -> U          |
| LongStream   | map(LongUnaryOperator)             | long -> long      |
| DoubleStream | mapToDouble(LongToDoubleFuction)   | long -> double    |
| IntStream    | mapToInt(LongToIntFuction)         | long -> int       |
| Stream<U>    | mapToObj(LongFuction)              | long -> U         |



#### 정렬(Sort())

- 스트림 요소가 최종 처리되기 전에 중간 단계에서 요소를 정렬해 최종 처리 순서를 변경

| 리턴 타입    | 메소드(매개 변수)     | 설명                                    |
| ------------ | --------------------- | --------------------------------------- |
| Stream<T>    | sorted()              | 객체를 Comparable 구현 방법에 따라 정렬 |
| Stream<T>    | sorted(Comparator<T>) | 객체를 주어진 Comparator에 따라 정렬    |
| DoubleStream | sorted()              | double 요소를 오름차순으로 정렬         |
| IntStream    | sorted()              | int 요소를 오름차순으로 정렬            |
| LongStream   | sorted()              | long 요소를 오름차순으로 정렬           |





#### 루핑(peek(), forEach())

- 전체 요소를 반복
- peek() : 중간 처리 메소드
- forEach : 최종 처리 메소드

```java
int[] intArr = {1,2,3,4,5};

Arrays.stream(intArr)
    .filter(a -> a%2==0)
    .peek(n -> System.out.println(n)); // 동작하지 않음

int total = Arrays.stream(intArr)
    .filter(a -> a%2==0)
    .peek(n -> System.out.println(n)) // 동작함
    .sum();							  // 최종 메소드

Arrays.stream(intArr)
    .filter(a -> a%2==0)
    .forEach(n -> System.out.println(n)); // 최종 메소드로 동작함
```



#### 매칭(allMatch(), anyMatch(), noneMatch())

- 최종 처리 단계에서 요소들이 특정 조건에 만족하는지 조사할 수 있도록 매칭 메소드 제공

- allMatch() : 모든 요소들이 매개 값으로 주어진 Predicate의 조건을 만족하는지 조사
- anyMatch() : 최소한 한 개의 요소가 매개 값으로 주어진 Predicate의 조건을 만족하는지 조사
- noneMatch() : 모든 요소들이 매개 값으로 주어진 Predicate의 조건을 만족하지 않는지 조사



#### 기본 집계

| 리턴 타입         | 메소드(매개 변수)         | 설명         |
| ----------------- | ------------------------- | ------------ |
| long              | count()                   | 요소 개수    |
| OptionalXXX       | findFirst()               | 첫 번째 요소 |
| Optional<T>       | max(Comparator<T>), max() | 최대 요소    |
| Optional<T>       | min(Comparator<T>), min() | 최소 요소    |
| OptionalDouble    | average()                 | 요소 평균    |
| int, long, double | sum()                     | 요소 총합    |



#### 수집(collect())

- 요소들을 필터링 또는 매핑한 후 요소들을 수집하는 최종 처리 메소드 제공
- 필요한 요소만 컬렉션에 담을 수 있고, 요소들을 그룹핑한 후 집계할 수 있다.

| 리턴 타입 | 메소드(매개 변수)                    | 인터페이스 |
| --------- | ------------------------------------ | ---------- |
| R         | collect(Collector<T,A,R> collector ) | Stream     |

- T : 요소 A : 누적기(accumulator) R : 요소가 저장될 컬렉션

-> T요소를 A누적기가 R에 저장

| 리턴 타입                           | Collectors의 정적 메소드                                     | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Collector<T, ?, List<T>>            | toList()                                                     | T를 List에 저장                                              |
| Collector<T, ?, Set<T>>             | toSet()                                                      | T를 Set에 저장                                               |
| Collector<T, ?, Collection<T>>      | toCollection( Supplier<Collection<T>>)                       | T를 Supplier가제공한 Collection에 저장                       |
| Collector<T, ?. Map<K,U>>           | toMap(Fuction<T,K> keyMapper, Fuction<T,U> valueMapper)      | T를 K와 U로 매핑해서 K를 키로, U를 값으로 Map에 저장         |
| Collector<T, ?, ConcurrentMap<K,U>> | toConcurrentMap(Fuction<T,K> keyMapper, Fuction<T,U> valueMapper) | T를 K와 U로 매핑해서 K를 키로, U를 값으로 ConcurrentMap에 저장 |





























