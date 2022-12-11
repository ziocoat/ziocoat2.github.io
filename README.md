### Stateless
  1. http 통신이 끝나면 상태를 유지하지 않는 특성
  2. 부하를 현저하게 줄일 수 있지만 매번 request를 보내야하는 상황 발생
 
 
 
### Cookie, Session
 - 위와 같은 http 프로토콜의 단점을 보완하고자 등장
 - 클라이언트와 서버의 통신 정보 및 상태를 기록하여 다시 접속 시 그대로 정보를 유지하기 위한 것
  
  
  
|구분|차이점|단점|
|-|-|-|
|Cookie | 해당 접속 정보를 클라이언특측에 저장 | 사용자가 임의로 변조하여 악용 가능|
|Session | 해당 접속 정보를 웹서버에 저장 | 쿠키에 비해 안전하지만 서버의 자원을 소모|



### Persistent Cookie, Session Cookie
 1. Persistent Cookie
  - 접속 정보를 유저의 디스크에 저장되며 브라우저를 닫거나 PC를 재시작해도 존재
  - 웹서버로부터 쿠키를 받을 때 유효기간이 세팅되어 만료시 파기
  ![image](https://user-images.githubusercontent.com/64004292/206189695-92c16d42-4386-4743-9e37-10d740252ed2.png)
 
 2. Session Cookie
   - 사용자가 사이트 탐색시 관련한 설정등 저장하는 임시 쿠키로 브라우저를 닫는 순간 삭제
   - non-persistent cookies 또는 temporary cookies라고 부르기도하며 메모리에 저장
   - 브라우저가 active 상태일때 까지만 유효하게 설정하려면 유효 시간 세팅을 하지 않음(ex. 온라인 뱅킹)

### Set-Cookie
   - 클라이언트 서버 모델에서는 서버가 클라이언트의 요청없이 데이터를 보낼 수 없기 때문에 쿠키 설정도 마찬가지로 클라이언트 요청에 응답할때 발생
   - 기본적으로 쿠키는 <이름>=<값>의 형태
   - 유효기간이 명시 되어 있는 쿠키인 Permanet cookie 같은 경우 Set-Cookie 헤더에 Expires나 Max-Age 속성을 사용<br />
   > Expires: 쿠키가 사라지는 시점
   > Max-Age: 쿠키 유효 기간, 초 단위로 설정 
   > Expires, Max-Age 속성 둘 다 존재 시 Max-Age 우선, 둘 다 없을 시 세션이 종료될때 만료 <br />
   ![image](https://user-images.githubusercontent.com/64004292/206891928-656a13f0-cc71-4137-b028-766bffa6b398.png)
   - Set-Cookie 같은 경우 쿠키 적용 범위를 적용하기 위해 Domain 속성 사용, Path를 사용해 도메인의 특정 경로로 쿠키 범위 축소
   > ![image](https://user-images.githubusercontent.com/64004292/206892412-a24fe643-e5cf-438d-834e-1f077cee777e.png)
   
   


### Cookie/Session Vulnerability
 1. XSS(Cross Site Script)
   - XSS 공격은 자바스크립트가 사용자의 컴퓨터에서 실행된다는 점을 이용한 공격으로 쿠키 값을 확인할 수 있는 document.cookie를 이용하여 쿠키 값 탈취 <br />
     - 대응 방법
    > javascript의 태그 문자인 <,> 등을 HTML entity (&lt;, &gt; 등)으로 필터링
    > http only 옵션을 설정하여 javascript로 쿠키를 조회하는 것을 차단
     <br/>
 2. Sniffing을 이용한 Session Hijacking
 ![image](https://user-images.githubusercontent.com/64004292/206892122-7f52310d-b692-426e-9205-567f5b30bdce.png)

  - 공격 순서
   1. 스니핑을 통해 세션을 확인하고 시퀀스 번호 획득
   2. 공격자는 알아낸 시퀀스 번호를 이용하여 사용자와 서버간의 TCP 연결을 RST 패킷을 보내 서버 쪽 연결만 종료 (Server-Closed, Client Established)
   3. 공격자는 새로운 시퀀스 번호을 생서해 서버로 전송
   4. 서버는 새로운 시퀀스 번호을 받고 다시 세션을 오픈
   5. 공격자는 정상 연결처럼 서버와 시퀀스 번호를 교환 후 공격자, 서버 모두 Established 상태
  - 대응 방안
   > Sniffing, Spoofing 공격을 방어하기 위해 암호 프로토콜 적용
   > 패킷의 유실 및 재전송 증가 탐지
   > ACK Strom 탐지
   > - 서버는 이미 공격자와 동기화를 이룬 후, 클라이언트는 계속 정상 패킷을 전송
   > - 서버는 클라이언트의 스퀀스 번호는 정상적이지 않다고 인식하여 시퀀스 번호를 맞추기 위해 Server_My_Seq과 Client_My_Seq을 전송을 반복

### Http Only
   - XST 공격
   https://sabjili.tistory.com/entry/httponly를-우회하는-XST


      
   
   
 ### Web Storage 
  - Web Storage는 웹에 있는 저장소가 아니라 브라우저의 내부 저장소를 사용할 수 있게끔 제공하는 기능
  - 등장 배경은 Session의 Server 데이터 저장 문제점, 기존 클라이언트에 저장하는 Cookie 문제점, 적은 Cookie의 저장 공간(4KB -> 5MB), 웹 요청시 쿠키는 매번 서버로 전송
  
  
  
 ### Local Storage, Session Storage
  1. Local Storage
    - 사용자의 세션 데이터를 유지할 수 있고 브라우저를 닫았다가 다시 열었을 때도 지속, 탭을 여러개 열어도 공유
    - 도메인마다 별도로 스토리지가 생성
    - 명시적으로 javascript를 이용하여 삭제될 때까지 지속
    
  2. Session Storage
    - 브라우저 세션 기간 동안만 사용할 수 있으며 탭이나 창을 닫을 때 삭제
    - 도메인 마다 별도 스토리지가 생성
    - 같은 브라우저라도 새로 생성된 창에서는 세션이 달라 서로 다른 스토리지를 가짐
    
    

