# 바인드 마운트 및 Docker 볼륨

## 1. 바인드 마운트

```bash
docker run -v $(pwd)/app:/usr/share/nginx/html -d -p 8080:80 my-web
```

* 호스트에서 파일 수정 후 브라우저 반영 확인

(수정 전/후 스크린샷 첨부)

---

## 2. Docker 볼륨 생성

```bash
docker volume create my-volume
```

---

## 3. 볼륨 연결 컨테이너 실행

```bash
docker run -d --name vol-test -v my-volume:/data ubuntu sleep infinity
```

---

## 4. 데이터 생성 및 확인

```bash
docker exec -it vol-test bash
echo "hello" > /data/test.txt
cat /data/test.txt
```

---

## 5. 컨테이너 삭제 후 재확인

```bash
docker rm -f vol-test

docker run -d --name vol-test2 -v my-volume:/data ubuntu sleep infinity
docker exec -it vol-test2 bash
cat /data/test.txt
```

* 동일 데이터 유지 확인

(스크린샷 첨부)