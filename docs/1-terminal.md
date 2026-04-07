# 터미널 조작 로그

## 1. 현재 위치 및 디렉토리 확인
```bash
pwd
ls -la
```

(스크린샷 첨부)

---

## 2. 디렉토리 생성 및 이동

```bash
mkdir test-dir
cd test-dir
```

(스크린샷 첨부)

---

## 3. 파일 생성 및 조작

```bash
touch test.txt
cp test.txt copy.txt
mv copy.txt moved.txt
rm moved.txt
```

(스크린샷 첨부)

---

## 4. 파일 내용 확인

```bash
cat test.txt
```

(스크린샷 첨부)

---

## 5. 권한 확인 및 변경

```bash
ls -l
chmod 755 test.txt
chmod 644 test.txt
```

(변경 전/후 스크린샷 첨부)