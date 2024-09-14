---
description: Git 서브모듈 삭제를 정리한 내용입니다.
---

# Git 서브모듈 삭제

## 1. 서브모듈 제거

```bash
$ git submodule deinit -f <submodule_path>
$ git rm -f <submodule_path>
```

* `<submodule_path>` 는 제거하려는 서브모듈의 경로이다.
* deinit 후 프로젝트 상에서 모듈을 제거한다.

## 2. 서브모듈 설정 삭제

```bash
$ rm -rf .git/modules/<submodule_path>
```

* 서브모듈의 설정을 저장하는 폴더를 삭제한다.

## 3. 로컬 파일 삭제

```bash
$ rm -rf <submodule_path>
```

* 프로젝트에서 더 이상 서브모듈이 필요없다면 관련 로컬 파일을 삭제한다.

## 4. 커밋 후 업데이트

```bash
$ git commit -m "Remove submodule <submodule_path>"
$ git push origin <branch_name>
```

* 서브모듈이 삭제된 상태를 커밋하고 관련 브렌치를 push 하며 업데이트 한다.
