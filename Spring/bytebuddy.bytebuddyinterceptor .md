# error-archive
Trouble Shooting

---

# 문제 정의

노트북의 스프링 2.x 버전을 데스크탑의 스프링 3.0이상에서 테스트하면서 게시글 작성과 댓글을 작성한 뒤 마이페이지를 접속한 결과  "class org.hibernate.proxy.pojo.bytebuddy.bytebuddyinterceptor cannot access a member of class com.example.basic.domain.baseentity with modifiers "public"" 에러가 발생!

# 원인추론

Baseentity 부분의 문제인 것 같아 구글링하였다.

# 해결책 및 결론

기존의 BaseEntity class는 abstract(추상) 클래스였으나 public class로 변경


# Reference

- <https://java8.tistory.com/512>

