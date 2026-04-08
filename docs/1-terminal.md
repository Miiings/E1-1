# 터미널 조작 로그

## 1. 현재 위치 및 디렉토리 확인
```bash
pwd
ls -la
```

---

## 2. 디렉토리 생성 및 이동

```bash
mkdir mskim
cd mskim
```

---

<img width="522" height="114" alt="Image" src="https://github.com/user-attachments/assets/d3b5ae76-f8cf-424a-ad53-1b59f1816390" />

## 3. 파일 생성 및 조작

```bash
touch test.txt
cp test.txt copy.txt
mv copy.txt moved.txt
rm moved.txt
touch a.txt
touch b.txt
cp a.txt ./b.txt
cp a.txt ../../Desktop
```

---

<img width="379" height="128" alt="Image" src="https://github.com/user-attachments/assets/1db62465-f6e6-406e-9903-9ec9b05b3eca" />

## 4. 파일 내용 확인

```bash
cat test.txt
```

---


## 5. 권한 확인 및 변경

```bash
ls -l
chmod 755 test.txt
chmod 644 test.txt
```

