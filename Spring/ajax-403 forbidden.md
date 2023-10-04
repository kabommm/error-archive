# error-archive
Trouble Shooting

---

# 문제 정의

댓글 저장을 위해 javascript 함수 호출 시 계속 403 에러가 발생했다.

# 원인추론

경로와 코드 문제는 없었다. 그래서 구글링을 해보니 csrf(Cross-site request forgery)의 token이 누락으로 발생일 수도 있다고 한다. 생각해보니 csrf를 설정한 후로 안됐던 것 같았다.

# 해결책 및 결론

```
<head>
    <meta name="_csrf_header" th:content="${_csrf.headerName}">
    <meta name="_csrf" th:content="${_csrf.token}">
</head>

...

<script th:inline="javascript">

var header = $("meta[name='_csrf_header']").attr('content');
var token = $("meta[name='_csrf']").attr('content');

...


$.ajax({
    url: '/replies/',
    ...
    
    beforeSend: function(xhr){
        xhr.setRequestHeader(header, token);
    },
    success: function(data) {
        console.log(data);
        ...
    }
})

...

</script>
```
위와 같이 jQuery ajax 요청시 csrf 값을 요청 전에 헤더에 담아서 보내면 이후 전송되는 Ajax 호출의 header에 csrf token이 추가되어 전송되기 때문에 csrf token으로 인한 403 에러는 발생하지 않는다.

# Reference

해결: <https://velog.io/@jyleedev/514-ajax-post-%ED%86%B5%EC%8B%A0-403-error>

