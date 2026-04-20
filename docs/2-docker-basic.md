# Docker 기본 실습

## 개념 이해

### 도커 쓰는 이유
어디서 실행해도 동일하게 동작하는 환경을 하나로 묶어서 배포
- 호스트: 컨테이너를 실행하는 실제 컴퓨터
- 호스트와 OS 커널을 공유해서 VM처럼 os 복사할 필요는 없지만 파일/프로세스/네트워크는 격리됨 -> 가볍지만 독립적인 환경

### 이미지 vs 컨테이너
- **이미지**: 실행 환경이 정의된 템플릿 (설계도, 레시피) - 빌드 시 생성되며 변경 불가능
- **컨테이너**: 이미지를 기반으로 실행된 실제 프로세스 (인스턴스, 요리) - 실행 시 생성되며 변경 가능하지만 일시적
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
**설명:**
- `docker --version`: Docker 버전을 확인하여 설치 상태를 검증 / 출력 예: "Docker version 24.0.5, build ced0996".
- `docker info`: Docker 데몬이 실행 중인지 확인하여 동작 가능 상태를 검증

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
- 정상 실행 시 메시지가 출력되어 컨테이너 생성 및 실행 검증


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

<img width="621" height="275" alt="Image" src="https://github.com/user-attachments/assets/ef11067e-49ea-4ca8-90b5-2fbb71e15330" />

