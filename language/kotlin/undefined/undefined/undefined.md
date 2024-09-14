---
description: 함수를 정리한 내용입니다.
---

# 함수

기본 파라미터값과 이름 있는 인자

{% tabs %}
{% tab title="code" %}
```kotlin
fun printMessage(message: String): Unit { // 1
    println(message)
}

fun printMessageWithPrefix(message: String, prefix: String = "info") { // 2
    println("[$prefix] $message")
}

fun sum(x: Int, y: Int): Int { // 3
    return x + y
}

fun multiply(x: Int, y: Int) = x * y // 4

fun main() {
    printMessage("Hello") // 5
    printMessageWithPrefix("Hello", "Log") // 6
    printMessageWithPrefix("Hello") // 7
    printMessageWithPrefix(prefix = "Log", message = "Hello") // 8
    println(sum(1, 2)) // 9
    println(multiply(2, 4)) // 10
}
```
{% endtab %}
{% endtabs %}

<table><thead><tr><th width="75.5">번호</th><th>내용</th></tr></thead><tbody><tr><td>1</td><td><code>String</code> 타입의 파라미터를 하나 받고 Unit을 반환한다.<br><code>Unit</code>은 반환할 값이 없다는 의미이다.</td></tr><tr><td>2</td><td>두번째 파라미터는 기본값으로 <code>Info</code>를 받는다.<br>반환값이 생략되었는데 이는 <code>Unit</code>을 반환한다는 의미이다.</td></tr><tr><td>3</td><td>이 함수는 Int를 반환한다.</td></tr><tr><td>4</td><td>단일 표현식 함수는 타입 추론을 통해 Int를 리턴한다.</td></tr><tr><td>5</td><td></td></tr><tr><td>6</td><td></td></tr><tr><td>7</td><td></td></tr><tr><td>8</td><td></td></tr><tr><td>9</td><td></td></tr><tr><td>10</td><td></td></tr></tbody></table>

