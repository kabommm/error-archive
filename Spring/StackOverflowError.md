# error-archive
Trouble Shooting

---

# 문제 정의

스프링 시큐리티의 설정에서 카카로 계정으로 로그인처리를 하기 위한 AuthenticationManager authenticationManager 를 가져와서 로직 실행을 하였더니

"Handler dispatch failed; nested exception is java.lang.StackOverflowError" 에러 발생

# 원인추론

검색해보니 authenticationManager()가 아니라 authenticationManagerBean()를 사용해야 한다고 한다.

# 해결책 및 결론

기존 코드를 아래와 같이 바꾼다.

```
//기존 코드
@Bean   //스프링 시큐리티의 인증(로그인 구현시 사용)
AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception {
        return authenticationConfiguration.getAuthenticationManager();
}

//변경 코드
@Bean   //스프링 시큐리티의 인증(로그인 구현시 사용)
public AuthenticationManager authenticationManagerBean() throws Exception {
    return super.authenticationManagerBean();
}
```

++ 최신

위의 변경 코드로도 StackOverflow가 발생하여 아래와 같이 코드를 수정하였다.

@Bean   //스프링 시큐리티의 인증(로그인 구현시 사용)
AuthenticationManager authenticationManager(AuthenticationConfiguration authenticationConfiguration) throws Exception{
        DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
        provider.setUserDetailsService(userDetailsService);
        provider.setPasswordEncoder(passwordEncoder());
        return new ProviderManager(provider);
}

# Reference

- <https://samtao.tistory.com/47>
- 최신 변경 코드: <https://hbyun.tistory.com/178>

