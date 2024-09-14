---
description: 3강 - 코틀린에서 Type을 다루는 방법을 정리한 내용입니다.
---

# 3강 - 코틀린에서 Type을 다루는 방법

자바 코드

{% tabs %}
{% tab title="code1" %}
```java
public class Lec03Main {

    public static void main(String[] args) {

    }

    public static void printAgeIfPerson(Object obj) {
        if (obj instanceof Person) {
            Person person = (Person) obj;
            System.out.println(person.getAge());
        }
    }
}

```
{% endtab %}

{% tab title="code2" %}
```java
public class Person {

    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

}
```
{% endtab %}
{% endtabs %}

## 1. 기본 타입

* 코틀린에는 Byte, Short, Int, Long, Float, Double 부호 없는 정수들 기본 타입이 있다.
* 코틀린은 선언된 기본값을 보고 타입을 추론한다.

{% tabs %}
{% tab title="code1" %}
```kotlin
val number1 = 3 // Int
val number2 = 3L // Long
```
{% endtab %}

{% tab title="code2" %}
```kotlin
val number1 = 3.0f // Float
val number2 = 3.0 // Double
```
{% endtab %}
{% endtabs %}

* 자바는 기본 타입간 암시적 변환이 가능하지만 코틀린은 명시적으로 변환해야 한다.
* 코틀린에는 명시적 변환 메소드인 toXXX()를 제공한다.

{% tabs %}
{% tab title="code1" %}
```java
int number1 = 4;
long number2 = number1; // 암시적 변환

System.out.println(number1 + number2);
```
{% endtab %}

{% tab title="code2" %}
```kotlin
val number1 = 4
val number2: Long = number1 // 컴파일 에러

println(number1 + number2)
```
{% endtab %}

{% tab title="code3" %}
```kotlin
val number1: Int = 4
val number2: Long = number1.toLong() // 명시적 변환

println(number1 + number2)
```
{% endtab %}

{% tab title="code4" %}
```kotlin
val number1 = 3
val number2 = 5
val result = number1 / number2.toDouble() // 명시적 형변환

println(result)
```
{% endtab %}
{% endtabs %}

* 변수가 nullable 타입이면 적절한 처리가 필요하다.

{% tabs %}
{% tab title="code" %}
```kotlin
val number1: Int? = 3
val number2: Long = number1.toLong() // 컴파일 에러
val number2: Long = number1?.toLong ?: 0L
```
{% endtab %}
{% endtabs %}

```
- nullable 변수는 Safe Call (?.)과 Elvis (?:)로 적절한 처리를 해야한다.
```

## 2. 타입 캐스팅

* 자바에서 일반 타입의 형변환은 instanceof 로 확인 후 변수 앞에 (타입)을 붙여 형변환을 한다.

{% tabs %}
{% tab title="code1" %}
```java
public static void printAgeIfPerson(Object obj) {
    if (obj instanceof Person) {
        Person person = (Person) obj;
        System.out.println(person.getAge());
    }
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun printAgeIfPerson(obj: Any) {
    if (obj is Person) {
        val person = obj as Person
        println(person.age)
    }
}
```
{% endtab %}
{% endtabs %}

```
- is는 instanceof와 동일하다.
- as는 (타입)과 동일하다.
- 코틀린에서는 if (obj is Person) 이후 자동 캐스팅 되서 obj as Person이 필요없다. (스마트 캐스트)
- 자바에서는 instanceof로 체크한 후에도 형변환이 필요하다.
- 코틀린은 컴파일러가 상황에 맞는 적절한 컨텍스트를 분석해서 타입을 자동으로 인지한다.
```

* 자바의 !(피연산자 instanceof 피연산자)가 코틀린에서는 자바처럼 처리해도 되나 !is로 간단히 처리도 가능하다.

{% tabs %}
{% tab title="code1" %}
```java
public static void printAgeIfPerson(Object obj) {
    if (!(obj instanceof Person)) {
        Person person = (Person) obj;
        System.out.println(person.getAge());
    }
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun printAgeIfPerson(obj: Any) {
    if (!(obj is Person)) { // 자바처럼 동일하게도 가능
        val person = obj as Person
        println(person.age)
    }
}
```
{% endtab %}

{% tab title="code3" %}
```kotlin
fun printAgeIfPerson(obj: Any) {
    if (obj !is Person) { // !is로 코틀린스럽게
        val person = obj as Person
        println(person.age)
    }
}
```
{% endtab %}
{% endtabs %}

* nullable 변수를 형변환 하기 위해서는 as?를 사용한다.

{% tabs %}
{% tab title="code1" %}
```kotlin
fun main() {
    printAgeIfPerson(null)
}

fun printAgeIfPerson(obj: Any?) {
    val person = obj as Person // NPE 발생
    println(person.age)
}
```
{% endtab %}

{% tab title="code2" %}
```kotlin
fun printAgeIfPerson(obj: Any?) {
    val person = obj as? Person
    println(person?.age) // as? 를 사용하므로 ?. 로 변경 필요
}
```
{% endtab %}
{% endtabs %}

```
- as?의 의미는 obj가 null이 아니면 Person?으로 형변환 하고 null이면 구문 자체가 null이 된다. 
```

{% tabs %}
{% tab title="is" %}
* 앞의 피연산자 값이 뒤의 피연산자 타입이면 true 아니면 false를 반환한다.
{% endtab %}

{% tab title="!is" %}
* 앞의 피연산자 값이 뒤의 피연산자 타입이 아니면 true 맞으면 false를 반환한다.
{% endtab %}

{% tab title="as" %}
* 앞의 피연산자 값이 뒤의 피연산자 타입이면 그 타입으로 캐스팅하고 아니면 예외를 발생시킨다.
* 연산자가 발생시키는 예외는 ClassCastException이다.
{% endtab %}

{% tab title="as?" %}
* 앞의 피연산자 값이 뒤의 피연산자 타입이면 그 타입으로 캐스팅하고 아니면 null을 반환한다.
* 앞의 피연산자가 null이면 그냥 null을 반환한다.
{% endtab %}
{% endtabs %}

## 3. Kotlin의 3가지 특이한 타입

* 코틀린에는 Any, Unit, Nothing이라는 자바에는 없는 타입이 존재한다.

### Any

* 자바의 Object 역할로 모든 객체의 최상위 타입이다.
* 자바의 Primitive Type의 최상위 타입은 Object가 아니나 코틀린에서는 Any가 최상위 타입이다.
* Any 자체는 null을 포함할 수 없고 Any?를 사용해야 한다.
* 자바의 Object와 비슷하게 equals, hashCode, toString이 존재한다.

### Unit

* 자바의 void와 동일하다.
* Unit은 그 자체로 타입 인자로 사용가능하나 자바에서의 void를 타입 인자로 사용시 Void 클래스를 써야 한다.

### Nothing

* 무조건 예외를 반환하는 함수나 무한 루프 함수등에 사용한다.
* 실제적으로는 잘 사용하지는 않는다.

## 4. String interpolation, String indexing

* 자바는 문자열 가공시 String.format을 사용하거나 StringBuilder를 사용한다.

{% tabs %}
{% tab title="code1" %}
```java
Person person = new Person("최태현", 100);
String log = String.format(
    "사람의 이름은 %s이고 나이는 %s세 입니다", person.getName(), person.getAge()
);
```
{% endtab %}

{% tab title="code2" %}
```java
StringBuilder builder = new StringBuilder();
builder.append("사람의 이름은");
builder.append(person.getName());
builder.append("이고 나이는");
builder.append(person.getAge());
builder.append("세 입니다");
```
{% endtab %}
{% endtabs %}

* 코틀린에서는 문자열 가공시 그냥 스트링 구문안에 ${변수}를 작성해서 사용한다.

{% tabs %}
{% tab title="code" %}
```kotlin
val person = Person("코틀린", 100);
val log = "사람의 이름은 ${person.name}이고 나이는 ${person.age}세 입니다"
```
{% endtab %}
{% endtabs %}

* 중괄호 없이 사용가능하나 1) 가독성 2) 일괄 변환 3) 정규식 활용의 이유로 중괄호를 사용하는 편이 좋다.
* 여러줄에 걸친 문자열을 작성할때 """ """(큰 따옴표 3개)를 사용해서 편하게 작성할 수 있다.

{% tabs %}
{% tab title="First Tab" %}
```kotlin
val name = "코틀린"
val str = """
    ABC
    EFG
    ${name}
""".trimIndent() // 중간에 Indent 제거

println(str)
```
{% endtab %}
{% endtabs %}

* 문자열에서 특정 문자를 가져올때 배열요소를 사용하듯이 사용할 수 있다.

{% tabs %}
{% tab title="code1" %}
```java
String str = "ABCDE";
char ch = str.charAt(1);
```
{% endtab %}

{% tab title="code2" %}
```kotlin
val str = "ABCDE"
val ch = str[1]
```
{% endtab %}
{% endtabs %}

## 정리

> 변수는 초기값으로 타입추론이 가능하고 타입간 명시적 형변환을 사용해야 한다.
>
> is, !is, as, as?를 이용해 타입을 확인하고 캐스팅한다.
>
> Any는 자바의 Object와 같은 최상위 타입이다.
>
> Unit은 자바의 void와 거의 동일하다.
>
> Nothing은 정상적으로 끝나지 않는 함수의 반환을 의미한다.
>
> 문자열 가공시 ${변수}와 """ """를 사용하면 깔끔한 코딩이 가능하다.
>
> 문자열에서 문자를 가져올때 배열 연산자 \[]를 사용해서 가져올 수 있다.
