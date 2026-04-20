# 바인드 마운트 및 Docker 볼륨

## 개념 이해

컨테이너는 **격리된 환경**으로, 기본적으로 컨테이너 내부에서만 데이터가 유지됩니다.

- **포트 매핑**: 네트워크 통신을 위한 포트 연결
- **바인드 마운트**: 호스트 파일 시스템을 컨테이너에 직접 연결 (개발 중 실시간 반영)
- **Docker 볼륨**: Docker가 관리하는 저장소 (데이터 영속성, 이식성)

---

## 1. 바인드 마운트

```bash
# app 디렉토리를 준비
mkdir app
echo "<h1>Dockerfile-nginx-webserver</h1>" > app/index.html

# 바인드 마운트로 컨테이너 실행
docker run -v $(pwd -P)/app:/usr/share/nginx/html -d -p 8080:80 my-image
```

**호스트에서 파일 수정:**
```bash
echo "<h1>modified</h1>" > app/index.html
```

브라우저에서 **즉시 새 내용이 반영됨**

**장점:**
- 개발 중 파일 수정 시 컨테이너를 다시 시작할 필요 없음
- 실시간 반영 가능

**단점:**
- 호스트 환경에 의존적
- 이식성이 낮음 (다른 머신에서는 경로가 다를 수 있음)

---

## 2. Docker 볼륨 생성

```bash
docker volume create my-volume
```

**확인:**
```bash
docker volume ls
```

**출력:**
```
DRIVER    VOLUME NAME
local     my-volume
```

---

## 3. 볼륨 연결 컨테이너 실행

```bash
docker run -d --name vol-test -v my-volume:/data ubuntu sleep infinity
```

**옵션 설명:**
- `-v my-volume:/data`: Docker 볼륨 마운트 - 컨테이너 삭제 후에도 데이터가 유지됨
  - 볼륨 이름: `my-volume`
  - 컨테이너 마운트 경로: `/data`
- `sleep infinity`: 컨테이너를 계속 실행 상태로 유지

---

## 4. 데이터 생성 및 확인

```bash
docker exec -it vol-test bash
```

컨테이너 내에서:
```bash
echo "hello" > /data/test.txt
cat /data/test.txt
exit
```

**출력:**
```
hello
```

---

## 5. 컨테이너 삭제 후 재확인

```bash
# 첫 번째 컨테이너 삭제
docker rm -f vol-test

# 동일 볼륨으로 새 컨테이너 생성
docker run -d --name vol-test2 -v my-volume:/data ubuntu sleep infinity

# 데이터 확인
docker exec -it vol-test2 bash
```

컨테이너 내에서:
```bash
cat /data/test.txt
exit
```

**출력:**
```
hello
```