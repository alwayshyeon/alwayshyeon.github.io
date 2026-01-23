---
title: "[Wargame] Bandit Level 4 -> Level 5"
date: 2025-11-15T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Security", "Bandit", "Linux"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 4 풀이"

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: true
---

## 문제
- inhere에 유일하게 사람이 읽을 수 있는 파일에 비밀번호가 숨겨져 있습니다.

## 풀이
```bash
bandit4@bandit:~$ ls -al
total 24
drwxr-xr-x   3 root root 4096 Oct 14 09:26 .
drwxr-xr-x 150 root root 4096 Oct 14 09:29 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Oct 14 09:19 .bashrc
drwxr-xr-x   2 root root 4096 Oct 14 09:26 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls -al
total 48
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file00
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file01
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file02
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file03
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file04
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file05
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file06
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file07
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file08
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file09
bandit4@bandit:~/inhere$ cat -file00
cat: invalid option -- 'f'
Try 'cat --help' for more information.
bandit4@bandit:~/inhere$ cat < -file00
�=
I�� ��V`n�5���ѳ��*�G^7cO�bandit4@bandit:~/inhere$ file < -file0*
-bash: -file0*: ambiguous redirect
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: OpenPGP Public Key
./-file02: OpenPGP Public Key
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat < -file07
PASSWORD
```
### Troubleshooting
- -file00의 파일을 읽고 알 수 없는 문자가 나왔을 때 유일하게 사람이 읽을 수 있는 파일이 있다라는 힌트를 떠올려서 `file`을 통해 파일 형식을 알아보려고 했다. `cat <` 형식은 오직 하나의 입력 소스만 받을 수 있다라는 것을 알게 되었습니다.
- `.`을 통해 `-`가 옵션이 아니라 파일 경로라는 것을 인식 시켜서 파일의 형식을 알 수 있었습니다.

```bash
exit
```