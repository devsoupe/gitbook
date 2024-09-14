---
description: AWS 네트워킹 서비스를 정리한 내용입니다.
---

# AWS 네트워킹 서비스

## AWS 네트워킹 서비스

* 클라우드 자원들의 통신을 위한 서비스로 클라우드 서비스의 기반이 되는 중요한 서비스이다.

### 중요한 네트워킹 서비스

{% tabs %}
{% tab title="VPC (Virtual Private Cloud)" %}
* 사용자 전용의 가상 프라이빗 클라우드 네트워크를 구성하는 서비스이다.
* 자신만의 VPC를 생성하여 네트워크를 구성하고, 내부에 클라우드 자원을 배치 통신한다.
{% endtab %}

{% tab title="ELB (Elastic Load Balancing)" %}
* 트래픽을 부하 분산하여 전달하는 기능의 서비스이다.
* IT 자원 구성시 단일 자원으로 구성하는 것은 장애시 서비스 불가 상태가 되므로 지양한다.
* 다수의 자원을 구성 고가용성을 확보하고 ELB로 트랙픽을 분산처리하여 효율적인 통신환경을 구축한다.
{% endtab %}

{% tab title="Route 53" %}
* AWS 에서 제공하는 관리형 DNS 서비스이다.
* 도메인을 등록하고 관리할 수 있다.
{% endtab %}
{% endtabs %}

```
그 외 Transit Gateway, Global Accelerator, Direct Connect, VPC Peering, 
CloudFront, Site-toSite VPN 등의 다양한 서비스가 있다.
```

