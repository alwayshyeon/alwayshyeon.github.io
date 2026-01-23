---
title: "[Wargame] Bandit Level 2 -> Level 3"
date: 2025-11-08T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Security", "Bandit", "Linux"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 2 풀이"

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: true
---

## 문제
- --spaces in this filename--가 이름인 파일에 비밀번호가 있습니다.

## 풀이
```bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ cat < --spaces in this filename--
-bash: --spaces: No such file or directory
```

- 원인: 터미널은 공백이 있으면 각각의 파일로 생각하기 때문입니다.
- 해결: 따옴표나 이스케이프 문자(\) + space를 이용하면 됩니다.

```bash
bandit2@bandit:~$ cat < --spaces\ in\ this\ filename--
PASSWORD
bandit2@bandit:~$ cat < '--spaces in this filename--'
PASSWORD
```

```bash
exit
```