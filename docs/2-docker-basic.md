# Docker 기본 실습

## 1. Docker 설치 확인
```bash
docker --version
docker info
```
<img width="346" height="32" alt="Image" src="https://github.com/user-attachments/assets/547526bd-7c55-47a9-9f30-992a42e48fc2" />
<img width="581" height="662" alt="Image" src="https://github.com/user-attachments/assets/7612cce5-dd7d-4111-96c1-e77e641515bc" />
---

## 2. hello-world 실행

```bash
docker run hello-world
```

<img width="610" height="388" alt="Image" src="https://github.com/user-attachments/assets/f4e17e2a-4f12-439a-a346-a48be090412a" />

---

## 3. Ubuntu 컨테이너 실행 및 진입

```bash
docker run -it ubuntu bash
```

컨테이너 내부에서 실행:

```bash
ls
echo "abc"
```

<img width="621" height="275" alt="Image" src="https://github.com/user-attachments/assets/ef11067e-49ea-4ca8-90b5-2fbb71e15330" />
