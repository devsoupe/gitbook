---
description: 2강 - 코틀린에서 null을 다루는 방법을 정리한 내용입니다.
---

# 2강 - 코틀린에서 null을 다루는 방법

## 자바 코드

{% tabs %}
{% tab title="code" %}
<pre class="language-java"><code class="lang-java">public class Lec02Main {

    public static void main(String[] args) {

    }

<strong>    public boolean startsWithA1(String str) {
</strong>        if (str == null) {
            throw new IllegalArgumentException("null이 들어왔습니다.");
        }
        return str.startsWith("A");
    }

    public Boolean startsWithA2(String str) {
        if (str == null) {
            return null;
        }
        return str.startsWith("A");
    }

    public boolean startsWithA3(String str) {
        if (str == null) {
            return false;
        }
        return str.startsWith("A");
    }

}

</code></pre>
{% endtab %}
{% endtabs %}

* 코틀린에서는 null이 들어가는 변수를 완전히 다르게 취급한다.
* 코틀린은 null이 들어가는 변수를 타입? 형태로 사용한다.

## 1. 코틀린에서의 null 체크

{% tabs %}
{% tab title="code" %}
```java
public boolean startsWithA(String str) {
    return str.startsWith("A");
}
```
{% endtab %}
{% endtabs %}

```
- Java에서는 str에 null이 들어올 수 있으므로 안전하지 않은 코드이다.
```

### 안전한 코드로 바꾸기

1. str이 null일 경우 Exception을 낸다.
2. str이 null일 경우 null을 반환한다.
3. str이 null일 경우 false를 반환한다.

{% tabs %}
{% tab title="code1" %}
```java
public boolean startsWithA1(String str) {
    if (str == null) {
        throw new IllegalArgumentException("null이 들어왔습니다.");
    }
    return str.startsWith("A");
}
```
{% endtab %}

{% tab title="code2" %}
```java
public Boolean startsWithA2(String str) {
    if (str == null) {
        return null;
    }
    return str.startsWith("A");
}
```
{% endtab %}

{% tab title="code3" %}
```java
public boolean startsWithA3(String str) {
    if (str == null) {
        return false;
    }
    return str.startsWith("A");
}
```
{% endtab %}
{% endtabs %}

### 코틀린 코드로 작성하기

{% tabs %}
{% tab title="code1" %}
```kotlin
fun startWithA1(str: String?): Boolean {
    if (str == null) {
        throw IllegalArgumentException("null이 들어왔습니다.")
    }
    return str.startsWith("A")
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun startWithA2(str: String?): Boolean? {
    if (str == null) {
        return null
    }
    return str.startsWith("A")
}
```
{% endtab %}

{% tab title="code3" %}
```kotlin
fun startWithA3(str: String?): Boolean {
    if (str == null) {
        return false
    }
    return str.startsWith("A")
}
```
{% endtab %}
{% endtabs %}

| Java    | Kotlin   |
| ------- | -------- |
| String  | String?  |
| Boolean | Boolean? |
| boolean | Boolean  |

## 2. Safe Call과 Elvis 연산자

* 코틀린에서는 null이 가능한 타입을 완전히 다르게 취급한다.
* null이 들어갈 수 있는 타입은 . 연산자로 바로 호출이 불가능하다.
* null이 들어갈 수 있는 타입은 Safe Call (?.)으로 호출한다.
* Safe Call (?.)은 null이 아니면 실행하고, null이면 실행하지 않는다. (그대로 null)

{% tabs %}
{% tab title="code" %}
```kotlin
val str: String? = "ABC"
println(str.length) // 컴파일 에러
println(str?.length)
```
{% endtab %}
{% endtabs %}

```
- str이 널이면 그대로 null이 출력된다.
```

* Elvis 연산자는 앞의 연산 결과가 null이면 연산자의 뒤의 값을 사용한다.

{% tabs %}
{% tab title="code" %}
```kotlin
val str: String? = "ABC"
println(str?.length ?: 0) // str?.length가 null이면 0을 사용
```
{% endtab %}
{% endtabs %}

### 엘비스 연산자를 활용해 좀 더 코틀린스럽게

{% tabs %}
{% tab title="code1" %}
```kotlin
fun startWithA1(str: String?): Boolean {
    return str?.startsWith("A") ?: 
        throw IllegalArgumentException("null이 들어왔습니다.")
}
```
{% endtab %}

{% tab title=" code2" %}
```kotlin
fun startWithA2(str: String?): Boolean? {
    return str?.startsWith("A")
}
```
{% endtab %}

{% tab title="code3" %}
```kotlin
fun startWithA3(str: String?): Boolean {
    return str?.startsWith("A") ?: false
}
```
{% endtab %}
{% endtabs %}

* Elvis 연산은 early return에도 사용할 수 있다.

{% tabs %}
{% tab title="code1" %}
```java
public long calculate(Long number) {
    if (number == null) {
        return 0;
    }
    
    // 다음 로직
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun calculate(number: Long?): Long {
    number ?: return 0
    
    // 다음 로직
}
```
{% endtab %}
{% endtabs %}

## 3. 널 아님 단언!!

* 타입 자체는 nullable 이지만, 로직상 특정 상황 이후에 null이 될 수 없는 경우가 있다.

{% tabs %}
{% tab title="code" %}
```kotlin
fun startsWith(str: String): Boolean {
    return str.startsWith("A") // 컴파일 에러
    return str!!.startWith("A")
}
```
{% endtab %}
{% endtabs %}

```
- str이 상황상 무조건 null이 아니어도 . 연산자는 컴파일 에러가 발생한다.
- !!는 컴파일러에게 절대 null이 아님을 단언하는 문법이다.
- 혹시 null이 들어오면 런타임에 NPE에러가 발생한다.
```

## 4. 플랫폼 타입

* 코틀린에서 Java 코드를 가져다 사용할때 null 여부에 대한 처리 기준이 있다.

{% tabs %}
{% tab title="code1" %}
```java
public class Person {

    private final String name;

    public Person(String name) {
        this.name = name;
    }

    @Nullable
    public String getName() {
        return name;
    }
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun main() {
    val person = Person("공부하는 개발자")
    startWithA(person.name) // 컴파일 에러
}

fun startWithA(str: String): Boolean {
    return str.startsWith("A")
}
```
{% endtab %}
{% endtabs %}

```
- 자바에서의 @Nullable, @NotNull 어노테이션 기준으로 코틀린 컴파일러가 인식하고 이해해서 활용한다.
```

* 자바에서 어노테이션을 붙이지 않으면 코틀린에서 null 여부를 알 수 없는데 이를 플랫폼 타입이라고 한다.
* 플랫폼 타입은 컴파일 타임에 에러가 발생하지 않고 런타임에 Exception이 날 수 있다.

{% tabs %}
{% tab title="code1" %}
```java
public class Person {

    private final String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun main() {
    val person = Person("공부하는 개발자")
    startWithA(person.name) // 컴파일 에러가 나지 않지만 런타임에 에러가 날 수 있음
}

fun startWithA(str: String): Boolean {
    return str.startsWith("A")
}
```
{% endtab %}
{% endtabs %}

```
- 코틀린 입장에서 정보가 없으면 '일단 되게 해줄게' 하는 느낌으로 받아 들이면 된다.
```

## 정리

> 코틀린에서 null이 들어가는 타입은 완전히 다르게 간주된다.
>
> 한번 null을 검사하면 그 이후에는 non-null임을 컴파일러가 알 수 있다. (스마트 캐스트)
>
> null이 아닌 경우만 호출되는 Safe Call (?.)이 있다.
>
> null인 경우에만 호출되는 Elvis (?:)가 있다.
>
> null이 절대 아니라고 생각될때 사용하는 단어 (!!)이 있다.
>
> 코틀린에서 자바코드를 사용할때 null 유무를 지정하지 않았을때의 플랫폼 타입 사용에 유의 해야 한다.
