# Git / GitHub 연동

## 개념 이해

### Git vs GitHub

**Git**: 로컬 버전 관리 도구
- 코드의 변경 이력을 기록
- 버전 관리, 브랜치 관리 등 로컬 작업 수행
- 설치 필요: `git --version`으로 확인

**GitHub**: 원격 저장소 및 협업 플랫폼
- Git으로 관리된 코드를 클라우드에 저장
- 팀 협업, 코드 리뷰, 이슈 추적 등 중앙 집중식 관리
- 웹 기반 인터페이스 제공

### 기본 흐름

```
호스트 작업 공간
    ↓
git add       (스테이징 영역에 파일 추가)
    ↓
git commit    (로컬 저장소에 커밋)
    ↓
git push      (원격 저장소(GitHub)에 업로드)
```

---

## 1. Git 설정

```bash
git config --global user.name "your-name"
git config --global user.email "your-email"
git config --list
```

**설명:**
- `--global`: 시스템 전체에 적용 (모든 저장소)
- `user.name`, `user.email`: 커밋 작성자 정보 - Git 설정 및 GitHub 연동을 확인
- `git config --list`: 현재 설정 확인

**출력 결과:**
```
user.email=your-email@example.com
user.name=your-name
core.repositoryformatversion=0
core.filemode=true
...
```

---

## 2. 저장소 초기화 및 연결

```bash
git init
git remote add origin <repository-url>
```

**명령어 설명:**
- `git init`: 현재 디렉토리를 Git 저장소로 초기화 (`.git` 폴더 생성)
- `git remote add origin <url>`: 원격 저장소 연결 - GitHub 연동을 확인
  - `origin`: 원격 저장소의 기본 이름
  - `<repository-url>`: GitHub 저장소 URL (예: `https://github.com/username/repo.git`)

**확인:**
```bash
git remote -v
```

**출력:**
```
origin    https://github.com/username/repo.git (fetch)
origin    https://github.com/username/repo.git (push)
```

---

## 3. 커밋 및 푸시

```bash
git add .                    # 모든 변경 사항 스테이징
git commit -m "init"         # 로컬에 커밋
git push origin main         # 원격: main 브랜치로 푸시
```

**각 단계 설명:**

### 3.1 git add
```bash
git add .                 # 모든 변경 파일 스테이징
git add <filename>        # 특정 파일만 스테이징
```
- 변경 사항을 스테이징 영역에 추가
- `git status`로 스테이징 상태 확인 가능

### 3.2 git commit
```bash
git commit -m "commit message"
```
- 스테이징된 변경 사항을 로컬 저장소에 저장
- 메시지는 명확하고 간결하게 작성

### 3.3 git push
```bash
git push origin main
```
- 로컬 커밋을 원격 저장소에 업로드
- `origin`: 원격 저장소 이름
- `main`: 브랜치 이름

**출력 결과:**
```
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 245 bytes, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/username/repo.git
 * [new branch]      main -> main
```

---

## 4. 확인

```bash
git remote -v
```

**원격 저장소 확인:**
```
origin    https://github.com/username/repo.git (fetch)
origin    https://github.com/username/repo.git (push)
```

```bash
git log --oneline
```

**커밋 이력 확인:**
```
abc1234 init
def5678 docs: add tutorial
ghi9012 fix: bug in parser
```
