# UserServer

![Backend_One](https://img.shields.io/badge/Backend-Django-green)  ![python](https://img.shields.io/badge/Language-Python-green)

> UserServer는 `Frontend`와 `axios`를 사용해 통신합니다.
>
> (다른 Backend 서버들과 직접적으로 통신하지 않습니다.)
>
> UserServer는 `Django`로 구현되었습니다.
>
> MySql DB의 User 테이블과 연결되며, 로그인, 회원가입 등 유저와 관련된 사항들을 처리합니다.



## UserServer Construction

```python
📦gameBack
 ┣ 📂accounts				# 유저 정보 관련 App
 ┃ ┣ 📂migrations
 ┃ ┃ ┣ 📜0001_initial.py
 ┃ ┃ ┗ 📜__init__.py
 ┃ ┣ 📜adapter.py
 ┃ ┣ 📜admin.py
 ┃ ┣ 📜apps.py
 ┃ ┣ 📜consumers.py
 ┃ ┣ 📜models.py
 ┃ ┣ 📜routing.py
 ┃ ┣ 📜serializers.py
 ┃ ┣ 📜tests.py
 ┃ ┣ 📜token_auth.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜views.py
 ┃ ┗ 📜__init__.py
 ┣ 📂gameBack				# UserServer의 setting을 위한 디렉토리
 ┃ ┣ 📜asgi.py
 ┃ ┣ 📜routing.py
 ┃ ┣ 📜settings.py
 ┃ ┣ 📜urls.py
 ┃ ┣ 📜wsgi.py
 ┃ ┗ 📜__init__.py
 ┣ 📜manage.py
 ┗ 📜requirements.txt
```



## Sequence Diagram

> 회원가입, 로그인 및 회원 정보 확인 sequence diagram

```mermaid
sequenceDiagram

AuthPage->>UserServer: 닉네임/아이디 중복 확인 요청
UserServer->>DB:데이터 조회
DB-->>UserServer:결과 전달
UserServer-->>AuthPage: 결과 전달
AuthPage->>UserServer: 로그인/회원가입 요청
UserServer->>DB: 계정 CRUD
DB-->>UserServer: token 전달
UserServer-->>AuthPage: 회원 인증용 토큰 전달
AuthPage->>AuthPage: sessionStorage에 토큰값 저장
AuthPage->>enterLobbyPage:페이지 전환
enterLobbyPage->>LobbyPage:페이지 전환
```





| 이름             | 위치     | 역할                   | 포트번호/주소 |
| ---------------- | -------- | ---------------------- | ------------- |
| `AuthPage`       | Frontend | 로그인/회원가입 페이지 | -             |
| `EnterLobbyPage` | Frontend | 로비 이동 페이지       | -             |
| LobbyPage        | Frontend | 로비 페이지            | -             |
| `UserServer`     | Backend  | 사용자 CRUD 서버       | 8000          |
| `DB`             | DataBase | 전체 Database (MySQL)  | 3306          |