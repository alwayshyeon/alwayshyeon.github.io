---
title: "[Wargame] Bandit Level 3 -> Level 4"
date: 2025-11-08T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Security", "Bandit", "Linux"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 3 풀이"

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: true
---

## 문제
- inhere에서 숨겨진 파일 안에 비밀번호가 있습니다.

## 풀이
```bash
bandit3@bandit:~$ ls -al
total 24
drwxr-xr-x   3 root root 4096 Oct 14 09:26 .
drwxr-xr-x 150 root root 4096 Oct 14 09:29 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Oct 14 09:19 .bashrc
drwxr-xr-x   2 root root 4096 Oct 14 09:26 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat Hiding-From-You
cat: Hiding-From-You: No such file or directory
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
PASSWORD
```

## Troubleshooting
- ., .., ...이 순서 인 줄 알았다.