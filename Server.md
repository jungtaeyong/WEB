# Server

서버에 대한 기초 개념을 정리한다.



## 라우터

![router](https://user-images.githubusercontent.com/52786355/84009371-1f22cf00-a9ae-11ea-9f04-cf1ec01a368d.PNG)

우리가 흔히 사용하는 공유기를 **라우터**라고 한다. 이 라우터는 통신사의 케이블을 WAN에 연결하고 주변의 인터넷이 필요한 기기들은 케이블로 연결해서 인터넷을 가능하게 한다. 이 때, WAN은 Public IP Address(공개망)라고 하고, 공유받는 기기들의 주소는 Gateway Address 또는 Router address라고 부른다. 이 Gateway Address는 Private IP Address(사설망)라고 한다. 사설망의 범위는 192.168.0.0 ~ 192.168.255.255로 총 65536개의 범위를 갖고 있다. 라우터도 라우터의 IP(내부 IP Address)를 갖고 있다. 보통 192.168.xxx.1이 기본 게이트웨이 IP이고, 사설망은 192.168.xxx.2부터 시작하는 식이다. Public IP Address를 알고 싶다면 라우터 정보에서 찾을 수 있기도하고, [웹 사이트](https://whatismyipaddress.com/)에서 알려주기도 한다.



## Network Address Translation

그렇다면 우리가(클라이언트) 정보를 인터넷에 보낼 때 어떤 변화가 일어날까? NAT(Network Address Translation)는 이와 관련된 개념이고 일종의 기술이다. 다음과 같은 과정을 거친다.

![NAT](https://user-images.githubusercontent.com/52786355/84010487-ade41b80-a9af-11ea-885b-9a922d02405e.PNG)

1. 192.168.0.1의 사설망을 사용하고 있는 클라이언트가 PC를 통해 인터넷에 정보를 올린다는 요청을 하면 그 정보가 케이블을 타고 라우터에 닿는다.
2. 라우터는 192.168.0.1의 사설망에서 보냈다는 것을 기록하고, NAT기술을 이용해 어디서든 접근가능한 Public IP Address인 59.6.66.238로 변환하여 보낸다.
3. 인터넷은 다시 정보를 접근할 수 있는 공개망(Public IP Address)으로 데이터를 보내면 라우터에서 어떤 사설망에서 정보를 보낸 것인지 기록했기 때문에 해당 사설망으로 데이터를 전달해준다.





