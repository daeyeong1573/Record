# IntArray

배열을 사용하다 보면 처음에 크기를 지정안하고 사용할 경우가 생긴다.
하지만 배열은 사이즈를 처음에 지정해야 하며 사이즈는 바뀔수가 없습니다.

하지만 코틀린에는 IntArray 클래스의 plus + 연산자를 재정의한 함수가 있어 += 연산자를 사용하여 값을 추가 할 수 있습니다.

```kotlin

var intArr : IntArray = intArrayOf()
(0..10).map { intArr += it }
print(intArr.contentToString())

```
### 실행결과
![실행 결과](../img/IntArrayResult.png)<br>