# DNS (Domain Name System)

DNS 이전의 Domain은 Stanford Research Institute라는 신뢰할 만한 기관에서 처리했다. 서버관리자가 기관에 전화를 걸어 해당 도메인과 IP주소를 등록해달라고 요청하면, 기관은 그 정보를 등록하고 클라이언트는 기관에서 host파일을 다운로드 받아 들어가는 방식이었다. 매우 복잡하고 비효율적인 방법이었다. 이러한 방법을 DNS를 통해 해결하게 된다. Domain Name System Server를 두어 기관이 아닌 시스템이 처리하도록 하는 방법이다. 서버관리자는 DNS Server에 해당 IP와 Domain을 등록하면, 클라이언트가 브라우저에서 도메인을 입력했을 때, DNS Server에 접속해(기본적으로 ISP가 제공하지만 구글같은 다른 Public DNS도 사용가능) 등록된 도메인의 IP주소를 받아와 접속하는 방식이다. Host파일도 필요없고, 사람이 처리하던 것을 서버 시스템이 처리하기 때문에 매우 효율적인 방법이라 할 수 있다.

![DNS](https://user-images.githubusercontent.com/52786355/84107041-b3953c00-aa57-11ea-9580-28ef4cf4f33e.PNG)

예를들어, blog.example.com.에서 (생략되었을 뿐, 모든 도메인의 끝은 `.`을 포함하고 있다.) 클라이언트가 해당 도메인의 IP주소를 요청할 때, 여러 개의 DNS서버를 조회하게 된다. 결론적으로 클라이언트가 원하는 정보는 sub DNS Server에 저장되어 있다. Root부터 시작해서 Top-level -> Second-level -> sub 순이다. sub에서 최종적으로 IP주소를 얻게 된다. 왜 바로 sub로 가지 않고 Root부터 시작할까? 클라이언트는 Root DNS Server 주소는 알고 있지만, 해당 도메인의 주소를 가지고 있는 sub가 어디에 존재하는지는 모른다. 그렇기 때문에 Root부터 시작해서 어떤 sub인지 알아가는 과정이 필요한 것이다. 다음과 같은 과정을 거친다.

1. 클라이언트가 해당 도메인을 Root DNS Server에 요청하면, `.`밑의 com을 담당하는 Top-level DNS Server를 알려준다.
3. 클라이언트가 Root에게 응답받은 정보를 근거로 해당 Top-level DNS Server에 요청하면, `.`밑의 example을 담당하는 Second-level DNS Server를 알려준다.
4. 클라이언트가 Top-level에게 응답받은 정보를 근거로 해당 Second-level에 요청하면, `.`밑의 blog를 담당하는 Sub DNS Server를 알려준다.
4. 클라이언트가 Second-level에게 응답받은 정보를 근거로 해당 Sub에 요청하면, sub는 해당 도메인의 IP주소를 알려준다.

결과적으로 클라이언트가 Root부터 시작해서 Top-level -> Second-level -> sub 순으로 요청을 주고 받으며 도메인의 실제 IP정보를 얻게 된다.

![DNS2](https://user-images.githubusercontent.com/52786355/84106894-471a3d00-aa57-11ea-929c-8bca93a8fade.PNG)

클라이언트는 PC등 우리가 사용하는 통신 장비이다. Root, Top-level, Second-level도 대응되는 실체가 있다. 

- Root : ICANN이라는 비영리 단체이다. 이 단체가 모든 DNS의 뿌리(Root)를 다루는 것이다. 위 그림에는 a.root-servers.net이라고 되어있는데, 서버는 하나만 존재하는 것이 아니다. 실제로는 `a ~ m`까지 13개의 Root서버가 있고, 다시 이 13개의 Root서버는 수백 개의 성능 좋은 서버로 나누어져 있다. Root뿐만 아니라 나머지 서버도 같은 개념이다. 
- Top-level : Registry 등록소이다. `.com`, `co.kr` 등과 같은 Top-level 도메인을 다룬다.
- Second-level : Registrar 등록대행자이다. 우리가 아는 도메인을 판매하는 기업들을 예로들 수 있다. (cafe24, 가비아 등) 



## DNS record & CNAME

![DNS3](https://user-images.githubusercontent.com/52786355/84110036-045c6300-aa5f-11ea-9cda-131ab3a26abe.PNG)

`Type = A` : 해당 도메인을 원하는 IP로 매핑시킨다.

`Type = CNAME` : 해당 도메인을 다른 도메인으로 매핑시킨다. 



참고자료 : 인프런 - 생활코딩 강의