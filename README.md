### Stateless
  1. http 통신이 끝나면 상태를 유지하지 않는 특성
  2. 부하를 현저하게 줄일 수 있지만 매번 request를 보내야하는 상황 발생
 
 
 
### Cookie, Session
 - 위와 같은 http 프로토콜의 단점을 보완하고자 등장
 - 클라이언트와 서버의 통신 정보 및 상태를 기록하여 다시 접속 시 그대로 정보를 유기하기 위한 것
  
  
  
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
   - 브라우저가 active 상태일 때 까지만 유효하게 설정하려면 유효 시간 세팅을 하지 않음(ex. 온라인 뱅킹)
   
   
   
 ### Web Storage 
  - Web Storage는 웹에 있는 저장소가 아니라 브라우저의 내부 저장소를 사용할 수 있게끔 제공하는 기능
  - 등장 배경은 Session의 Server 데이터 저장 문제점, 기존 클라이언트에 저장하는 Cookie 문제점, 적은 Cookie의 저장 공간(4KB -> 5MB), 웹 요청시 쿠키는 매번 서버로 전송
  
  
  
 ### Local Storage, Session Storage
  1. Local Storage
    - 사용자의 세션 데이터를 유지할 수 있고 브라우저를 닫았다가 다시 열었을 때도 지속, 탭을 여러개 열어도 공유
    - 도메인마다 별도로 스토리지가 생성
    - 명시적으로 삭제될 때까지 지속
    
  2. Session Storage
    - 브라우저 세션 기간 동안만 사용할 수 있으며 탭이나 창을 닫을 때 삭제
    - 도메인 마다 별도 스토리지가 생성
    - 같은 브라우저라도 새로 생성된 창에서는 세션이 달라 서로 다른 스토리지를 가짐
    
    
 ### Set-Cookie
   - 
