# error-archive
Trouble Shooting

---

# 문제 정의

APPLICATION FAILED TO START

Description:

Web server failed to start. Port 8080 was already in use.

# 원인추론

이전 프로젝트에서 8080 포트가 사용중이다.

# 해결책 및 결론

- 다른 프로젝트의 어플리케이션을 중지(빨간색 네모)시키고 Run을 한다.

- application.properties에 새로운 포트를 만들어 사용한다.  ----- server.port=9090

