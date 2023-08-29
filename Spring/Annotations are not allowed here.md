# error-archive
Trouble Shooting

---

# 문제 정의

DTO에서 검증을 위해   @Pattern 어노테이션에서 정규식을 작성중 Annotations are not allowed here라는 에러가 생겼다.

# 원인추론

정규식이 잘못되었는지 한참을 고민하였다.

# 해결책 및 결론

```
@Pattern(regexp = "^[a-zA-Z]*$", message = "영문 또는 숫자만 가능합니다.");
```

위 코드와 같이 어노테이션 마지막에 ;를 붙혀버렸기에 에러가 났었다.
새벽 3시에 코딩이라 피로 이슈인듯 하다.

혹시나 언젠가 이런 에러를 또 맞딱뜨릴 경우 ; 때문이라는 것을 상기하기 위해 이를 기록한다..

