# Git / GitHub 연동

## 1. Git 설정
```bash
git config --global user.name "your-name"
git config --global user.email "your-email"
git config --list
```

---

## 2. 저장소 초기화 및 연결

```bash
git init
git remote add origin <repository-url>
```

---

## 3. 커밋 및 푸시

```bash
git add .
git commit -m "init"
git push origin main
```

---

## 4. 확인

```bash
git remote -v
git log --oneline
```

(스크린샷 첨부)