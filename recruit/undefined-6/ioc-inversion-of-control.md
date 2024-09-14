---
description: IoC (Inversion of Control)를 정리한 내용입니다.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# IoC (Inversion of Control)

## 1. 일반적인 의미

* IoC는 제어의 역전으로, 애플리케이션의 제어 흐름을 프레임워크나 컨테이너로 넘기는 디자인 원칙을 의미한다.
* 전통적으로 애플리케이션 코드는 주로 개발자가 제어하고 조작하는데, IoC는 이를 바꾸어 개발자가 아닌 외부 엔티티 (프레임워크 또는 컨테이너)에 의해 제어 흐름이 결정되도록 한다.
* IoC를 통해 애플리케이션의 모듈화와 유연성을 향상시킬 수 있으며, 테스트 용이성과 유지보수성을 높일 수 있다.

## 2. 스프링 프레임워크에서의 의미

* 스프링 프레임워크는 IoC 컨테이너는 DI를 구현하는 형태로 IoC를 제공한다.
* 스프링은 빈(Bean) 객체를 등록하고 관리하며, 필요한 의존성을 자동으로 주입하여 IoC와 DI를 제공한다.

## 3. 스프링부트 예제

{% tabs %}
{% tab title="kotlin" %}
* 스프링 부트 애플리케이션 클래스&#x20;

```kotlin
import org.springframework.boot.autoconfigure.SpringBootApplication
import org.springframework.boot.runApplication

@SpringBootApplication
class MyApplication

fun main(args: Array<String>) {
    runApplication<MyApplication>(*args)
}
```

* 빈 객체를 생성하고 주입하는 클래스

```kotlin
import org.springframework.stereotype.Component

@Component
class MyBean {
    fun sayHello() {
        println("Hello from MyBean!")
    }
}
```

* 빈 객체를 주입받고 사용하는 클래스

```kotlin
import org.springframework.beans.factory.annotation.Autowired
import org.springframework.stereotype.Service

@Service
class MyService @Autowired constructor(private val myBean: MyBean) {

    fun greet() {
        myBean.sayHello()
    }
}
```
{% endtab %}

{% tab title="java" %}
* 스프링 부트 애플리케이션 클래스&#x20;

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

* 빈 객체를 생성하고 주입하는 클래스

```java
import org.springframework.stereotype.Component;

@Component
public class MyBean {
    public void sayHello() {
        System.out.println("Hello from MyBean!");
    }
}
```

* 빈 객체를 주입받고 사용하는 클래스

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class MyService {

    private final MyBean myBean;

    @Autowired
    public MyService(MyBean myBean) {
        this.myBean = myBean;
    }

    public void greet() {
        myBean.sayHello();
    }
}
```
{% endtab %}
{% endtabs %}



