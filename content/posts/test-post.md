---
title: "블로그 테스트 및 첫 번째 글 (Hello World)"
date: 2026-01-08T20:45:00+09:00
draft: false
weight: 1
aliases: ["/test"]

tags: ["Test", "Free Talk", "Hugo"]
categories: ["Log"]

author: "AlwaysHyeon"

summary: "Hugo PaperMod 테마 적용 테스트 글입니다. 마크다운 문법과 코드 하이라이팅이 잘 적용되는지 확인합니다."

showToc: true
TocOpen: true

cover:
    image: ""
    alt: "Test Image"
    caption: "Test Caption"
    relative: false
---

## 1. 개요 (Intro)

안녕하세요, **AlwaysHyeon**의 보안 블로그입니다.
이 글은 GitHub Pages와 Hugo PaperMod 테마가 정상적으로 연동되었는지 확인하기 위한 테스트 포스트입니다.

### 테스트 환경
- **Generator:** Hugo
- **Theme:** PaperMod
- **Hosting:** GitHub Pages

---

## 2. 기능 테스트 (Feature Test)

### 2.1. 코드 하이라이팅 (Code Block)
Python 코드가 예쁘게 나오는지 확인합니다.

```python
import os

def check_security():
    print("System Secure... maybe?")
    return True

if __name__ == "__main__":
    check_security()