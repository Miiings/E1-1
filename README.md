# AI/SW 개발 워크스테이션 구축

## 1. 프로젝트 개요
터미널, Docker, Git을 활용하여 개발 환경을 구축하고, 동일한 환경을 재현 가능하도록 정리하는 것을 목표로 한다.

주요 수행 내용
- 작업 디렉토리 및 권한 정리
- Docker 설치 및 점검
- 컨테이너 실행 및 관리
- 웹 서버 Dockerfile 작성 및 이미지 빌드
- 포트 매핑 접속 확인
- 바인드 마운트 및 Docker 볼륨 검증
- Git 설정 및 GitHub 저장소 연동

---

## 2. 실행 환경
- OS:
```
cjdrbf223275@c4r9s4 ~ % sw_vers
ProductName:		macOS
ProductVersion:		15.7.4
BuildVersion:		24G517
```
- Shell / Terminal:
```
cjdrbf223275@c4r9s4 ~ % echo $SHELL
/bin/zsh
```
- Docker:
```
cjdrbf223275@c4r9s4 ~ % docker --version
Docker version 28.5.2, build ecc6942
```
- Git:
```
cjdrbf223275@c4r9s4 ~ % git --version
git version 2.53.0
```

---

## 3. 수행 항목 체크리스트
- [x] 터미널 기본 명령어 실습
- [x] 파일/디렉토리 권한 변경 실습
- [x] Docker 설치 및 점검
- [x] hello-world 실행
- [x] Ubuntu 컨테이너 실행 및 내부 명령 수행
- [x] Docker 운영 명령 실행
- [x] Dockerfile 기반 이미지 빌드
- [x] 포트 매핑 접속 확인
- [x] 바인드 마운트 반영 확인
- [x] Docker 볼륨 영속성 검증
- [x] Git 설정 및 GitHub 연동

---

## 4. 수행 로그

### 4.1 터미널 조작
- 현재 위치 확인
- 디렉토리 생성 / 이동
- 파일 생성 / 복사 / 이동 / 삭제
- 파일 내용 확인
- 권한 변경

상세 로그: [docs/1-terminal.md](./docs/1-terminal.md)

### 4.2 Docker 기본 실습
- docker --version
- docker info
- docker run hello-world
- docker run -it ubuntu bash

상세 로그: [docs/2-docker-basic.md](./docs/2-docker-basic.md)

### 4.3 Docker 운영 명령
- docker images
- docker ps / docker ps -a
- docker logs
- docker stats

상세 로그: [docs/3-docker-ops.md](./docs/3-docker-ops.md)

### 4.4 Dockerfile 기반 웹 서버 실행
- Dockerfile 작성
- 이미지 빌드
- 컨테이너 실행
- 웹 서버 접속 확인

상세 로그: [docs/4-dockerfile.md](./docs/4-dockerfile.md)

### 4.5 바인드 마운트 / 볼륨
- 바인드 마운트 반영 확인
- Docker 볼륨 생성 및 연결
- 컨테이너 삭제 전/후 데이터 유지 확인

상세 로그: [docs/5-storage.md](./docs/5-storage.md)

### 4.6 Git / GitHub 연동
- git config 설정
- 저장소 생성
- 원격 저장소 연결 및 push

상세 로그: [docs/6-git.md](./docs/6-git.md)

---

## 5. 검증 방법

### Docker 설치 확인
```bash
docker --version
docker info

### 컨테이너 실행 확인

```
```bash
docker run hello-world
docker ps -a
```

### 웹 서버 실행 및 포트 매핑 확인

```
docker build-t my-web .
docker run-d-p8080:80--name my-web my-web
curl http://localhost:8080
```

- 브라우저에서 [http://localhost:8080](http://localhost:8080/) 접속 시 정상 화면 확인

### 바인드 마운트 확인

- 호스트에서 index.html 수정
- 브라우저 또는 curl 결과 변경 여부 확인

### Docker 볼륨 확인

- 볼륨 생성 후 컨테이너에 연결
- 컨테이너 내부에서 파일 생성
- 컨테이너 삭제 후 동일 볼륨으로 재실행
- 동일 파일 존재 여부 확인

### Git 연동 확인

```
git config--list
git remote-v
git log--oneline
```

---

## 6. 트러블슈팅

### 문제 1. 포트 충돌로 컨테이너 실행 실패

- 원인: 이미 사용 중인 포트에 매핑 시도
- 해결: 다른 포트로 변경하여 실행 (예: 8081:80)

---

### 문제 2. 컨테이너 삭제 후 데이터가 사라짐

- 원인: 컨테이너 내부 파일 시스템만 사용
- 해결: Docker 볼륨을 생성하고 컨테이너에 연결하여 데이터 영속성 확보
