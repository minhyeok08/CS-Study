## IPv4 & IPv6

### IPv4
- 32비트를 주소로 사용

- .으로 구분 된 4개의 10진수로 표현

    ex) 192.68.32.5

- 2^32개 약 43억개를 ip주소로 사용가능

- 헤더는 20바이트로, 옵션 필드가 있어서 복잡하고 처리가 느릴 수 있다

- IPsec라는 보안 프로토콜이 선택사항

### IPv6 도입 이유

- IPv4만으로는 부족하다고 생각되어 2^128 (=거의 무한대) 에 가까운 IPv6가 도입됨

### IPv6

128비트를 주소로 사용

- : 으로 구분 된 8개의 16진수

    ex) 2001:230:abcd:ffff:0000:0000:ffff:1111

- 2^128개를 주소로 사용 가능

- 주소를 16진수로 표현

- 헤더는 40바이트로, 옵션 필드가 없어서 처리가 빠르며, 라우팅 효율성과 성능이 향상

- IPsec가 표준으로 포함되어 있어서, 데이터의 무결성, 기밀성, 인증 기능을 제공

### IPv6 도입 지연 원인

- 업그레이드 비용

    - 하드웨어 장비 교체, 소프트웨어 업데이트, 테스트, 교육 등에 많은 비용이 든다.

- 호환성 문제

    - IPv4와 IPv6는 직접적으로 호환되지 않기 때문에 IPv6를 완전히 도입하려면 네트워크의 모든 컴포넌트를 업그레이드하거나 적절하게 구성해야 한다.

- 필요성 부족

    - IPv4 주소 공간이 부족한 문제는 NAT(Network Address Translation)와 같은 기술로 어느 정도 해결할 수 있다.

- 기술적 복잡성

    - IPv6 주소는 IPv4 주소보다 길고 복잡하여 사람이 이해하거나 기억하기 어렵다.

- 보안 문제

    - 새로운 프로토콜은 항상 새로운 보안 위협을 가져올 수 있습니다. IPv6에 대한 완전한 이해 없이 네트워크를 IPv6로 전환하면, 예상치 못한 보안 문제가 발생할 수 있다.

## 고정 IP & 유동 IP

### 고정 IP
 - 특징

    - 고정 IP는 네트워크 장치에 한 번 할당되면 변경되지 않는 IP 주소이다.
    
    - 서버와 같이 항상 동일한 IP 주소를 유지해야 하는 장치에 주로 사용된다. 

    - 고정 IP를 사용하면 원격에서 장치에 접근하기 쉽고, 일관된 네트워크 연결을 유지할 수 있다. 

    - 그러나 고정 IP는 추가 비용이 발생할 수 있고, 보안 위협에 노출될 수 있다.

### 유동 IP
 - 등장 배경

    - 인터넷 사용자가 증가하고 주소 공간이 부족해졌다.

    - 이를 해결하기 위해 ip주소를 동적으로 할당해주는 DHCP가 등장하였고, 유동 ip 개념이 나오게 되었다.

 - 특징

    - 장치가 네트워크에 연결될 때마다 DHCP (Dynamic Host Configuration Protocol) 등의 프로토콜을 통해 새로운 IP 주소를 할당받는 방식.

    - 사용하지 않는 IP 주소가 다른 장치에 재할당될 수 있기 때문에 효율적.

    - 왜냐하면 IP 주소가 자주 변경되기 때문에 외부 공격자가 특정 IP 주소를 타겟으로 설정하기 어렵기 때문에 보안성이 높다.


## 공인 IP & 사설 IP

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbdNkvK%2FbtrdmBT3Ad4%2FcsmuwzYknhih4FR6BGFqKK%2Fimg.png" width="800" height="400">

### 공인 IP
- 인터넷상에서 유일한게 식별되는 IP 주소

- ISP로 부터 주소를 할당 받음

- 인터넷상의 다른 장치와 통신할 때 공인 IP를 사용 
    
    ex) 웹 서버나, 이메일과 같이 외부에서 접근이 필요한 서버

### 사설 IP
- 로컬상에서 유일하게 식별되는 IP 주소

- DHCP로 부터 자동으로 할당 받음

- 일반적으로 가정이나 사무실등 작은 네트워크에서 사용

### 공인/사설 IP 사용의 장점

- 사설 ip를 사용하면 같은 주소를 여러 네트워크에서 사용가능하므로 주소 공간을 효율적으로 사용할 수 있다.

- 사설 ip주소는 외부에서 접근할 수 없기 때문에 네트워크 보안이 강화된다.

### NAT
- 통신을 하기 위해 사설 ip를 공인 ip로 변환해주거나 반대의 경우로 변환해주는 것.

## 서브넷

<img src="https://user-images.githubusercontent.com/24274424/83946405-93912d00-a84b-11ea-89c3-584763a6ff7a.png" width="700" height="500">


### A 클래스

네트워크 앞자리 0 시작

0xxx xxxx. hhhh hhhh. hhhh hhhh. hhhh hhhh

네트워크 주소 범위 : 0 ~ 127

호스트 주소 범위 : 0.0.0 ~ 255.255.255
 
네트워크 할당 개수 : (2^7)-1 개 (127은 제외)

호스트 할당 개수 : (2^24)-2 개 


### B 클래스

네트워크 앞자리 10 시작

10xx xxxx. xxxx xxxx. hhhh hhhh. hhhh hhhh

네트워크 주소 범위 : 128.0 ~ 191.255

호스트 주소 범위 : 0.0 ~ 255.255

네트워크 할당 개수 : 2^14 개

가능한 호스트 주소 수 : (2^16) - 2개



### C 클래스

네트워크 앞자리 110 시작

110x xxxx. xxxx xxxx. xxxx xxxx. hhhh hhhh

네트워크 주소 범위 : 192.0.0 ~ 223.255.255

호스트 주소 범위 : 0 ~ 255

네트워크 할당 개수 : 2^21 개

가능한 호스트 주소 수 : (2^8) - 2개

- D는 멀티캐스트 주소, E는 연구용 주소(미래계획)



## 질문
Q. 예를들어 A Class의 네트워크 주소에서 호스트가 사용할 수 있는 주소는 2^24-2이다.
-2를 하는 이유는?

A. 14이라는 네트워크 주소를 받았다면 첫번째, 14.000.000.000은 네트워크 자체를 식별할 수 있는 주소로 사용되어야 하기 때문에 호스트 주소로 쓰지못한다. 두번째, 14.255.255.255는 브로드캐스트 주소로 해당 네트워크의 모든 호스트들에게 데이터를 보낼 때 사용하므로 호스트 주소로 사용하지 못한다. 때문에 호스트가 사용할 수 있는 주소는 2^24 - 2개이다.


## 참조

https://github.com/im-d-team/Dev-Docs/blob/master/Network/IP.md

https://nordvpn.com/ko/blog/public-ip-and-private-ip/