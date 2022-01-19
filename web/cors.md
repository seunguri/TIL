# SOP
Access to XMLHttpRequest at '주소A' from origin '주소B' has been blocked by CORS policy

Origin -> Scheme://Host:Port

다른 Origin에서 온 자원들을 모두 사용할 수 없게 차단했다면 CDN과 같은 것을 사용하기 어려웠을 것이다.
<img>, <script>, <link>, <iframe>과 같은 특정 HTML Tag는 다른 Origin으로부터 온 것은 임베딩할 수 있게 허용해준다. (임베딩만 가능하고 데이터를 읽는 건 보안상의 이유로 차단한다.)
다른 Origin의 데이터를 읽고 싶으면 CORS 표준을 지켜서 내 사이트로부터의 응답에 "다른 Origin이더라도 허용해줘!" 라고 말해주면 된다.

# CORS
### iframe
iframe.content, window.parent, window.open, window.opener
- Same-Origin: 상호간의 document에 자유롭게 접근 가능
- Cross-Origin: 상호간의 document에 접근 불가, 매우 제한적인 객체에만 접근이 가능

Cross-Origin간 데이터 교환
window.postMessage

### XMLHttpRequest
- Cross-Origin인 경우 Write/쓰기는 일반적으로 가능함. (Preflight면 다른 오리진끼리 요청도 못함)
- embedding은 가능함.
- read는 실패함.

> Preflight Request의 경우
> 다른 Origin 요청을 보낼 때 미리 내 요청을 받을 수 있는지 확인하기 위해서 사전 요청(Preflight Request)을 보낸다. 그러고 나서 가능하면 나의 실제 요청을 보내고 응답을 받는다.

### 통신 방법
1. ~JSONP: 모든 origin을 대상으로 SOP 무력화~ 쓰지마
2. CORS: Access-Control-Allow-Origin에 origin 추가

### 검사
1. Access-Control-Allow-Origin에는 *를 사용할 수 없으며, 명시적인 URL이어야한다.
응답 헤더에는 반드시 Access-Control-Allow-Credentials: true가 존재해야한다.

이 헤더는 Nginx나 Apache와 같은 서버 엔진의 설정에서 추가할 수도 있지만, 아무래도 복잡한 세팅을 하기는 불편하기 때문에 소스 코드 내에서 응답 미들웨어 등을 사용하여 세팅하는 것을 추천한다. Spring, Express, Django와 같이 이름있는 백엔드 프레임워크의 경우에는 모두 CORS 관련 설정을 위한 세팅이나 미들웨어 라이브러리를 제공하고 있으니 세팅 자체가 어렵지는 않을 것이다.

# 해결
🐸  authenticate 설정 후 이렇게 된 것!!
```
CORS_ORIGIN_WHITELIST = ['http://127.0.0.1:3000' ,'http://localhost:3000'] 
CORS_ALLOW_CREDENTIALS = True
```

- https://coding-groot.tistory.com/91
- https://evan-moon.github.io/2020/05/21/about-cors/