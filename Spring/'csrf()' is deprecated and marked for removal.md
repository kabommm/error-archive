# error-archive
Trouble Shooting

---

# 문제 정의

SecurityConfig 부분의 기존 버전을 스프링 3.0이상에서 형식에 맞게 마이그레이션 하려는데 각 기능 밑에 빨간줄이 그어지며 "~~ is deprecated and marked for removal" 에러가 발생!

# 원인추론

버전이 바뀌면서 문법이 바뀐것 같아 구글링하였다.

# 해결책 및 결론

서로 무관한 애들끼리도 직렬로 이어지던 메서드 체이닝을 지양하고 함수형으로 잘 수납해서 쓰면 된다.

- 기존 코드

```
 .csrf().disable()

    .sessionManagement().sessionCreationPolicy(...)

    .and()
    .authorizeHttpRequests()
    // ...
```

- 함수형으로 수납된 코드

```
.csrf(이곳에 CSRF 설정을 위한 함수)

.sessionManagement(이곳에 세션 설정을 위한 함수)

.authorizeHttpRequest(이곳에 인가 설정을 위한 함수);
```

- 기존(Deprecated)

```
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    protected SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .csrf().disable()

                .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)

                .and()
                .authorizeHttpRequests()
                .anyRequest().permitAll();

        return http.build();
    }
}
```

- 변경된 코드

```
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    protected SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .csrf(AbstractHttpConfigurer::disable)
                .sessionManagement((sessionManagement) ->
                        sessionManagement.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
                )
                .authorizeHttpRequests((authorizeRequests) ->
                        authorizeRequests.anyRequest().permitAll()
                );

        return http.build();
    }
}
```

이미 잘 만들어진 메서드는 Method Reference 연산자로(::), 이제 작업할 함수는 람다식(()->{}) 등으로 전달하는 게 일반적이다.

# Reference

- <https://velog.io/@letsdev/Spring-Boot-3.1Spring-6.1-Security-Config-csrf-is-deprecated-and-marked-for-removal>

