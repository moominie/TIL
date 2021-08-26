# GitHub_Basic

✏️📖 Git과 GitHub의 기초를 배워요



## 버전 관리 시스템(Version Control System, VCS)

파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템

소스코드뿐만 아니라 실제로 거의 모든 컴퓨터 파일의 버전을 관리할 수 있음



#### 버전 관리 시스템의 장점

- 소스코드 백업이 편리함
- 빌드 후 오류 발생 시 빌드 이전의 소스코드로의 복구가 편함
- 여러 작업자 또는 다른 장소에서의 소스코드 동기화가 편리함
- 동시에 여러 프로젝트가 진행될 때 동일 소스코드에 대한 병합이 편리함
- 소스코드의 변경시점 및 변경자 확인이 편리함



### 분산 버전 관리 시스템(Distributed Version Control System, DVCS)

클라이언트는 단순히 서버 파일의 마지막 스냅샷만 저장하는 게 아니라 서버의 저장소를 히스토리와 더불어 전부 복제함

만약 서버에 문제가 생기면 이 복제물로 다시 작업을 시작할 수 있음

클라이언트 중에서 아무거나 골라도 서버를 복원할 수 있음

Clone은 모든 데이터를 가진 진정한 백업임



![분산 버전 관리 시스템(DVCS)](https://git-scm.com/book/en/v2/images/distributed.png)

- 대부분의 DVCS 환경에서는 리모트 저장소가 존재함

사람들은 동시에 다양한 그룹과 다양한 방법으로 협업할 수 있음

계층 모델 같은 중앙집중식 시스템으로는 할 수 없는 워크플로를 다양하게 사용할 수 있음



## Git 기초

##### #Repository란?

Git 프로젝트 저장소

- local repository : 내 컴퓨터의 프로젝트 저장소
- remote repository : 외부(서버)의 프로젝트 저장소



#### Git 특징

###### 1. 차이가 아니라 스냅샷

Git은 데이터를 스냅샷의 스트림처럼 취급함

![시간순으로 프로젝트의 스냅샷을 저장](https://git-scm.com/book/en/v2/images/snapshots.png)

###### 2. 거의 모든 명령을 로컬에서 실행

거의 모든 명령이 로컬 파일과 데이터만 사용하기 때문에 네트워크에 있는 다른 컴퓨터는 필요 없음

프로젝트의 모든 히스토리가 로컬 디스크에 있기 때문에 모든 명령이 순식간에 실행됨

오프라인 상태이거나 VPN에 연결하지 못해도 막힘없이 일할 수 있음

###### 3. Git의 무결성

Git은 데이터를 저장하기 전에 항상 체크섬을 구하고 그 체크섬으로 데이터를 관리하기 때문에 체크섬을 이해하는 Git없이는 어떠한 파일이나 디렉토리도 변경할 수 없음

###### 4. Git은 데이터를 추가할 뿐

Git으로 무얼하든 Git 데이터베이스에 데이터가 추가됨

일단 스냅샷을 커밋하고 나면 데이터를 잃어버리기 어려움

###### **5. 세가지 상태**

Git은 파일을 세가지 상태로 관리함

- Modified : 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않은 것
- Staged : 현재 수정한 파일을 곧 커밋할 것이라고 표시한 상태
- Committed : 데이터가 로컬 데이터베이스에 안전하게 저장됐다는 것을 의미

###### Git 프로젝트의 세가지 단계

![워킹 트리, Staging Area, Git 디렉토리](https://git-scm.com/book/en/v2/images/areas.png)

- Git 디렉토리 : Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳, **Git의 핵심**
- 워킹 트리 : 프로젝트의 특정 버전을 `Checkout`한 것
- Staging Area : Git 디렉토리에 있는 단순한 파일로, 곧 커밋할 파일에 대한 정보를 저장함

###### Git으로 하는 일

1. 워킹 트리에서 파일을 수정한다.
2. Staging Area에 파일을 `Stage`해서 커밋할 스냅샷을 만든다. 모든 파일을 추가할 수도 있고 선택하여 추가할 수도 있다.
3. Staging Area에 있는 파일들을 `Commit`해서 Git 디렉토리에 영구적인 스냅샷으로 저장한다.



### Git 시작하기 (Mac 기준)

---

#### Git 설치

Terminal에서 Git 설치 여부 확인

`$ git --version`

만약 'git'이 설치돼 있지 않으면 설치하라는 안내가 나옴

- Git 다운로드 사이트

http://git-scm.com/download/mac

다양한 Git 설치 방법이 나와있음



**Homebrew를 이용한 Git 설치**

1. Homebrew가 없다면 Homebrew부터 설치

`$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

2. Homebrew로 Git 설치

`$ brew install git`



#### Git 최초 설정

환경 설정은 한 컴퓨터에서 한 번만 하면 됨

##### 사용자 정보

사용자이름, 이메일 주소 설정

한 번 `커밋`한 후에는 정보를 변경할 수 없음

`$ git config --global user.name "사용자 이름"`

`$ git config --global user.email "이메일 주소"`

##### 설정 확인

`$ git config --list`

설정한 모든 것 확인 가능



### Git 저장소 만들기

---

##### WARNING

1. Home폴더(~)를 리포로 업그레이드하지 않는다.
2. 리포 안의 폴더에서 git init하지 않는다. (리포 안에 리포를 두지 않는다.)



##### Git 저장소 만드는 2가지 방법

1. 아직 버전관리를 하지 않은 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법
2. 다른 어딘가에서 Git 저장소를 `Clone` 하는 방법



#### 기존 디렉토리를 Git 저장소로 만들기

버전관리를 하지 아니하는 기존 프로젝트를 Git으로 관리하고 싶은 경우

1. 프로젝트의 디렉토리로 이동

`$ cd /Users/<userName>/<directoryName>`

2. 저장소 초기화하기 (.git이라는 하위 디렉토리 만들기)

`$ git init`

###### +) 저장소를 일반 디렉토리로 되돌리려면?

`rm -rf .git`



#### 기존 저장소를 Clone하기

다른 프로젝트에 참여(Contribute)하거나 Git 저장소를 복사하고 싶을 때

`$ git clone <url>`

###### 예시

`$ git clone https://github.com/libgit2/libgit2`

libgit2라는 디렉토리를 만들고 그 안에 .git 디렉토리를 만들어서 저장소의 데이터를 모두 가져와서 자동으로 가장 최신 버전을 `Checkout` 해놓음

`$ git clone https://github.com/libgit2/libgit2 mylibgit`

디렉토리 이름을 libgit2가 아닌 mylibgit으로 `Clone`함



### 수정하고 저장소에 저장하기

---

##### 워킹 디렉토리의 파일 분류

- Untracked (관리대상이 아님)
- Tracked (관리대상임) : 이미 스냅샷에 포함돼있던 파일
  - Unmodified (수정하지 않음)
  - Modified (수정함)
  - Staged (커밋으로 저장소에 기록할 상태)



처음 저장소를 `Clone`하면 모든 파일은 Tracked이면서 Unmodified 상태임 (파일을 Checkout하고나서 아무것도 수정하지 않았기 때문)

어떤 파일을 수정하면 Git은 그 파일을 `Modified`상태로 인식함

이 수정한 파일을 `Staged`상태로 만들고, Staged 상태의 파일을 `Commit`함



![파일의 라이프사이클](https://git-scm.com/book/en/v2/images/lifecycle.png)



#### 파일 무시하기

로그 파일이나 빌드 시스템이 자동으로 생성한 파일 등 Git이 관리할 필요가 없는 파일들을 무시하기

`.gitignore` 파일을 만들고 그 안에 무시할 파일 패턴을 적음

 처음에 `.gitignore` 파일을 만들어두면 Git 저장소에 커밋하고 싶지 않은 파일을 실수로 커밋하는 것을 방지할 수 있음



##### `.gitignore` 파일에 입력하는 패턴 규칙

- 아무것도 없는 라인이나 '#'으로 시작하는 라인은 무시
- 표준 Glob 패턴을 사용, 이는 프로젝트 전체에 적용됨
  - 애스터리스크(*) : 문자 0개 이상을 의미
  - 중괄호([abc]) : [ ] 안에 있는 문자 중 하나를 의미 (이 경우에는 a, b, c 중 하나)
  - 물음표(?) : 문자 1개를 의미
  - 중괄호 안의 캐릭터 사이에 하이픈 사용([0-9]) : 그 캐릭터 사이에 있는 문자 하나 의미 (이 경우에는 0부터 9까지 숫자 중 하나)
  - 애스터리스크 2개(**) : 디렉토리 안의 디렉토리 지정
  - 슬래시와 애스터리스크(a/*/z) : a/z. a/b/z, a/b/c/z 디렉토리에 사용 가능
- 슬래시(/)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않음
- 디렉토리는 슬래시(/)를 끝에 사용하는 것으로 표현
- 느낌표(!)로 시작하는 패턴의 파일은 무시하지 않음



##### `.gitignore` 파일의 예

`*.a`

확장자가 .a인 파일 무시

`!lib.a`

윗 라인에서 확장자가 .a인 파일은 무시하게 했지만, lib.a는 무시하지 않음

`/TODO`

현재 디렉토리에 있는 TODO 파일은 무시하고, subdir/TODO처럼 하위디렉토리에 있는 TODO 파일은 무시하지 않음

`build/`

build/ 디렉토리에 있는 모든 파일은 무시

`doc/*.txt`

doc/ 디렉토리에 있는 .txt파일은 무시하고 doc/ 디렉토리의 하위디렉토리에 있는 .txt파일은 무시하지 않음

`doc/**/*.pdf`

doc/ 디렉토리 아래의 모든 .pdf 파일을 무시



##### https://www.gitignore.io/

원하는 ignore 파일을 간단하게 생성할 수 있음



#### 파일을 새로 추적하기

`git add` 명령을 통해 디렉토리에 있는 파일을 추적하고 관리하도록 함

파일을 수정하고나면 꼭 `git add` 명령을 통해서 최신 버전을 `Staged` 상태로 만들어야 함

- 특정 파일만 stage하기

`$ git add <filename>`

- 현재 위치의 모든 파일을 stage하기

`$ git add .`



#### 파일의 상태 확인하기

`$ git status`

- 빨간색으로 표시되는 파일은 `commit`에 포함되지 않음
- 초록색으로 표시되는 파일은 `commit`에 포함됨
- 변경사항이 없는 파일은 표시되지 않음



#### 커밋을 통해 스냅샷 저장하기

`$ git commit -m "MESSAGE"`

커밋하면 `git add`를 실행한 시점의 파일이 커밋되어 저장소 히스토리에 남게 됨

###### +) 커밋 재작성

`$ git commit --amend`

완료한 커밋을 살짝 수정하고 다시 커밋하고 싶을 때 사용

`amend` 명령을 통한 두번째 커밋은 첫번째 커밋을 덮어씀



#### 파일 삭제하기

1. Tracked 상태의 파일을 Staging Area에서 삭제하기 (워킹 디렉토리에 있는 실제 파일도 삭제됨)

`$ git rm <fileName>`

2. 커밋하기

`$ git commit -m "MESSAGE"`



- 수정한 파일 또는 Staging Area에 추가한 파일을 강제 삭제하기

`$ git rm -f <filename>`

- Staging Area에서만 파일을 제거하고 워킹 디렉토리에 있는 파일은 지우지 않고 남겨두기

`$ git rm --cached <filename>`

- 여러개의 파일이나 디렉토리를 한꺼번에 삭제하기

`$ git rm <directoryname>/`

`$ git rm \<*.확장자>`

`$ git rm <directoryname>/\<*.확장자>`

디렉토리에 있는 .확장자 파일을 모두 삭제함



#### 파일 이름 변경하기

`$ git mv <oldName> <newName>`



### 커밋 히스토리 조회하기

---

`$ git log`

Git 저장소의 히스토리 조회하기

`$ git log --oneline`

각 커밋을 한 줄로 보여줌



### 리모트 저장소

---

#### 리모트 저장소 확인하기

`$ git remote`

- 단축이름과 url을 함께 보려면?

`$ git remote -v`



#### 리모트 저장소 추가하기

기존 워킹 디렉토리에 새 리모트 저장소 추가하기

`$ git remote add <단축이름> <url>`

- 리모트에서 최초 Clone 받을 경우에는 자동으로 'origin'이라는 이름으로 리모트 저장소를 추가함



#### 리모트 저장소를 Pull하거나 Fetch하기

- 로컬에는 없지만 리모트 저장소에 있는 데이터를 모두 가져오기

`$ git fetch <remote>`

- Clone한 이후 수정된 것을 모두 가져오기

`$ git fetch origin`

- 리모트 저장소 브랜치에서 데이터를 가져와서 자동으로 로컬 브랜치와 Merge 시키기

`$ git pull <remote> <branch>`



#### 리모트 저장소에 Push하기

`$ git push  <remote> <branch>`

- 단, Clone한 사람이 여러 명 있을 때 다른 사람이 Push한 후에는 바로 Push할 수 없으며, 먼저 다른 사람이 작업한 것을 가져와서 Merge한 후에 Push할 수 있음



#### 리모트 저장소 살펴보기

`$ git remote show <remote>`



#### 리모트 저장소 이름 바꾸기

`$ git remote rename <oldName> <newName>`



#### 리모트 저장소 삭제하기

`$ git remote remove <remote>`

