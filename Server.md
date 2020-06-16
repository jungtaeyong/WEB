# Server

서버에 대한 기초 개념을 정리한다. 



## Index

- [Router](#Router)
- [Network Address Translation](#Network-Address-Translation)
- [Port Forwarding](#Port-Forwarding)
- [Dynamic IP Address VS Static IP Address](#Dynamic-IP-Address-VS-Static-IP-Address)
- [DHCP (Dynamic Host Configuration Protocol)](#DHCP-(Dynamic-Host-Configuration-Protocol))
- [HTTP/응답코드](#HTTP/응답코드)
- [ETC](#ETC)



## Router

![router](https://user-images.githubusercontent.com/52786355/84009371-1f22cf00-a9ae-11ea-9f04-cf1ec01a368d.PNG)

우리가 흔히 사용하는 공유기를 **라우터**라고 한다. 이 라우터는 통신사의 케이블을 WAN(Wide Area Network)에 연결하고 주변의 인터넷이 필요한 기기들은 케이블을 LAN(Local Area Network) 연결해서 인터넷을 가능하게 한다. 이 때, WAN은 Public IP Address(공개망)라고 하고, 공유받는 기기들의 주소는 Gateway Address 또는 Router address라고 부른다. 이 Gateway Address는 Private IP Address(사설망)라고 한다. 사설망의 범위는 192.168.0.0 ~ 192.168.255.255로 총 65536개의 범위를 갖고 있다. 라우터도 라우터의 IP(내부 IP Address)를 갖고 있다. 보통 192.168.xxx.1이 기본 게이트웨이 IP이고, 사설망은 192.168.xxx.2부터 시작하는 식이다. Public IP Address를 알고 싶다면 라우터 정보에서 찾을 수 있기도하고, [웹 사이트](https://whatismyipaddress.com/)에서 알려주기도 한다.



## Network Address Translation

그렇다면 우리가(클라이언트) 정보를 인터넷에 보낼 때 어떤 변화가 일어날까? NAT(Network Address Translation)는 이와 관련된 개념이고 일종의 기술이다. 다음과 같은 과정을 거친다.

![NAT](https://user-images.githubusercontent.com/52786355/84010487-ade41b80-a9af-11ea-885b-9a922d02405e.PNG)

1. 192.168.0.1의 사설망을 사용하고 있는 클라이언트가 PC를 통해 인터넷에 정보를 올린다는 요청을 하면 그 정보가 케이블을 타고 라우터에 닿는다.
2. 라우터는 192.168.0.1의 사설망에서 보냈다는 것을 기록하고, NAT기술을 이용해 어디서든 접근가능한 Public IP Address인 59.6.66.238로 변환하여 보낸다.
3. 인터넷은 다시 정보를 접근할 수 있는 공개망(Public IP Address)으로 데이터를 보내면 라우터에서 어떤 사설망에서 정보를 보낸 것인지 기록했기 때문에 해당 사설망으로 데이터를 전달해준다.



## Port Forwarding

 공유기(라우터)를 사용하지 않고 바로 컴퓨터에 연결하는 경우는 공인IP(Public IP Address)를 사용하기 때문에 다른 사용자가 직접 컴퓨터에 접속할 수 있다.(원격접속, 띄운 서버에 접속 등) 그러나 라우터를 거치고 사설망으로 인터넷을 사용하는 경우가 대부분이고, 이 경우엔 라우터를 통해 어떤 사설망에 접속할 것인지 라우터가 모르기 때문에 접속할 수 없다. 이럴때 사용하는 기술이 포트 포워딩이다. 포트 포워딩은 **해당 라우터의 공인IP의 N번 포트로 접속했을 경우, 지정한 사설망의 M번 포트로 연결시켜주는 기술**이다.  



## Dynamic IP Address VS Static IP Address

직역하면 동적 아이피, 정적 아이피라고 할 수 있다. 유동 IP라고도 부르고, AWS에서는 정적 IP를 탄력적 IP라고 부른다. 우리는 통신사에게 인터넷을 제공받는다. 보통 통신사라고도 하지만, `ISP(Internet Service Provider)`라고 한다. ISP는 기본적으로 유동 IP를 우리에게 제공한다. 이유는 쓰지않는 IP를 재활용하기 위함이다. 그렇기 때문에 우리가 인터넷을 사용하지 않을 때, ISP는 우리 IP를 회수해 인터넷을 필요로 하는 다른 사용자에게 IP를 할당해 준다. 우리가 서버를 운용한다고 생각해보자. 서버를 운용하려면 고정적인 주소가 필요한데 지속적으로 IP가 바뀐다면 운용할 수 없을 것이다. 따라서 다른 처리를 해주거나, 정적IP가 필요하다. 통신사는 돈을 더 받고 Static IP Address를 할당해주기도 하고, AWS에서 탄력적 IP를 할당 받을 수 있다.



## DHCP (Dynamic Host Configuration Protocol)

우리가 라우터에 WAN에 통신사 케이블을 연결하고, 사설망 포트에 케이블을 연결했을 때, 어떻게 사설망 IP를 할당받을 수 있을까? 바로 DHCP가 이러한 로직을 처리한다. 라우터에는 DHCP Server가 깔려있고, 클라이언트 장비(PC)에는 DHCP Client가 깔려있다. 또, MAC Address(물리적 주소라고도 부른다.)라는 게 있는데, Media Access Control의 약자로 각 장비에 있는 고유한 시리얼 번호이다. 앞 6자리는 제조사의 번호, 뒤는 고유 시리얼 번호를 의미한다. PC에 깔린 MAC Address를 식별자로 이용해 DHCP Clinet가 라우터에게 사설망 IP 할당을 요청하면 라우터의 DHCP Server가 MAC Address로 식별하고 해당 PC에게 사설IP를 할당한다. IP 대여시간도 설정할 수 있다.



## HTTP/응답코드

- 1XX : 정보전달. 요청을 받았고, 작업을 진행 중이라는 의미이다. HTTP/1.0 이후 정의되지 않았다. 서버도 클라이언트에 이 코드를 보내지 않는다. 

- 2XX : 성공. 이 작업을 성공적으로 받았고, 이해했으며, 받아들여졌다는 의미이다.

  - 200 OK
  - 201 Created : 요청이 성공적으로 처리되어서 리소스가 만들어졌음을 의미한다. 
  - 204 No Content : 성공적으로 처리했지만 컨텐츠를 제공하지 않는다.

  - 206 Partial-Content : 컨텐츠의 일부 부분만 제공한다.

- 3XX : 리다이렉션. 이 요청을 완료하기 위해서는 리다이렉션이 이루어져야 한다는 의미이다. 

- 4XX : 클라이언트 오류. 이 요청은 올바르지 않다는 의미이다. 여기서부터 브라우저에 직접 표출된다. 굵게 강조된 것은 자주 보이는 오류들이다. 

  - **400 Bad Request** (잘못된 요청) : 요청 자체가 잘못됨
  - **401 Unauthorized** (권한 없음) : 인증이 필요한 리소스에 인증 없이 접근할 경우 발생. 이 응답 코드를 사용할 때에는 반드시 브라우저에 어느 인증 방식을 사용할 것인지 보내야 한다.
  - **403 Forbidden** (거부됨) : 서버가 요청을 거부함. 관리자가 해당 사용자를 차단했거나 서버에 index.html이 없는 경우에도 발생할 수 있다. (클라이언트가 파일 리스트를 보는 권한을 요청할 경우. 단일 파일을 요청할 경우의 에러는 404)

  - **404 Not Found** (찾을 수 없음) : 찾는 리소스가 없다는 뜻이다. (url 자체가 없음, 리소스가 없음, jsp가 없음 등...)
  - **410 Gone** (사라짐) : 404와는 달리 찾는 리소스가 영원히 사라진 경우. 

- 5XX : 서버 오류. 올바른 요청에 대해 서버가 응당할 수 없다는 의미.

  - **500 Internal Server Error** (내부 서버 에러) : 서버에 오류가 발생해 작업을 수행할 수 없음. 보통 설정이나 퍼미션 문제. (문법 오류, 배열 사이즈 초과, jstl 문법 오류 등..)

  - **502 Bad Gateway** : 게이트웨이가 연결된 서버로부터 잘못된 응답을 받았을 경우.
  - **503 Service Temporarily Unavailable** (일시적으로 서비스를 이용할 수 없음) : 웹 서버 과부하로 다운되었을 경우.



## ETC

포트번호는 65536개가 있는데, `0 ~ 1023`은 **Well-Known Port**라고 부른다. 이 포트는 약속된 포트로, 예를들면 22는 ssh, 80은 http, 443은 https이다. 따라서 개인서버의 포트를 정할 때는 `0 ~ 1023`을 피해 다른 포트번호로 설정해야한다. 관습적으로 8080포트를 쓰는데 이것은 관습적인 포트번호일뿐, `0 ~ 1023`만 피한다면 어디든 상관없다. 





#### 참고자료 : 인프런 - 생활코딩 강의(Server), [나무위키 : HTTP/응답코드](https://namu.wiki/w/HTTP/응답 코드)

