---
title: "[Wargame] Bandit Level 1 -> Level 2"
date: 2025-11-01T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Security", "Bandit", "Linux", "SSH"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 1 풀이"

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: true
---

## 문제
- -가 파일인 곳에 비밀번호가 있습니다.

## 풀이
```bash
bandit1@bandit:~$ ls
-
```

```bash
bandit1@bandit:~$ cat -
^C
bandit1@bandit:~$ cd -
-bash: cd: OLDPWD not set
```
- 평소와 같이 하려고 했지만 되지 않았습니다.
- 보통 dash(-)는 명령어의 옵션과 arguments로 사용되기 때문에 "-" 파일을 열기위해서는 더 많은 주의가 필요합니다.

---

### Create

- 파일을 생성하기 위해서는 특별한 argument로 -- 를 앞에 붙여줘야 한다. 
```bash
touch -- -filename
```

### Read & Copy
```bash
touch -- -filename
```

### filename 안에 내용넣기 
```bash
echo "Hello bandit!" > -filename
```

### 파일 내용 읽기 
```bash
cat < -filename
```

### 파일 내용 복사하기
```bash
cp -- -filename /opt
```

### List

- 파일 찾기
```bash
ls -l -- -filename
```

### Remove 
```bash
rm -rf -- -filename
```

---


```bash
bandit1@bandit:~$ cat < -
PASSWORD
```

```bash
exit
```