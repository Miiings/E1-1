# Dockerfile 기반 웹 서버 실행

## Dockerfile 개념 이해

**Dockerfile은 "이미지를 만드는 설계도"입니다.**

- `FROM`: 베이스 이미지 지정 (어떤 환경에서 시작할지)
- `COPY`: 호스트의 파일을 컨테이너로 복사
- `RUN`: 이미지 빌드 과정에서 실행할 명령
- `CMD`: 컨테이너 실행 시 기본 명령 (진입점)

---

## 1. Dockerfile 작성

```dockerfile
FROM nginx:alpine
RUN echo "Dockerfile-nginx-webserver" > /usr/share/nginx/html/index.html
```

**각 라인 설명:**
- `FROM nginx:alpine`: Nginx 웹 서버 이미지 (Alpine Linux 기반, 용량 작음)
- `RUN`: 이미지 빌드 중에 명령 실행하여 HTML 파일 생성

---

## 2. 이미지 빌드

```bash
docker build -t my-web .
```

**옵션 설명:**
- `-t my-web`: 빌드된 이미지에 이름 지정 (태그)
- `.`: Dockerfile이 있는 현재 디렉토리

**출력 결과:**
```
[+] Building 3.2s (5/5) FINISHED
 => [internal] load build definition from Dockerfile
 => => transferring dockerfile: 121B
 => [base] FROM nginx:alpine
 => [1/1] RUN echo "Dockerfile-nginx-webserver" > /usr.../index.html
 => exporting to image
 => => exporting layers
 => => naming to docker.io/library/my-web:latest
```

---

## 3. 컨테이너 실행

```bash
docker run -d -p 8080:80 --name my-web my-web
```

**옵션 설명:**
- `-d`: 백그라운드 실행 (detach)
- `-p 8080:80`: 포트 매핑 (호스트:8080 ← 컨테이너:80)
- `--name my-web`: 컨테이너 이름 지정
- `my-web`: 실행할 이미지 이름

**출력:**
```
8bc95371db5dcf9f3f27e073fe861d44c65d8e24
```
(컨테이너 ID 반환)

---

## 4. 접속 확인

```bash
curl http://localhost:8080
```

또는 브라우저에서 `http://localhost:8080` 접속

**출력 결과:**
```
Dockerfile-nginx-webserver
```

**화면 확인:**
브라우저에서 페이지 로드 시 위 메시지가 표시되면 성공

---

## 핵심 요점

✅ Dockerfile은 이미지 빌드 과정을 자동화  
✅ `docker build`로 이미지 생성  
✅ `docker run`으로 컨테이너 실행  
✅ 포트 매핑으로 호스트와 컨테이너 연결