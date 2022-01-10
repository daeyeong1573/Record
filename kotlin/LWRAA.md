코틀린에는 let,with,run,apply,also등의 확장 함수가 있습니다.<br>
위 5개의 함수는 잘 모른다면 비슷한 함수처럼 보여서 헷갈리는 경우가 많아 이번 기회에 정리해봅니다.

먼저 일반적인 사용방식을 봐보겠습니다.

```kotlin
data class Student(var name: String, var studentId: Int)

val student = Student("", 0)
student.name = "김대영"
student.studentId = 2403
println("$person")

// 결과값(김대영,2403) 
```
**Student** 객체의 **name**과 **studentId**를 각각 호출해주는데, 이러한 부분을 블럭``{}``으로 묶어서 간결한 코드로 정리할 수 있습니다.



먼저 **let** 방식을 살펴 보겠습니다.<br>
코틀린의 let을 타고 들어가보면 아래와 같이 나옵니다.
```kotlin
public inline fun <T, R> T.let(block: (T) -> R): R {
    contract {
        callsInPlace(block, InvocationKind.EXACTLY_ONCE)
    }
    return block(this)
}
```
**let** 함수는 매개변수화된 타입 T의 확장 함수입니다. 자기 자신을 받아서 R을 반환하는((T) -> R) 람다 식을 입력으로 받고, 블럭 함수의 반환값 R을 반환한다. 여기서는 Student 클래스의 확장 함수로 사용되어 student.let 의 형태가 가능해집니다.

ex)
```kotlin
    val student = Student("",0)

    val st1 = student.let {
        it.name = "김대영"
        it.studentId = 2403
        it
    }

    val st2 = student.let {
        it.name = "김대영"
        it.studentId = 2403
    }

    val st3 = student.let {
        it.name = "김대영"
        it.studentId = 2403
        "${it.name} is ${it.studentId}"
    }

    println(st1)
    println(st2)
    println(st3)
    
    //결과값
    Student(name=김대영, studentId=2403)
    kotlin.Unit // 리턴값을 주지않아 값이 제대로 나오지 않는걸 확인 가능합니다.
    김대영 is 2403

```

2.with
with 함수를 타고 들어가면 아래와 같은 with함수의 형태를 확인할 수 있다.
```kotlin
public inline fun <T, R> with(receiver: T, block: T.() -> R): R {
    contract {
        callsInPlace(block, InvocationKind.EXACTLY_ONCE)
    }
    return receiver.block()
}
```
**with**는 일반 함수이기 때문에 객체 **receive**를 직접 입력받고, 객체를 사용하기 위한 두 번째 파라미터 블럭을 받는다. T.()를 람다 리시버라고 하는데, 입력을 받으면 함수 내에서 this를 사용하지 않고도 입력받은 객체(receiver)의 속성을 변경할 수 있습니다.

간단하 예시로 아래와 같은 방법이 있습니다.
```kotlin
fun test() = with(binding){
    //기존 binding 방식
    binding.id

    //with을 사용한 binding
    id
}
```

```kotlin
    val student = Student("김대영",2403)
    with(student){
         println(name)
         println(studentId)
         //자기자신을 반환해야 할 경우 it이 아닌 this를 사용하여 반환해야 합니다.
    }

    //결과값
    김대영
    2403    

```