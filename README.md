# ReactorNetty

# Tcp서버에서 Reactor 활용을 위해 ReactorNetty 서버를 이용한다.
기존 reactor.netty.ipc 패키지에서 -> reactor.netty로 변경되었다.(0.8.5버전)
ReactorNetty로 변경되면서 기존 Netty서버 구성에 들이는 코드보다 더 간결해졌다.
기존과 동일하게 TCP, HTTP, UDP 등 프로토콜을 지원한다.
<br/>
# TcpServer
TcpServer 객체를 통해서 decorator 패턴으로 계속해서 handler와 옵션을 추가해서 생성된다.
handler는 FunctionalInterface의 형태로 대부분 등록되어 차 후에 이벤트가 일어나면 실행된다.
라이프 사이클에 존재하는듯 하다.
<br/>
# doOn...종류
doOn종류의 메서드를 통해 handler를 통해 codec을 등록한다.
이때, doOn에서 client또는server에서 메시지를 보낼 경우에는 Mono타입은 불가하며 ByteBuf타입으로 받고 전송한다.
그러나, handle메서드에서는 Mono나 Flux타입으로 전송 가능하다.
<br/>
# doOn..상세
- doOnBind: serverChannel이 bind되었을때 호출, 서버 옵션 설정할때 필요해보임
- doOnBound: serverChannel이 bound되었을때 호출, 위와 차이점 모르겠음
- doOnConnection: 클라이언트와 연동되었을때 호출 codec 설정 필요
- doOnUnBound: serverChannel 종료시 
<br/>
