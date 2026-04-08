# Docker 기본 실습

## 개념 이해

### 이미지 vs 컨테이너
- **이미지**: 실행 환경이 정의된 템플릿 (레시피에 비유 가능)
- **컨테이너**: 이미지를 기반으로 실행된 실제 프로세스 (요리에 비유 가능)
- 하나의 이미지에서 여러 컨테이너를 생성할 수 있음

### Docker 기본 명령어 개요
- `docker run`: 컨테이너 실행
- `docker ps`: 실행 중인 컨테이너 확인
- `docker images`: 이미지 목록 확인
- `docker logs`: 컨테이너 로그 확인
- `docker stats`: 리소스 사용량 확인

---

## 1. Docker 설치 확인
```bash
docker --version
docker info
```
**출력 결과:**
<img width="346" height="32" alt="Image" src="https://github.com/user-attachments/assets/547526bd-7c55-47a9-9f30-992a42e48fc2" />
<img width="581" height="662" alt="Image" src="https://github.com/user-attachments/assets/7612cce5-dd7d-4111-96c1-e77e641515bc" />
---

## 2. hello-world 실행

```bash
docker run hello-world
```

**설명:**
- Docker가 설치되고 정상 작동하는지 확인하는 가장 간단한 테스트
- 원격 저장소에서 `hello-world` 이미지를 다운로드 후 컨테이너로 실행

**출력 결과:**
<img width="610" height="388" alt="Image" src="https://github.com/user-attachments/assets/f4e17e2a-4f12-439a-a346-a48be090412a" />

---

## 3. Ubuntu 컨테이너 실행 및 진입

```bash
docker run -it ubuntu bash
```

**옵션 설명:**
- `-i` (--interactive): 표준 입력을 열어둠 (대화형)
- `-t` (--tty): 터미널 할당
- `bash`: 컨테이너 내부에서 실행할 셸

**컨테이너 내부에서 실행:**
```bash
ls
echo "abc"
exit  # 컨테이너 빠져나가기
```

**출력 결과:**
<img width="621" height="275" alt="Image" src="https://github.com/user-attachments/assets/ef11067e-49ea-4ca8-90b5-2fbb71e15330" />

**핵심 포인트:**
- 컨테이너는 격리된 환경: 호스트와 별도의 파일시스템 보유
- `-it` 옵션 없으면 쉘 접근 불가능
