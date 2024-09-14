---
description: Hello World를 정리한 내용입니다.
---

# Hello World

{% tabs %}
{% tab title="code" %}
```kotlin
package org.kotlinlan.play // 1

fun main() { // 2
    println("Hello, World") // 3
}
```
{% endtab %}
{% endtabs %}

<table><thead><tr><th width="75.5">번호</th><th>내용</th></tr></thead><tbody><tr><td>1</td><td><p>코틀린 코드는 패키지 안에 정의한다.</p><p>패키지 선언을 하지 않으면 디폴트 패키지에 속하게 된다.</p></td></tr><tr><td>2</td><td><p>코틀린 애플리케이션의 시작점은 <code>main</code> 함수이다.</p><p>코틀린 1.3부터 파라미터 없이 <code>main</code> 함수를 정의할 수 있다.</p><p>반환타입을 정의하지 않으면 아무것도 반환하지 않는다.</p></td></tr><tr><td>3</td><td><p><code>println</code>은 표준 출력에 한 줄 출력한다.</p><p>코틀린에서 세미콜론을 넣는 것은 선택사항이다.</p></td></tr></tbody></table>

* 코틀린 1.3 이전이라면 `main` 함수의 `Array<String>` 파라미터가 필수이다.

{% tabs %}
{% tab title="code" %}
```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```
{% endtab %}
{% endtabs %}
