# error-archive
Trouble Shooting

---

# 문제 정의

![](https://github.com/kabommm/error-archive/blob/main/img/MySQL_Error.PNG)

'spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver'에서 Driver에 빨간불이 뜨며 cannot resolve class or package 발생

# 원인추론

https://start.spring.io/ 에서 의존성을 추가 할 때 MySQL Driver을 추가하지 않고 build.gradle에 단순히 runtimeOnly 'com.mysql:mysql-connector-j'를 추가했기 때문에 문제가 생겼다고 생각했다.

# 해결책 및 결론

재부팅으로 해결

