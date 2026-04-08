# 바인드 마운트 및 Docker 볼륨

## 개념 이해

컨테이너는 **격리된 환경**으로, 기본적으로 컨테이너 내부에서만 데이터가 유지됩니다.

- **포트 매핑**: 네트워크 통신을 위한 포트 연결
- **바인드 마운트**: 호스트 파일 시스템을 컨테이너에 직접 연결 (개발 중 실시간 반영)
- **Docker 볼륨**: Docker가 관리하는 저장소 (데이터 영속성, 이식성)

---

## 1. 포트 매핑

```bash
docker run -d -p 8080:80 my-web
```

**옵션 설명:**
- `-d`: 백그라운드 실행
- `-p 8080:80`: 포트 매핑 (호스트의 8080 포트 → 컨테이너의 80 포트)

**포트 매핑이 필요한 이유:**
- 컨테이너 내부는 외부와 격리되어 있음
- 호스트에서 컨테이너 내 애플리케이션에 접근하려면 포트를 연결해야 함

**확인:**
```bash
curl http://localhost:8080
docker port my-web
```

**출력:**
```
80/tcp -> 0.0.0.0:8080
```

---

## 2. 바인드 마운트

```bash
# app 디렉토리를 준비
mkdir app
echo "<h1>Hello from Host</h1>" > app/index.html

# 바인드 마운트로 컨테이너 실행
docker run -v $(pwd)/app:/usr/share/nginx/html -d -p 8080:80 my-image
```

**옵션 설명:**
- `-v $(pwd)/app:/usr/share/nginx/html`: 바인드 마운트
  - 호스트 경로: `$(pwd)/app`
  - 컨테이너 경로: `/usr/share/nginx/html`

**호스트에서 파일 수정:**
```bash
echo "<h1>Updated from Host</h1>" > app/index.html
```

브라우저에서 **즉시 새 내용이 반영됨**

**장점:**
- 개발 중 파일 수정 시 컨테이너를 다시 시작할 필요 없음
- 실시간 반영 가능

**단점:**
- 호스트 환경에 의존적
- 이식성이 낮음 (다른 머신에서는 경로가 다를 수 있음)

---

## 3. Docker 볼륨 생성

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

## 4. 볼륨 연결 컨테이너 실행

```bash
docker run -d --name vol-test -v my-volume:/data ubuntu sleep infinity
```

**옵션 설명:**
- `-v my-volume:/data`: Docker 볼륨 마운트
  - 볼륨 이름: `my-volume`
  - 컨테이너 마운트 경로: `/data`
- `sleep infinity`: 컨테이너를 계속 실행 상태로 유지

---

## 5. 데이터 생성 및 확인

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

## 6. 컨테이너 삭제 후 재확인

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

**핵심점:** 
✅ 컨테이너가 삭제되었지만 데이터는 **여전히 존재**함  
✅ 동일 볼륨을 다른 컨테이너에서도 사용 가능

---

## 바인드 마운트 vs Docker 볼륨

| 특성 | 바인드 마운트 | Docker 볼륨 |
|------|------------|-----------|
| 관리 | 호스트의 임의 위치 | Docker이 관리 |
| 이식성 | 낮음 (경로 의존) | 높음 (어디서나 사용 가능) |
| 성능 | 약간 느림 | 더 빠름 |
| 데이터 영속성 | 호스트 파일 유지 | Docker 볼륨 유지 |
| 개발용도 | 실시간 반영 필요할 때 ✓ | 프로덕션 데이터 ✓ |

---

## 트러블슈팅

### 문제 1: 데이터가 유지되지 않음
**원인:** 마운트 옵션 미설정으로 컨테이너 내부 저장만 사용  
**해결:** `-v` 옵션으로 바인드 마운트 또는 볼륨 설정

### 문제 2: 호스트 파일이 반영되지 않음
**원인:** 컨테이너 경로가 잘못 지정됨  
**해결:** `docker exec`로 컨테이너 내부를 직접 확인하여 경로 검증

### 문제 3: 포트 충돌
**원인:** 이미 사용 중인 포트로 매핑 시도  
**해결:** 다른 포트 번호 사용 (예: `-p 8081:80`)