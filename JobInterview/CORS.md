# CORS란 무엇인가

- 질문 의도 : 브라우저에서 크로스 오리진에 대해서 이해하고 있는가?
- [https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
- 보안 상의 이유로, 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청을 제한함
- 경험 및 해결 사례 문의
- 웹의 동일 출처 정책 (Same-Origin Policy)
  - 어떠한 문서나 스크립트가 다른 프로토콜, 포트, 호스트에 있는 리소스를 사용하는 것을 제한하는 정책
- CORS

  - HTTP 헤더를 사용해 클라이언트와 서버로 하여금 서로에 대해 인지하고 한 출처에서 다른 출처의 자원을 사용할 수 있게 하는 메커니즘
  - 클라이언트가 서버에 요청을 보낼 때 http 헤더의 origin 속성에 자동으로 값이 할당됨

  ```jsx
  Origin: http://company.com
  // 다른 출처의 자원을 사용하기 위해 요청이 올 경우,
  // 서버의 HTTP 응답 헤더에 다음과 같이 요청을 허용하는 도메인을 명시
  Access-Control-Allow-Origin: http://company.com
  ```

- [https://github.com/baeharam/Must-Know-About-Frontend/blob/main/Notes/security/sop.md](https://github.com/baeharam/Must-Know-About-Frontend/blob/main/Notes/security/sop.md)
