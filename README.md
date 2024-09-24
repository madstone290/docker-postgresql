# Postgresql 도커 컨테이너
- 작업 디렉토리로 저장소의 파일을 이동한다
- `.env` 파일에서 환경 변수값을 설정한다
    - 명령어 사용시 편의상의 이유로 사용자는 `root` 추천
- 작업 디렉토리에서 `docker-compose up -d` 명령어를 실행한다
    - 컨테이너, 볼륨이 생성된다
- `data` 폴더에 가면 생성된 파일들을 확인할 수 있다.
- 원격 접속을 위해 `data/pg_hba.conf` 파일을 열고 아래 설정을 추가한다.
    ```
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    host    all             all             0.0.0.0/0               md5
    ```
- 로깅이 필요한 경우 `data/postgresql.conf` 파일을 열고 아래 설정을 추가한다.
    ```
    logging_collector = on
    log_directory = '/var/log/postgresql'
    log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
    log_statement = 'ddl'
    log_min_messages = 'info'
    log_min_error_statement = 'info'
    log_min_duration_statement = 0
    log_line_prefix = '%m [%p]: [%l-1] user=%u,db=%d '  # Time, process ID, line number, username, and database name.
    listen_addresses = '*'
    ```