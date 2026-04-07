# Docker 기본 실습

## 1. Docker 설치 확인
```bash
docker --version
docker info
```

(스크린샷 첨부)

---

## 2. hello-world 실행

```bash
docker run hello-world
```

(스크린샷 첨부)

---

## 3. Ubuntu 컨테이너 실행 및 진입

```bash
docker run -it ubuntu bash
```

컨테이너 내부에서 실행:

```bash
ls
echo "test"
```

(스크린샷 첨부)