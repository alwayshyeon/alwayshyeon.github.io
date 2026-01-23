---
title: "[Wargame] Bandit Level 5 -> Level 6"
date: 2025-11-15T21:30:00+09:00
draft: false
weight: 1

tags: ["Security", "Bandit", "Linux"]
categories: ["Wargame"]

author: "AlwaysHyeon"

summary: "OverTheWire Bandit Level 5 풀이"

showToc: true
TocOpen: true
---

## 문제
- inhere에 비밀번호가 있습니다.
- 파일 속성: 사람이 읽을 수 있는 형식, 1033 바이트의 크기, 실행 불가능

## 풀이
```bash
bandit5@bandit:~$ ls -l
total 4
drwxr-x--- 22 root bandit5 4096 Oct 14 09:26 inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls -l
total 80
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere00
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere01
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere02
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere03
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere04
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere05
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere06
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere07
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere08
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere09
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere10
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere11
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere12
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere13
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere14
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere15
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere16
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere17
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere18
drwxr-x--- 2 root bandit5 4096 Oct 14 09:26 maybehere19
bandit5@bandit:~/inhere$ find . -size 1033b
bandit5@bandit:~/inhere$ find . -size 1033B
find: invalid -size type `B`
bandit5@bandit:~/inhere$ find . -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
PASSWORD
```

## Troubleshooting
- 폴더도 너무 많고 폴더 안에 파일도 많을 것 같아서 문제에서 파일 크기가 1033 바이트라고 해서 그 부분에 집중 하기로 했습니다.
- `find . -size 1033b` 명령어를 입력했는데 아무 결과 없이 그냥 끝났습니다.
- 구글링 결과 단위 b의 의미가 다르다는 것을 알게 되었습니다. 리눅스 `find` 명령어에서 소문자 `b`는 바이트(Byte)가 아니라 **블록(Block, 512 Bytes)**을 의미합니다. 
    - 컴퓨터는 1033b를 1033 * 512 bytes로 계산합니다.
- `find . -size 1033B` 명령어를 입력했을 때는 B는 유효한 단위가 아니라서 오류가 났습니다.
- `find . -size 1033c`를 구글링을 통해 알게 되었고, 비밀번호를 찾을 수 있었습니다.
- find 명령어의 크기 단위 정리
| 접미사 | 의미 | 설명 (기억법) |
| :---: | :--- | :--- |
| `c` | Bytes | Characters (문자 1개 = 1바이트) |
| `b` | 512-byte blocks | Blocks (기본값, 단위를 안 쓰면 이걸로 인식됨) |
| `k` | Kilobytes | Kilo (1024 bytes) |
| `M` | Megabytes | Mega (1024 kilobytes) |
| `G` | Gigabytes | Giga (1024 megabytes) |

```bash
exit
```