# error-archive
Trouble Shooting

---

# 문제 정의

게시판 기능에서 댓글을 작성을 했을때 detached entity passed to persist 발생

# 원인추론

DB 연관관계 문제일거라고 생각했다.

# 해결책 및 결론

검색을 해보니 에러 원인은 종속성 관계에 있었다. 

cascade = CascadeType.ALL로 종속성 설정이 되어있었기 때문에 cascade = CascadeType.ALL 설정이 적용된 writer을 저장하면 이와 관계를 맺은 값이 한번 더 저장이 되므로 에러가 발생한다.

왜냐하면 이미 저장된 값의 entity가 이미 DB에 등록되 키 값을 가지고 있기 때문!

따라서 cascade = CascadeType.ALL 옵션을 지워 종속성을 해제하면 이 에러가 해결된다.

# Reference

- <https://m.blog.naver.com/sim4858/220998440706>

