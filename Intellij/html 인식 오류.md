# error-archive
Trouble Shooting

---

# 문제 정의

기존에 있던 html 파일들이 html이 나닌 문서(txt)로 인식되어 회색 글로만 나온다. 새로 만들어도 이미 문서로 연결이 되어있는지 파일명.html을 해도 문서형태로 작성됨

# 원인추론

html을 새로 만들면서 잘못된 이름 형식으로 오타가 나서 문서형태로 생성하면서 문서로 연결이 변경된 것 같다.

# 해결책 및 결론

File - File Properties - Associate with File Type에 들어간 뒤 File Pattern을 *.html로 하고(모든 html 파일) html을 클릭 후 OK

