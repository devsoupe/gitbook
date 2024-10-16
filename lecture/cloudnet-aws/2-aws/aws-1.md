---
description: AWS 글로벌 클라우드 인프라를 정리한 내용입니다.
---

# AWS 글로벌 클라우드 인프라

## AWS 글로벌 클라우드 인프라

* AWS는 리전과 가용 영역이라는 형태로 글로벌 클라우드 인프라를 구성한다.
* 리전이라는 지리적인 위치헤는 다수의 가용 영역이 존재 한다.
* 우리나라에도 서울 리전이 있고 그 안에 4개의 가용 용역이 있다.

{% tabs %}
{% tab title="리전 (Region)" %}
* 클라우드 자원이 모여 있는 지리적인 위치이다.
* 현재 기준으로 전 세계 31개의 리전을 보유중이고 지속적으로 증가하고 있다.
* 리전과 리전간은 초고속 통신이 가능한 네트워크 환경을 갖추고 있다.
{% endtab %}

{% tab title="가용 영역 (Availability Zone)" %}
* 리전내에 구성되는 하나 이상의 데이터센터의 집합니다.
* 가용 영역내의 데이터센터들은 서로 연결되어 안정적인 네트워크 환경을 구성하고 있다.
* 현재 기준으로 전 세계에 99개의 가용 용역을 보유하고 있고 이 역시 지속적으로 증가하고 있다.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
AWS의 클라우드 자원을 보유하는 작은 단위 부터 나열하면 다음과 같다.

데이터센터 > 여러 개의 데이터센터가 집합된 가용 영역 > 여러 개의 가용 영역을 가지고 있는 리전
{% endhint %}



