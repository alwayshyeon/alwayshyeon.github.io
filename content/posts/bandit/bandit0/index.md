---
title: "[Wargame] Bandit Level 0 -> Level 1"
date: 2025-11-01T21:30:00+09:00
draft: false
weight: 1
aliases: ["/study"]

tags: ["Security", "Bandit", "Linux", "SSH"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 0 풀이 및 SSH 접속 에러 해결"

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: true
---
# Bandit 시작
```bash
ssh -p 2220 bandit[level]@bandit.labs.overthewire.org 

# ssh: 원격 호스트에 접속하기 위한 프로토콜
# -p 2220: SSH의 기본 포트는 22번이지만, Bandit 연구소는 2220번 포트를 사용하므로 -p 옵션으로 포트를 지정해야 합니다.
```
로 시작할 수 있습니다.

## Troubleshooting

실습 도중 아래와 같은 DNS 에러가 발생하여 접속이 불가능했습니다.

```bash
ssh: Could not resolve hostname bandit.labs.overthewire.org: Temporary failure in name resolution
```

- 가상머신(Kali Linux)의 네트워크 설정 문제였습니다. /etc/resolv.conf에 구글 DNS(8.8.8.8)를 추가하여 해결했습니다.

{{< figure src="bandit0.png" caption="주소를 입력했을 때" width="80%" align="center" >}}

![비밀번호를 입력했을 때](login.png)

## 문제
- readme 파일에서 비밀번호 찾기

```bash
bandit0@bandit:~$ ls    # ls (List): 현재 디렉토리의 파일과 폴더 목록을 보여줍니다.
readme
bandit0@bandit:~$ cat readme    # cat (Concatenate): 파일의 내용을 터미널에 출력합니다.
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: PASSWORD
```

```bash
exit
```