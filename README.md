# ReactorNetty

1. Tcp서버에서 Reactor 활용을 위해 ReactorNetty 서버를 이용한다.
기존 reactor.netty.ipc 패키지에서 -> reactor.netty로 변경되었다.
ReactorNetty로 변경되면서 기존 Netty서버 구성에 들이는 코드보다 더 간결해졌다.
기존과 동일하게 TCP, HTTP, UDP 등 프로토콜을 지원한다.

2. TcpServer
TcpServer 객체를 통해서 decorator 패턴으로 계속해서 handler와 옵션을 추가해서 생성된다.
handler는 FunctionalInterface의 형태로 대부분 등록되어 차 후에 이벤트가 일어나면 실행된다.




<br/>
