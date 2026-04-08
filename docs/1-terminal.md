# 터미널 조작 로그

## 터미널(Shell)이란?

터미널은 사용자가 명령어를 입력하여 컴퓨터 시스템과 직접 상호작용하는 **텍스트 기반 인터페이스**입니다.

- **GUI**: 마우스로 클릭 (Finder, Explorer 등)
- **CLI**: 명령어로 제어 (터미널)

### 기본 명령어

| 명령어 | 설명 |
|--------|------|
| `pwd` | 현재 디렉토리 경로 표시 |
| `ls` | 파일/폴더 목록 표시 |
| `mkdir` | 디렉토리 생성 |
| `cd` | 디렉토리 이동 |
| `touch` | 빈 파일 생성 |
| `cp` | 파일 복사 |
| `mv` | 파일 이동/이름 변경 |
| `rm` | 파일 삭제 |
| `cat` | 파일 내용 출력 |
| `chmod` | 파일 권한 변경 |

---

## 1. 현재 위치 및 디렉토리 확인

```bash
pwd          # Print Working Directory
ls -la       # 상세 목록 (숨김 파일 포함)
```

**설명:**
- `pwd`: 현재 작업 중인 디렉토리의 절대 경로를 표시
- `ls`: 현재 디렉토리의 파일/폴더 목록 표시
- `-l`: 상세 정보 (권한, 소유자, 크기, 수정 날짜)
- `-a`: 모든 파일 표시 (숨김 파일 `.`로 시작하는 파일)

**출력 결과:**
```
/Users/username/Desktop

drwxr-xr-x  5 username  staff  160  Apr  8 10:30 .
drwxr-xr-x  8 username  staff  256  Apr  7 15:45 ..
-rw-r--r--  1 username  staff  245  Apr  8 10:20 test.txt
drwxr-xr-x  3 username  staff   96  Apr  8 09:15 project
```

---

## 2. 디렉토리 생성 및 이동

```bash
mkdir mskim          # 디렉토리 생성
cd mskim             # 디렉토리로 이동
pwd                  # 현재 위치 확인
```

**설명:**
- `mkdir`: 새 디렉토리 생성
- `cd`: 디렉토리 변경 (Change Directory)
- `.`: 현재 디렉토리
- `..`: 상위 디렉토리
- `cd ~`: 홈 디렉토리로 이동

**출력 결과:**
```
/Users/username/Desktop/mskim
```

**스크린샷:**
<img width="522" height="114" alt="Image" src="https://github.com/user-attachments/assets/d3b5ae76-f8cf-424a-ad53-1b59f1816390" />

---

## 3. 파일 생성 및 조작

```bash
touch a.txt          # 파일 생성
touch b.txt
mv a.txt moved.txt   # 파일 이름 변경
cp moved.txt copy.txt # 파일 복사
rm copy.txt          # 파일 삭제
cp moved.txt ../../Desktop  # Desktop으로 복사
```

**각 명령어 설명:**

### 파일 생성
- `touch filename`: 빈 파일 생성 또는 수정 시간 변경

### 파일 이름 변경
- `mv oldname newname`: 파일 또는 폴더 이동/이름 변경

### 파일 복사
- `cp source destination`: 원본 → 대상으로 복사
- `cp file /path/`: 특정 디렉토리로 복사

### 파일 삭제
- `rm filename`: 파일 삭제 (되돌릴 수 없음, 신중히!)
- `rm -r dirname`: 디렉토리와 내용 전체 삭제

**출력 결과:**
```
$ ls -la
total 24
drwxr-xr-x  3 username  staff    96  Apr  8 10:45 .
drwxr-xr-x  8 username  staff   256  Apr  8 10:30 ..
-rw-r--r--  1 username  staff     0  Apr  8 10:45 b.txt
-rw-r--r--  1 username  staff     0  Apr  8 10:44 moved.txt
```

**스크린샷:**
<img width="379" height="128" alt="Image" src="https://github.com/user-attachments/assets/1db62465-f6e6-406e-9903-9ec9b05b3eca" />

---

## 4. 파일 내용 확인

```bash
cat test.txt         # 파일 내용 전체 출력
head -n 5 file.txt   # 처음 5줄만 출력
tail -n 5 file.txt   # 마지막 5줄만 출력
```

**설명:**
- `cat`: 파일 내용을 화면에 출력
- `head`: 파일의 처음 부분 출력
- `tail`: 파일의 마지막 부분 출력

**출력 결과:**
```
This is a test file.
It contains multiple lines.
For demonstration purposes.
```

---

## 5. 권한 확인 및 변경

```bash
ls -l               # 파일 권한 확인
chmod 755 test.txt  # 실행 권한 추가
chmod 644 test.txt  # 읽기/쓰기 권한
```

**권한 설명:**

파일 권한은 3자리 숫자로 표현:
- `7`: 소유자 권한 (읽기+쓰기+실행 = 4+2+1)
- `5`: 그룹 권한 (읽기+실행 = 4+1)
- `5`: 다른 사용자 권한 (읽기+실행 = 4+1)

**권한 분류:**
- `4` (r): 읽기 (read)
- `2` (w): 쓰기 (write)
- `1` (x): 실행 (execute)

**출력 결과:**
```
-rw-r--r-- 1 username staff 245 Apr 8 10:20 test.txt
```

좌측부터:
- `-`: 파일 타입 (폴더는 `d`)
- `rw-`: 소유자 권한 (읽기, 쓰기)
- `r--`: 그룹 권한 (읽기만)
- `r--`: 다른 사용자 권한 (읽기만)

**스크린샷:**
<img width="478" height="195" alt="Image" src="https://github.com/user-attachments/assets/58de4522-d1be-4c01-856a-06719e07bea3" />
<img width="422" height="446" alt="Image" src="https://github.com/user-attachments/assets/29aef69a-e10a-422a-9c20-64f91873a5e3" />

---

## 팁 및 주의사항

📌 **상대 경로 vs 절대 경로**
- 절대 경로: `/Users/username/Desktop` (루트에서 시작)
- 상대 경로: `./Desktop` 또는 `../Desktop` (현재 위치 기준)

📌 **자동 완성**
- 파일/폴더명 입력 후 `Tab` 키 누르면 자동 완성

📌 **이전 명령어 재사용**
- 화살표 키 ↑/↓로 이전 명령어 열람
- `history`: 명령어 이력 확인

⚠️ **위험한 명령어**
- `rm -rf /`: 시스템 전체 삭제 (절대 금지!)
- `rm`: 휴지통으로 가지 않고 완전 삭제

📌 **도움말 확인**
```bash
man ls              # 명령어 설명서 보기
ls --help           # 간단한 도움말
```
