# error-archive
Trouble Shooting

---

# 문제 정의

로그인 API에서 JWT를 이용해서 회원 인증을 구현하는 중 java.lang.NoClassDefFoundError: javax/xml/bind/DatatypeConverter] with root cause 발생

# 원인추론

javax.xml.bind.DatatypeConverter 를 찾지 못하면서 발생한 에러였다. JDK 11 이 되면서 Java EE와 CORBA Module이 제거되었다고 한다.

# 해결책 및 결론

build.gradle에 implementation 'javax.xml.bind:jaxb-api:2.3.0' 의존성 추가

# Reference

- <https://jminie.tistory.com/123>

