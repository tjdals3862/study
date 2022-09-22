# javascript 기초



#### 자바스크립트(javascript)란

자바스크립트(JavaScript)는 객체(object) 기반의 스크립트 언어입니다.

HTML로는 웹의 내용을 작성하고, CSS로는 웹을 디자인하며, 자바스크립트로는 웹의 동작을 구현할 수 있습니다.

자바스크립트는 주로 웹 브라우저에서 사용되나, Node.js와 같은 프레임워크를 사용하면 서버 측 프로그래밍에서도 사용할 수 있습니다.

현재 컴퓨터나 스마트폰 등에 포함된 대부분의 웹 브라우저에는 자바스크립트 인터프리터가 내장되어 있습니다.



#### 자바스크립트의 특징

1. 자바스크립트는 객체 기반의 스크립트 언어입니다.

2. 자바스크립트는 동적이며, 타입을 명시할 필요가 없는 인터프리터 언어입니다.

3. 자바스크립트는 객체 지향형 프로그래밍과 함수형 프로그래밍을 모두 표현할 수 있습니다.



#### 자바스크립트 출력

##### window.alert() 메소드

- window.alert() 메소드는 브라우저와는 별도의 대화 상자를 띄워 사용자에게 데이터를 전달해 줍니다

```javascript
<script>
    function alertDialogBox() {
        alert("확인을 누를 때까지 다른 작업을 할 수 없어요!");
    }
</script>
```



##### HTML DOM 요소를 이용한 innerHTML 프로퍼티

```javascript
<script>
    var str = document.getElementById("text");
    str.innerHTML = "이 문장으로 바뀌었습니다!";
</script>
```



##### document.write() 메소드

- document.write() 메소드는 웹 페이지가 로딩될 때 실행되면, 웹 페이지에 가장 먼저 데이터를 출력합니다.

```javascript
<script>
    document.write(4 * 5);
</script>
```



##### console.log() 메소드

- console.log() 메소드는 웹 브라우저의 콘솔을 통해 데이터를 출력

```javascript
<script>
    console.log(4 * 5);
</script>
```





