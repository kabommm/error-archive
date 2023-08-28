# error-archive

Trouble Shooting

---

# 문제 정의

![](https://github.com/kabommm/error-archive/blob/main/img/actual%20and%20formal%20argument%20lists%20differ%20in%20length.PNG)

model.addAttribute로 MemberDTO 객체를 가져오는데 위와 같은 오류가 발생

# 원인추론

기존에 오류가 없었던 MemberForm과 MemberDTO의 차이를 비교해보았을 때 어노테이션의 차이가 있었다.

# 해결책 및 결론

@AllArgsConstructor, @NoArgsConstructor 어노테이션을 추가해주니 해결

@Builder를 사용하는 Dto에는 Builder 이용 시 컴파일 에러 방지하는 어노테이션인 @AllArgsConstructor, @NoArgsConstructor가 있어야 한다. 
