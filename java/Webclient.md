 : WebClient는 RestTemplate를 대체하는 HTTP 클라이언트
> 역할
- 기존의 동기 API를 제공할 뿐만 아니라, 논블로킹 및 비동기 접근 방식을 지원
- 요청을 나타내고 전송하게 해주는 빌더 방식의 인터페이스를 사용하며, 외부 API로 요청을 할 때 리액티브 타입의 전송과 수신(Mono, Flux)

> 특징
- 싱글스레드
- Non-Blocking
- JSON.XML 응답 용이
- 참고)
-> <img width="1349" alt="스크린샷 2022-07-08 오후 4 36 28" src="https://user-images.githubusercontent.com/59461124/177942101-622a7065-ad49-4390-8885-3bde88ecce12.png">

