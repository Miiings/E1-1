# Dockerfile 기반 웹 서버 실행

## 1. Dockerfile 작성

```dockerfile
FROM nginx:alpine
RUN echo "Dockerfile-nginx-webserver" > /usr/share/nginx/html/index.html
```

---

## 2. 이미지 빌드

```bash
docker build -t my-web .
```

---

## 3. 컨테이너 실행

```bash
docker run -d -p 8080:80 --name my-web my-web
```

---

## 4. 접속 확인

```bash
curl http://localhost:8080
```

또는 브라우저 접속

(스크린샷 첨부)C