# Docker 운영 명령

## 컨테이너 상태 관리 흐름

컨테이너는 생성 → 실행 → 중지 → 삭제의 라이프사이클을 가집니다. 각 단계에서 상태를 확인해야 합니다.

---

## 1. 이미지 확인
```bash
docker images
```

**설명:**
- 로컬에 저장된 모든 Docker 이미지를 나열 -> 내가 실행할 수 있는 환경
- `REPOSITORY`, `TAG`, `IMAGE ID`, `SIZE` 등 주요 정보 표시

**출력 결과:**
```
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu        latest    c6b84b685f35   2 weeks ago    77.8MB
nginx         alpine    a92c4d764cde   3 weeks ago    42.8MB
hello-world   latest    d2c94e258dcb   3 months ago   13.3kB
```

---

## 2. 컨테이너 상태 확인

```bash
docker ps          # 실행 중인 컨테이너
docker ps -a       # 모든 컨테이너 (중단된 것 포함)
```

**설명:**
- `docker ps`: 현재 실행 중인 컨테이너만 조회
- `docker ps -a`: 종료된 컨테이너도 포함한 모든 컨테이너 조회
- `CONTAINER ID`, `IMAGE`, `STATUS` 정보로 컨테이너 상태 파악

**출력 결과:**
```
CONTAINER ID   IMAGE     COMMAND   CREATED       STATUS
8bc95371db5d   nginx     "nginx"   5 hours ago   Up 2 hours
9f2e4a8c9d1b   ubuntu    "bash"    1 day ago     Exited (0) 3 hours ago
```

---

## 3. 로그 확인

```bash
docker logs <container_id>
docker logs -f <container_id>     # 실시간 로그 추적
```

**설명:**
- 컨테이너에서 발생한 모든 표준 출력/미비 출력 확인 -> 내부 파일 직접보기 어려움
- 웹 서버나 데이터베이스 등의 로그를 디버깅할 때 중요
- 애플리케이션 에러 추적 및 상태 모니터링에 활용

**출력 결과:**
```
2026-04-08T12:34:56.789Z [INFO] Server started on port 80
2026-04-08T12:34:57.123Z [INFO] Connected database
```

---

## 4. 리소스 사용량 확인

```bash
docker stats
```

**설명:**
- 실시간으로 관찰되는 컨테이너의 CPU, 메모리, 네트워크 사용률 표시
- 도커 컨테이너의 리소스 사용률을 모니터링할 때 중요
- `quit` 또는 `Ctrl+C`로 중단 가능

**출력 결과:**
```
CONTAINER ID   NAME          CPU %     MEM USAGE / LIMIT
8bc95371db5d   quirky_jones  0.00%     4.219MiB / 7.777GiB
```

---

## 심층 인터뷰 관련 설명

이 미션에서 가장 어려웠던 지점은 포트 매핑 실패였습니다. 가설로는 호스트 포트 충돌, 확인으로는 netstat 명령어로 포트 사용 상태를 확인, 조치로는 다른 포트 번호를 사용하여 문제를 해결했습니다. 근거는 Docker 로그와 시스템 명령어로 진단하였습니다.