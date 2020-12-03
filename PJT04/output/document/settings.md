# settings

> 해당 문서는 **그리고 아무도 없었다**의 코드를 실행하기 위한 setting들을 모아둔 문서입니다.



## DataBase (MySQL)

> Django와 Spring을 둘 다 쓰기 때문에 Django의 default DB인 sqlite를 사용하지 않고 mysql을 사용

- WorkBench 8.0을 사용해서 Docker를 사용하지 않음

1. DataBase 명 `game`, 비밀번호 `1234`로 설정

2. sql문을 통해 Table 생성
   - [sql문 바로가기](../database/sql.txt)

3. Django - migrate 필요 (UserServer - `gameBack/`)

   ```bash
   $ python manage.py makemigrations
   $ python manage.py migrate
   ```

### Modify DB

- gameBack/accounts/migrations 폴더 내의 `0001_initial.py` 파일 삭제

- migrate 과정을 통해 DB 연결 완료



## Frontend (Vue.js)

> Frontend는 오직 `Vue.js`만 사용하여 구현하였습니다.
>
> npm을 사용해서 실행한다.

1. 패키지 설치

   ```bash
   $ cd game-front/
   $ npm i
   ```

2. Vue.js 실행

   ```bash
   $ npm run serve
   ```



## Backend - UserServer(Django)

> 가상환경 venv를 사용해서 설정한다.

1. 가상환경 생성

   ```bash
   $ cd gameBack/
   $ python -m venv venv
   ```

   - 반드시 실행 전에 `python --version`으로 python이 3.7 이상임을 확인한다.
     - 3.5 등의 하위 버전에서는 가상환경에 문제가 생길 수 있음

2. 가상 환경 들어가기

   ```bash
   $ source venv/Scripts/activate
   # 만약 맥 환경이면
   $ source venv/bin/activate
   ```

3. 패키지 인스톨

   ```bash
   $ pip install -r requirements.txt
   ```

4. Django 실행

   ```bash
   $ python manage.py runserver
   ```

5. 가상 환경 나오기

   ```bash
   $ deactivate
   ```



## Backend - AIServer(Django)

> 기본 환경에서 실행했으므로 package를 따로 설치해주어야했다.

1. 디렉토리 이동

   ```bash
   $ cd gameAI/
   ```

2. 설치해야할 패키지 목록

   ```txt
   Cython==0.29.21
   darkflow
   Django==3.1.1
   django-cors-headers==3.5.0
   Keras-Applications==1.0.8
   Keras-Preprocessing==1.1.2
   numpy==1.19.2
   Pillow==7.2.0
   tensorflow==1.14.0
   tensorflow-estimator==1.14.0
   tensorflow-gpu==2.0.0
   ```

3. 패키지 설치

   ```bash
   $ pip install 패키지명
   ```

4. Django 실행

   ```bash
   $ python manage.py runserver 8005
   ```

   

## Backend - InGameServer, LobbyServer (Spring)

> STS를 사용한다.
>
> open directory로 `game_InGame` / `game_Lobby` 을 불러와서 각각 오른쪽 마우스 -> `Run As` -> `Spring Boot App`으로 실행한다.