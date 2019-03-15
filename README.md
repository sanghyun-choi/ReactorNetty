# ReactorNetty

# Tcp서버에서 Reactor 활용
기존 reactor.netty.ipc 패키지에서 -> reactor.netty로 변경되었다.(0.8.5버전)
ReactorNetty는 기존 Netty서버 구성에 들이는 코드보다 더 간결해졌다.
기존과 동일하게 TCP, HTTP, UDP 등 프로토콜을 지원한다.
Reactor코드를 적용할 수 있고, 흐름 자체가 Reactor 방식으로 적용되어 있다.
<br/>
# TcpServer
TcpServer 객체의 create 메소드로 서버를 생성할 수 있다.
이 때 내부 구현을 보면 decorator패턴 형태로 계속해서 기능을 추가한다.
기존에 Netty에서 설정했던 ChannelFactory(스레드 설정) 및 EventLoop 설정 등을 동일하게 할 수 있다.
(LoopResource 설정 및 Option을 설정한다.)
<br/>
# doOn...종류
doOn종류의 메서드를 통해 handler를 통해 codec을 등록한다.
이때, doOn에서 client또는server에서 메시지를 보낼 경우에는 Mono타입은 불가하며 ByteBuf타입으로 받고 전송한다.
그러나, handle메서드에서는 Mono나 Flux타입으로 전송 가능하다.
(handle메소드에 등록한 Bifunction 자체가 클라이언트와 IO 통신 하는 로직)
<br/>
# doOn..상세
- doOnBind: serverChannel이 bind되었을때 호출, 서버 옵션 설정할때 필요해보임(ServerChannel handler 설정은 여기서 진행해야 한다.)
- doOnBound: serverChannel이 bound되었을때 호출, 위와 동일하지만 DisposableServer를 리턴, 연결 끊는것이 가능하다.
- doOnConnection: 클라이언트와 연동되었을때 호출, childHandler 설정 가능(내부적으로 connection에 대한 pipeline 설정)
- doOnUnBound: serverChannel 종료시, DispoabvleServer를 리턴, 연결 끊는 것이 가능하다.
<br/>
# ConnectionObserver
- 연결에 대한 context를 다룰 수 있음, 커넥션에 대한 이벤트 리스너, ThreadLocal같은 형태의 저장소라고 보면됨
- onStateChange: 커넥션에 상태 변화에 따라 값을 가져올 수 있다.
- then : chain형태로 여러 Observer 등록 가능
- currenctContext로 context가져오는 것도 가능하다.
- TcpServer.observe로 등록 가능
<br/>
# LoopResource
- TcpServer.runOn을 통해 기존의 Netty처럼 EventLoop 설정이 가능하다.


