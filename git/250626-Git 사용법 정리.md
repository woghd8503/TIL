# Git 사용법 정리

> AI Kernel Academy Bootcamp
---

## 📌 표지:Git Logo

![Git Logo](https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png)

---

## 📚 보조 아이템

* **Shell & Vim 명령어 기초**
* **Git 기본 사용법**: clone, add, commit, push
* **Pre-commit Hook 활용**
* **Git 고급 기능**: branch, merge, rebase, conflict 해결
* **Branch 전략**: Git Flow, GitHub Flow, GitLab Flow
* **GitHub 협업**: Issues, Projects, Pull Requests, Wiki

---

## 🎯 발췌 목표

1. Git 기능을 이해하고 충분히 사용할 수 있다.
2. Remote & Local Repository 구조를 파악한다.
3. 협업 중 발생하는 충돌(conflict)을 해결할 수 있다.
4. Pre-commit Hook을 통해 코드 품질을 사전에 보장할 수 있다.
5. 다양한 브랜치 전략을 프로젝트에 맞게 선택할 수 있다.

---

## 🧠 Git 기본 개념 (업데이트)

* **Git**은 **Linus Torvalds**가 **Linux 커널 버전 관리를 위한 상용 툴의 속도와 라이센스에 불만을 품고 2005년 4월**, 분노 속에서 단 **일주일 만에 개발**한 고성능 분산 버전 관리 시스템입니다.
* Git은 빠르고, 효율적이며, 오픈소스 생태계에서 가장 널리 사용되는 VCS입니다.

---

## 📂 Git 작업 공간 구조

```txt
Working Directory → Staging Area → Local Repository → Remote Repository
```

```bash
$ git add 파일명      # 작업 파일을 스테이징 영역에 추가
$ git commit -m "메시지"   # 커밋으로 저장소에 기록
$ git push origin main  # 원격 저장소로 전송
```

![Git 구조도](https://i.namu.wiki/i/OHK0kICoGdyuxcBRvS24kQyIzfLv2AycocM6N95QsBMm_5WU2yzJgeR0y7J_cUhzUBCjLJfTmRmuFwZSQHTJGQ.webp)

---

## 📁 .gitignore 생성 & 사용하는 이유

### ✅ `.gitignore`란?

- Git이 **버전 관리하지 않을 파일** 또는 디렉토리를 지정하는 설정 파일입니다.
- 예: 로그 파일, 빌드 산출물, 캐시, 환경 설정 파일 등은 추적하지 않는 것이 좋습니다.

---

### 🧠 사용하는 이유

1. **불필요한 파일 커밋 방지**  
   → IDE 설정, 바이너리 파일 등  
2. **보안 유지**  
   → `.env`, 인증키, 개인 설정  
3. **협업 효율성 증가**  
   → 팀원이 공통적으로 무시해야 할 파일 공유

---

### 🛠️ 기본 예시

```plaintext
# Python 관련 무시 파일
__pycache__/
*.py[cod]
*.egg-info/

# 환경 설정
.env

# macOS
.DS_Store

# VSCode
.vscode/
```
### 🌐 자동 생성 사이트
- https://www.toptal.com/developers/gitignore
- https://gitignore.io
```
🔍 언어(ex: python, node, macos, vscode)를 입력하면 자동 생성해 줍니다!
```
---
## ✅ Conventional Commits

* `feat`: 기능 추가
* `fix`: 버그 수정
* `docs`: 문서 작업
* `style`: 포매팅 (코드 변경 없음)
* `refactor`: 리팩토링
* `test`: 테스트 코드 추가

예시:

```bash
$ git commit -m "feat: 사용자 로그인 기능 추가"
```

---

## 🌱 Branch & Merge

### 브랜치 생성 및 전환

```bash
$ git branch feature/login
$ git switch feature/login
```

### 브랜치 병합

```bash
$ git switch main
$ git merge feature/login
```

### 브랜치 삭제

```bash
$ git branch -d feature/login
```

---

## 🔁 Rebase 사용법

`merge` 대신 `rebase`를 사용하면 커밋 히스토리가 더 깔끔하게 유지됩니다.

```bash
$ git switch feature/login
$ git rebase main
```

### 충돌 발생 시 해결 절차

```bash
$ git status                # 충돌 확인
$ vi 파일명                 # 충돌 해결
$ git add 파일명
$ git rebase --continue     # 계속 진행
# 또는
$ git rebase --abort        # 취소
```

![Rebase 이미지](https://lh3.googleusercontent.com/YEKEfhsdA9VCR44ZjX5oBFs4U9VBdkChSx1wqOeqqesnL9wSw7Hm5AiZsHMXyEq3OqpO9pK3k1RAeWKRIoFiaZIYUIAN6kDmiR_oNDq2PisKvrhryK4dHLHgWT1m0fYcFl25olG1K_1QDsLZxj0j9WA)

---

## 🛠️ Conflict 해결 예시

```bash
$ git merge main
# <<<<<<<, =======, >>>>>>> 표기 제거
$ git add .
$ git commit
```

팁:

* `git diff`, `git log`, `git mergetool` 사용 권장
* 코드 리뷰 후 직접 수동 해결하는 것이 가장 안전함

---

## ✅ Pre-commit Hook

### pre-commit 설치 및 설정

```bash
$ pip install pre-commit
$ pre-commit --version
$ touch .pre-commit-config.yaml
```

### 예시 설정파일 (YAML)

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.4.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-added-large-files
```

### 적용

```bash
$ pre-commit install
$ pre-commit run --all-files
```

> commit 전 코드 스타일, 문법, 보안 문제 등을 자동 점검하여 품질 유지

![Pre-commit 로고](https://azure.github.io/AKS-DevSecOps-Workshop/assets/images/module2/pre-commit-hook-flow.png)

---

## 🔗 GitHub 협업 (요약)

* **Issues**: 작업 할당, 버그 추적
* **Projects**: 칸반 보드로 작업 흐름 추적
* **Pull Requests**: 코드 리뷰 요청, 병합 승인
* **Wiki**: 프로젝트 문서화

---

## 📌 마무리 Tip

* 실수 방지용 alias 설정 추천

```bash
$ git config --global alias.st status
$ git config --global alias.co checkout
$ git config --global alias.br branch
```

* 커밋 메시지는 작업 단위를 명확히 보여줘야 함
* conflict는 두려워하지 말고 적극적으로 해결할 것!

---

## 📖 참고 자료

* [Git 공식 문서](https://git-scm.com/book/ko/v2)
* [Pre-commit 공식](https://pre-commit.com/)
* [GitHub Docs](https://docs.github.com/)
* [Git Flow 전략](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)

---

## 🎬 마무리 명언

> "Git은 가장 간단하지만, 가장 강력한 도구이며, 개발자의 궁극기이다."

---
