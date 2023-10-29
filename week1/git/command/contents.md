# git command
<br/>

1. [git init](#1-git-init)
2. [git status](#2-git-status)
3. [git add](#3-git-add)
4. [git commit](#4-git-commit)
5. [git log](#5-git-log)
6. [git tag](#6-git-tag)
7. [git diff](#7-git-diff)
8. [git reset](#8-git-reset)
9. [git revert](#9-git-revert)
10. [git stash](#10-git-stash)
11. [git branch](#11-git-branch)
12. [git checkout](#12-git-checkout)
13. [git merge](#13-git-merge)
14. [git rebase](#14-git-rebase)
15. [git clone](#15-git-clone)
16. [git remote](#16-git-remote)
17. [git push](#17-git-push)
18. [git fetch](#18-git-fetch)
19. [git pull](#19-git-pull)
20. [git <명령> --help](#20-git-<명령>---help)
---

## 1. git init : 로컬 저장소 만들기
git init는 깃 저장소(repository)를 만드는 명령어이다.
```
git init
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/fccec9b5-57f7-4d98-8b1f-42449d5b8de8" width="550" height="90"/><br/>

저장소가 만들어지면 해당 경로에 다음 그림처럼 .git 폴더가 만들어진 것을 볼 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/a119dc45-4fb7-4ede-87de-fe1b5634a948" width="500" height="170"/><br/>

<br/>

## 2. git status : 작업 디렉터리 상태 확인하기
git status는 현재 작업 디렉터리의 상태를 알려주는 명령어이다.
```
git status
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/b5aff5ca-dc4a-4508-a23c-878cbfc51dce" width="550" height="180"/>

- On branch main : 현재 기본 브랜치, 즉 main 브랜치에 있다는 의미
- No commits yet : 현재 아무런 커밋도 하지 않았음을 의미
- Untracked files : 깃이 기존에 변경 사항을 추적하지 않은 대상을 나타냄
  - fileA.txt 표시 - 기존에 버전을 관리한 적 없던 fileA.txt라는 새로운 파일이 생성되었음을 의미
 
<br/>

## 3. git add : 스테이지에 올리기
git add는 버전으로 만들 파일을 스테이지에 추가할 수 있다.
```
git add <스테이지에 추가할 대상>
git add .
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c04fce7f-6fb0-49d9-bd3f-e0baa33f1e24" width="550" height="180"/>

- `Changes to be committed:` 항목에 fileA.txt 파일이 표기됐으므로 성공적으로 스테이지에 추가된 것을 알 수 있다.

<br/>

## 4. git commit : 커밋하기
git commit은 스테이지에 올린 파일을 커밋하여 새로운 버전을 만드는 명령어이다.
```
git commit --message "커밋 메시지"
git commit -m "커밋 메시지"
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/281ace25-cad8-48b4-b51e-2a37e0aa3961" width="550" height="200"/>

- git log를 입력하면 **커밋 해시, 만든 사람, 커밋이 만들어진 날짜, 커밋 메시지**가 출력된다.
- 커밋 해시 우측의 `HEAD -> master`는 현재 HEAD가 master 브랜치에 있음을 나타낸다.


#### [git commit -am] : 스테이지에 추가(add)와 커밋(commit)을 동시에 수행
깃이 변경 사항을 추적하는(tracked) 파일에만 사용 가능하다.
```
git commit -am "커밋 메시지"
git commit -a -m "커밋 메시지"
git commit --add --message "커밋 메시지"
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/d7d7269e-61c4-4d3b-abc3-927d80caa1ab" width="550" height="370"/>

- modified: 항목 : 수정된 파일 항목
  - fileA.txt 표시 - fileA.txt 파일이 수정되었음을 의미

### [커밋 메시지를 아주 길고 자세히 남기는 경우]
커밋 메시지의 제목뿐 아니라 본문까지 자세하게 작성해야 하는 경우에는 git commit 명령을 사용하면 된다.
```
git commit
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/dec5b731-121e-4104-87cc-5a0a1cb02a1e" width="550" height="100"/><br/>

다음과 같이 커밋 메시지를 입력할 수 있는 Vim 창이 나온다. 제목과 본문을 포함한 자세한 커밋 메시지를 작성하면 되는데, 아직은 입력할 수 없다.
무언가를 입력하기 위해서는 입력 모드로 전환해야 한다. `a` 또는 `i` 를 입력하면 된다. 하단에 **INSERT**가 나온다면 **입력 모드**로 전환된 것이다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/94f7dd85-48f0-47d1-ac1d-08d16bee0596" width="550" height="320"/><br/>

커밋 메시지 제목은 첫 번째 줄에 적을 수 있고, 커밋 메시지의 본문은 제목에서 한 줄 띄고, 세 번째 줄부터 작성할 수 있다.

입력한 내용을 저장하려면 입력 모드에서 **명령 모드**로 전환해야 한다. [Esc]를 누르면 하단의 INSERT가 사라진다.<br/>
:wq를 입력하고 Enter를 누른다. :wq는 :w와 :q를 동시에 입력하는 것과 같다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/4e7ed4cc-f148-4ee5-803c-922f1d9f3ccd" width="550" height="300"/><br/>

다음과 같이 새로운 커밋이 생성된 것을 확인할 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/da69a4bc-939c-4bf6-b66f-79679cb8a771" width="550" height="40"/><br/>

git log 명령으로 세 번째 커밋을 확인한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/95f2748b-4777-4333-a250-76a458d3b2f3" width="550" height="150"/><br/>

<br/>

## 5. git log : 커밋 조회하기
git log는 저장소의 커밋 목록을 보는 명령어이다. 여러 유용한 옵션을 제공한다.
```
git log
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/4dfb8edd-c931-4038-8db1-c8257f02bd6b" width="550" height="200"/><br/>

#### [git log --oneline] : 커밋을 단순한 형태로 조회하기
--oneline은 말 그대로 커밋 목록을 커밋당 한 줄로 출력해주는 옵션이다. 이 명령은 다음과 같이 **짧은 커밋 해시**와 **커밋 메시지 제목**만을 출력한다.
```
git log --oneline
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/12de084e-d1c4-48a1-8c49-18e578bee0f7" width="550" height="100"/><br/>

#### [git log --patch] : 각 커밋의 수정 내역 조회하기
해당 커밋으로 어떤 파일이 어떻게 수정됐는지 알 수 있다.
```
git log --patch
git log -p
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/6569047f-66dd-4154-a267-986d81b9ae91" width="550" height="300"/><br/>

#### [git log --patch] : 각 커밋을 그래프 형태로 조회하기
브랜치가 여러 개로 나뉘어지고 합쳐지는 환경에서 --graph 옵션을 이용하면 브랜치별 커밋의 가독성을 높일 수 있다.
```
git log --graph
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/939ad193-fe61-47d1-85f8-f019a6e24ae3" width="550" height="200"/>

- 출력 결과 왼쪽에 빨간색 그래프를 볼 수 있다.

#### [git log --patch] : 모든 브랜치의 커밋 조회하기
git log 명령은 기본적으로 현재 브랜치를 기준으로 커밋 목록을 조회한다.
--branches 옵션을 붙여 git log 명령을 입력하면 모든 브랜치의 커밋 목록이 출력되기 때문에 어떤 브랜치에서 커밋 목록을 조회하든 동일한 결과를 볼 수 있다.

<br/>

## 6. git tag <태그> : 태그 추가하기
git tag는 HEAD(현재 브랜치의 최신 커밋)가 가리키는 커밋에 태그를 붙이는 명령어이다.
```
git tag <태그>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/4f0cbb50-f33d-4157-8502-2d306b0b4f91" width="550" height="220"/>

- 커밋 목록을 조회하면 가장 최근 커밋인 second commit에 v1.0.0 태그가 붙은 것을 볼 수 있다.

HEAD가 가리키는 커밋이 아닌 특정 커밋에 태그를 붙이려면 git tag <태그> <커밋> 형식으로 명령을 입력해야 한다.
```
git tag <태그> <커밋>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/9008b28b-7ff0-4e5f-810b-2465b6149bae" width="550" height="190"/>

- git log 또는 git log --oneline 명령으로 커밋 해시를 확인 후, git tag <태그> <커밋> 형식으로 명령을 입력한다.
- 다시 git log 또는 git log --oneline 명령으로 첫 번째 커밋에 붙은 태그가 v0.0.1임을 알 수 있다.

#### [git tag --list] : 태그 조회하기
태그 목록을 조회하는 명령은 git tag --list 또는 git tag -l이다. 단순히 git tag라고만 입력해도 된다.
```
git tag
git tag --list
git tag -l
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/e887f0f4-879a-4d28-871a-6f698e75028f" width="550" height="200"/><br/>

#### [git tag --delete] : 태그 삭제하기
태그를 삭제하는 명령은 git tag --delete 또는 git tag -d이다.
```
git tag --delete <태그>
git tag -d <태그>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/06fe81d9-8543-496d-8030-625a1114b577" width="550" height="270"/><br/>

<br/>

## 7. git diff : 최근 커밋과 작업 디렉터리 비교하기
최근 커밋과 현재 작업 디렉터리(현재 작업 내역)의 차이를 출력한다. 이 명령은 보통 커밋한 이후로 작업 디렉터리에서 무엇을 수정했는지 확인하기 위해 사용한다.
```
git diff
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/5f2515f3-c880-4807-ae70-bbcebe48899d" width="550" height="170"/>

- 최근 커밋과 비교했을 때 문자 D가 새롭게 추가됐으니 +D가 출력된다.

#### [git diff --staged] : 최근 커밋과 스테이지 비교하기
스테이지에 추가된 항목과 최근 커밋의 차이를 보여준다.
```
git diff --staged
git diff --cached
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c41c1be2-d679-46b7-a99c-db89e5382604" width="550" height="200"/><br/>

#### [git diff <커밋> <커밋>] : 커밋끼리 비교하기
커밋 간 차이를 비교하는 명령이다. <커밋>에는 비교하려는 커밋의 해시를 입력하면 되는데, 짧은 커밋 해시를 이용해도 무방하다.
```
git diff <커밋1> <커밋2> // <커밋1>을 기준으로 <커밋2>가 달라진 점
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/46c57cd8-07dd-48b3-a045-c4b402a2cd6f" width="550" height="420"/><br/>


커밋을 비교할 때 매번 커밋 해시를 조회하고 붙여넣는 것이 번거롭다면, **HEAD**를 기준으로 비교하면 된다.<br/>
HEAD는 현재 브랜치의 최신 커밋을 가리킨다. HEAD 뒤에 붙는 ^의 개수 또는 HEAD~ 뒤에 붙는 숫자는 ‘HEAD에서 몇 번째 이전을 나타내는지’를 의미한다.
- 세 번째 커밋을 기준으로 네 번째 커밋을 비교하고 싶다면 git diff HEAD^ HEAD 또는 git diff HEAD~1 HEAD를 입력하면 된다.

#### [git diff <브랜치> <브랜치>] : 브랜치끼리 비교하기
git diff <브랜치> <브랜치> 명령으로 두 브랜치의 차이를 알 수 있다.
```
git diff <브랜치1> <브랜치2> // <브랜치1>을 기준으로 <브랜치2>가 달라진 점
```

<br/>

## 8. git reset : 예전 커밋으로 되돌아가기
reset은 저장소를 특정 커밋으로 완전히 되돌리는 방식이다.
```
git reset <되돌아갈 커밋>
```

#### [git reset --soft] : 커밋만 되돌리기
파일을 스테이지로 추가한 순간으로 되돌리는 명령이다.
```
git reset --soft <되돌아갈 커밋>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2906ea39-b0a3-41da-a00f-0d45cdb7dee2" width="550" height="380"/>

- 네 번째 커밋이 사라졌으며, 세 번째 커밋(현재 최근 커밋)과 스테이지의 차이를 보면 문자 D가 추가된 변경 사항이 스테이지로 추가되어 있는 것을 볼 수 있다.
  즉, 세 번째 커밋으로 soft reset하는 것은 곧 네 번째 커밋이 만들어진 그 순간만을 되돌린다는 것을 의미한다.
  정확하게는, 네 번째 커밋을 만들기 위해 파일을 수정하고 변경 사항을 스테이지에 추가한 순간으로 되돌아가는 것이다.

#### [git reset --mixed] : 스테이지까지 되돌리기
스테이지에 추가하고 커밋한 사실을 되돌리는 명령이다. 즉, 파일을 변경만 한 상태로 되돌아간다.<br/>
아무 옵션 없이 git reset 명령을 사용하면 mixed reset이 된다.
```
git reset --mixed <되돌아갈 커밋>
git reset <되돌아갈 커밋>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c8a331c3-462c-48ef-a5c2-7ed87f449e9e" width="550" height="400"/>

- Changes not staged for commit 항목에 fileA.txt 파일이 파일이 있음을 볼 수 있다. 이는 변경만 됐을 뿐 아직 스테이지에 추가되지는 않았음을 의미한다.
  즉, mixed reset은 커밋한 사실과 스테이지에 추가한 사실만을 되돌릴 뿐 파일을 수정한 내역까지 되돌리지는 않는 방식임을 알 수 있다.

#### [git reset --hard] : 작업 디렉터까지 되돌리기
파일을 수정했던 사실까지 완전하게 되돌리는 방식이다.
```
git reset --hard <되돌아갈 커밋>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/769a1d1c-b922-45d5-b01f-91e3519720bc" width="550" height="350"/>

- 네 번째 커밋이 사라졌으며, nothing added to commit but untracked files present (use "git add" to track)를 통해 변경된 파일이 없음을 알 수 있다.
  세 번째 커밋으로 완전하게 리셋된 셈이다.

<br/>

## 9. git revert : 취소된 새로운 커밋 만들기
reset이 특정 커밋으로 되돌아가는 방식이라면, revert는 해당 커밋을 취소한 새로운 커밋을 추가하는 방식이다.<br/>
git reset은 뒤에 되돌아갈 커밋을 명시하는 반면, git revert는 뒤에 취소할 커밋을 명시한다는 점에 주의한다.
```
git revert <취소할 커밋>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0e15ed47-1b66-4580-8a03-aaae1dea878c" width="550" height="130"/><br/>

git revert 명령을 입력하면 Vim 창이 나타난다.<br/>
revert는 기존의 커밋을 취소한 새로운 커밋을 만드는 명령이기 때문에, 커밋 메시지를 작성해야 한다.
지금 보이는 메시지, 즉 하단의 박스는 기본으로 작성된 커밋 메시지이다. 기본으로 작성된 메시지를 커밋 메시지로 삼을 경우, :wq 입력 후 Enter를 누른다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/994276d3-b8d3-4b64-a846-bab49c8d3c66" width="550" height="300"/><br/>
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/fd5382c1-ead9-465d-9ed2-1b7d53bf505e" width="550" height="40"/>

- 새로운 커밋이 성공적으로 만들어졌음을 알 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/bac6a2ed-a0dc-4af5-9f4d-8e07a0e31acc" width="550" height="230"/>

- Revert "third commit"이라는 새로운 커밋이 추가된 것을 볼 수 있다. 추가된 새 커밋은 기존의 세 번째 커밋의 작업 내역을 뒤로 돌리는 커밋이다.
  git diff 명령으로도 확인할 수 있다.

<br/>

## 10. git stash : 변경 사항 임시 저장하기
git stash 명령은 기본적으로 tracked 상태의 파일에 대해서만 사용할 수 있다.<br/>
단순히 git stash 명령을 입력해도 작업이 임시 저장되지만, git stash -m "메시지" 또는 git stash --message "<메시지>" 명령으로 간단한 메시지와 함께 임시 저장할 수도 있다.
이는 임시 저장할 작업에 간단한 메모를 붙여 놓는 것과 같다.
```
git stash
git stash --message "<메시지>"
git stash -m "<메시지>"
```
fileA.txt 파일에 문자 B를 추가한 후, add B라는 간단한 메시지와 함께 현재 수정 내역을 임시 저장해보자. git stash -m "add B" 명령을 입력하면 된다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c0e7f3a8-998a-4e85-947d-c4cbf2ec59e6" width="550" height="80"/>

- fileA.txt 파일을 열어보면, 방금 수정했던 내용은 온데간데없고 첫 커밋을 만든 상태로 돌아간 것을 알 수 있다. B를 추가한 수정 사항이 임시 저장된 것이다.

이번에는 fileA.txt 파일에 문자 C를 추가한 후, add C라는 간단한 메시지와 함께 현재 수정 내역을 임시 저장해보자.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2652f831-a579-4136-8ae2-17214327db52" width="550" height="80"/>

- fileA.txt 파일을 열어보면, 작업한 내역이 사라진(임시 저장된) 것을 확인할 수 있다.

  <img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/d458eef0-0d6b-4741-81ab-4918d60e9fc6" width="400" height="80"/>

#### [git stash list] : 임시 저장된 작업 내역 조회하기
스태시한 작업 목록을 조회하는 명령이다.
```
git stash list
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/26192452-2eb4-4429-b0c8-bcb54af44c5d" width="550" height="90"/>

- 하나는 stash@{0}이고, 또 다른 하나는 stash@{1}이다. 임시 저장된 항목에 붙는 번호, 즉 0과 1 같은 번호는 최근에 저장된 작업일수록 숫자가 작다.
  만일 또 다른 작업을 임시 저장하면 문자 C를 추가한 변경 사항(add C)은 stash@{1}이 되고, 문자 B를 추가한 변경 사항(add B)은 stash@{2}가 된다.

만약, 아무런 메시지도 작성하지 않은 채 git stash 명령을 입력했다면 git stash list의 결과는 다음과 같다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/63e59de9-4684-4d0d-bc4b-30704360e643" width="550" height="90"/>

- WIP는 Work In Progress의 준말이고, 4fdcb74은 스태시가 만들어진 커밋, first commit은 스태시가 만들어졌던 커밋의 커밋 메시지이다.
 
#### [git stash apply] : 임시 저장된 작업 적용하기
임시 저장된 작업을 작업 디렉터리에 적용하는 명령이다.<br/>
스태시 이름을 명시하지 않고 그냥 git stash apply 명령을 입력할 경우 최근에 임시 저장한 항목, 즉 stash@{0}가 적용된다.
```
git stash apply <스태시>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/254cabd3-a43c-48d8-b621-bcc3d00ea1dd" width="550" height="200"/>

- 임시 저장된 변경 사항 stash@{0}를 적용해보면, a.txt 파일이 수정됐다(modified)고 나온다.
  fileA.txt 파일을 확인해보면, 문자 C를 추가했던 stash@{0}의 변경 사항이 적용된 것을 볼 수 있다.

  <img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/229efd15-3df3-40fa-8f42-a064e4ac5513" width="400" height="80"/><br/>

#### [git stash drop] : 임시 저장된 작업 삭제하기
스태시 내의 임시 저장된 작업을 지우는 명령이다.
```
git stash drop <스태시>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/08f49b50-8665-4207-b6ef-a2bbd50b27dc" width="550" height="180"/>

- git stash drop stash@{0} 명령으로 스태시를 삭제하면 기존에 stash@{0}였던 작업(add C)은 목록에서 삭제되고, stash@{1}이었던 작업(add B)이 stash@{0}가 된다.

#### [git stash clear] : 임시 저장된 작업 모두 삭제하기
임시 저장된 작업을 전부 삭제하는 명령이다.
```
git stash clear
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0b168325-dd47-4568-8e75-84cba6512bbc" width="550" height="150"/><br/>

<br/>

## 11. git branch : 브랜치 나누기
브랜치를 만드는 명령이다.
```
git branch <브랜치>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/efa5576b-c43e-4c51-9efb-ce963f853789" width="550" height="120"/>

- `git branch` 명령을 입력하면 현재 브랜치의 목록과 함께 현재 작업 중인 브랜치가 **`*`** 로 표시된다.

#### [git branch --delete] : 브랜치 삭제하기
브랜치를 삭제하는 명령이다.<br/>
브랜치를 삭제하려면 삭제하려는 브랜치가 아닌 다른 브랜치로 체크아웃해야 한다.
```
git branch --delete <브랜치>
git branch -d <브랜치>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/19a8efc3-4c41-4e2b-a40a-6d1f6fa75858" width="550" height="130"/>

- git branch 명령으로 브랜치 목록을 확인하면 foo 브랜치가 삭제됐음을 확인할 수 있다.

<br/>

# 12. git checkout : 체크아웃하기
체크아웃이란 해당 브랜치로 작업 환경을 바꾸는 것을 의미한다. 특정 브랜치로 체크아웃하는 명령은 git checkout <브랜치>이다.
```
git checkout <브랜치>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/29caab64-3296-4a57-8b78-3b4fb434d140" width="550" height="80"/>

- 위와 같이 깃 배시에서 (master)가 (foo)로 변경됐으므로 올바르게 체크아웃했음을 알 수 있다.
<br/>

다음과 같이 master 브랜치에는 커밋 세 개가 쌓여 있고, foo 브랜치에는 커밋 다섯 개가 쌓여 있다고 가정해보자.


<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/bb987f0c-bc9e-4e58-8802-1f9b8c16aedd" width="570" height="170"/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2a3a13b7-f4d3-473d-8f2e-a094f43eb832" width="150" height="290"/><br/>
<br/>

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c603d8bb-8aa5-4198-9352-44235ce4e6c4" width="550" height="120"/><br/>

git checkout main 명령으로 main 브랜치로 체크아웃하는 순간, 파일이 세 개만 남는 것을 확인할 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/4d82eb90-da2e-4031-91fe-d1db5e0edba2" width="550" height="100"/><br/>

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/5ffe8de0-8e96-4a68-a2c3-a4f50f14ea10" width="580" height="170"/><br/><br/>

#### [git checkout -b] : 브랜치를 만듦과 동시에 체크아웃하기
```
git checkout -b <브랜치>
```

<br/>

## 13. git merge : 브랜치 병합하기
브랜치를 병합하는 명령이다.<br/>
```
git merge <브랜치>
```

만일 foo 브랜치를 main 브랜치에 병합하고 싶다면 main 브랜치로 체크아웃한 상태여야 한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/eb284abf-5ed3-40e8-8a05-338a14c69ef9" width="550" height="140"/><br/>

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/bb987f0c-bc9e-4e58-8802-1f9b8c16aedd" width="570" height="170"/><br/>

- 병합 이후 작업 디렉터리를 확인하면 foo 브랜치에서 만들었던 foo_fileD.txt와 foo_fileE.txt 파일을 main 브랜치에서 볼 수 있다.

### [충돌 해결]
브랜치를 병합할 때 충돌이 발생할 수도 있다. 명령어로 브랜치를 병합하는 과정에서 충돌이 발생할 경우, 이를 어떻게 해결할 수 있는지 알아보자.

main 브랜치와 foo 브랜치는 fileA 파일을 서로 다르게 수정했을 때, foo 브랜치를 main 브랜치로 병합하면 충돌이 발생한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/c2487bc2-d957-4549-bd2b-21b30407caf4" width="550" height="100"/>

- 박스 친 부분 속 브랜치 이름을 보면 (main)가 아닌 (main|MERGING)으로 표기되는 것을 볼 수 있다.
  이는 ‘현재 충돌이 발생했으니, 이를 해결하고 다시 커밋하여 병합을 완성하라’는 의미이다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/5e4e33ec-6446-4ef8-87a6-eba499402b92" width="550" height="200"/>
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2ee3ca14-ac18-429c-b592-04a55a547ac6" width="350" height="120"/>

- <<<<<<<, =======, >>>>>>> 기호는 일종의 영역 표기이다.<br/>
  ======= 기호의 **윗부분**은 **HEAD**가 가리키는 브랜치, 즉 main 브랜치의 내용이 적혀 있고, ======= 기호의 **아랫부분**은 **foo** 브랜치의 내용이 적혀 있다.
<br/>

병합의 결과로 main 브랜치의 내용(<<<<<<< 기호와 ======= 기호 사이의 내용)을 선택할지, foo 브랜치의 내용(======= 기호와 >>>>>>> 기호 사이의 내용)을 선택할지 결정해야 한다.

병합의 결과로 main 브랜치의 내용을 반영한다면, 파일의 내용을 다음과 같이 수정한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/5084983f-6457-43f9-bc63-4b2eed92eadb" width="550" height="200"/><br/>

이를 스테이지에 추가하고, 커밋하면 성공적으로 병합된다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/976ab688-146c-48de-b436-af2e8a840a5f" width="550" height="100"/><br/>
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/9702a032-af74-4591-9df1-30da6c189714" width="550" height="300"/><br/>

충돌이 발생했을 경우, 충돌이 발생한 브랜치 중 어떤 브랜치의 내용을 최종적으로 반영할지 **직접 선택**해야 한다.
어떤 내용을 반영할지 직접 선택한 뒤 **충돌이 발생한 파일을 스테이지에 추가하고 커밋**하면 병합이 완료된다.

<br/>

## 14. git rebase : 브랜치 재배치하기
브랜치를 재배치, 즉 브랜치가 뻗어나온 기준점을 옮기는 명령이다.<br/>
재배치하고자 하는 브랜치로 체크아웃되어 있어야 한다.
```
git rebase <브랜치>
```

bar 브랜치를 만든 뒤, bar 브랜치에 두 가지를 커밋하였다.<br/>
첫 번째 커밋(bar first)은 문자 A가 저장된 bar_fileA.txt 파일을 만든 커밋이고, 두 번째 커밋(bar second)은 문자 B가 저장된 bar_fileB.txt 파일을 만든 커밋이다.
bar 브랜치는 현재 main 브랜치의 최신 커밋(Merge branch ‘foo’)에서부터 뻗어나와 커밋 두 개가 쌓여 있는 상태이다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/134dde81-8910-417f-a195-7f3ef5ff9cba" width="550" height="180"/><br/>

master 브랜치에서도 문자 D가 저장된 fileD.txt 파일을 만든 커밋(ninth commit), 문자 E가 저장된 fileE.txt 파일을 만든 커밋(tenth commit)을 만들었다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2eb0afd9-ddbb-4590-a990-19d852b589db" width="550" height="200"/><br/>

bar 브랜치의 현재 기준점은 Merge branch ‘foo’ 커밋이다. 이때, bar 브랜치를 main 브랜치로 재배치하면 bar 브랜치의 기준점이 tenth commit으로 이동하게 된다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/8840c112-bb2e-430e-b9dd-60f5ac4b110e" width="550" height="130"/>

- Successfully rebased and updated refs/heads/bar. 메시지가 떠있으므로 rebase가 성공적으로 이루어졌음을 알 수 있다.

지금까지의 커밋을 확인해 보면 다음과 같다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/edfd3711-92e7-46cf-b8b2-5249f69eaba4" width="550" height="210"/>

- bar first와 bar second의 위치가 달라졌다. rebase한 후 bar first와 bar second는 Merge branch ‘foo’가 아닌 tenth commit 위에 쌓여 있음을 확인할 수 있다.
  다시 말해, bar 브랜치의 기준점이 tenth commit으로 옮겨간 것이다.

참고로 bar 브랜치를 main 브랜치로 재배치한 결과를 다음과 같이 커밋당 한 줄로 출력된 그래프 형태로도 확인할 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0d6a9d01-ce88-4368-8320-4bf40b5b245d" width="550" height="230"/><br/>

<br/>

## 15. git clone : 원격 저장소를 복제하기
원격 저장소를 클론하는 명령이다.<br/>
클론이란 원격 저장소를 복제하는 방법이다.
```
git clone <원격 저장소>
git clone <원격 저장소> <클론받을 경로>
```

다음처럼 Code를 클릭한 다음 원격 저장소 경로를 복사한다.

 <img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/3d4b9d8e-7d49-4486-93d6-6cd5c1e3f914" width="600" height="250"/><br/>

이 저장소를 클론받을 위치에서 깃 배시를 열어주거나 클론받을 경로를 추가해준다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/2d4ec95b-425c-480c-93c5-577c1f34b667" width="550" height="280"/><br/>

원격 저장소가 알맞게 클론되었음을 확인할 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/7ab1469b-b1d1-42fc-aaa4-ee443ca81f50" width="500" height="200"/><br/>

<br/>

## 16. git remote : 원격 저장소를 추가, 조회, 삭제하기
원격 저장소를 추가하고, 조회하고, 삭제할 수 있는 명령이다.

#### [git remote add] : 원격 저장소 추가하기
로컬 저장소에 원격 저장소를 추가하는 명령은 git remote add이다.
```
git remote add <원격 저장소 이름> <원격 저장소 경로>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/9668daf8-8efa-4e04-b777-1e77ba5736e9" width="550" height="70"/>

- 이렇게 원격 저장소를 추가하면 추후 origin이라는 이름으로 https://github.com/silxbro/test-repo.git 과 상호 작용할 수 있다.

#### [git remote] : 원격 저장소 조회하기
추가된 원격 저장소 목록을 조회할 수 있다.
```
git remote
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/834cab2c-01ff-4fed-a1de-1f193ef99233" width="550" height="80"/>

#### [git remote --verbose] : 원격 저장소 이름, 경로 조회하기
원격 저장소의 **이름**과 **경로**를 함께 확인할 수 있다.
```
git remote --verbose
git remote -v
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/599678f1-7244-4d68-85ea-b11c64680b06" width="550" height="100"/>

#### [git remote rename] : 원격 저장소 이름 바꾸기
원격 저장소의 이름을 바꾸는 명령이다.
```
git remote rename <기존 원격 저장소 이름> <바꿀 원격 저장소 이름>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0b9e9a19-725b-4c88-9a99-86be724a28b5" width="550" height="130"/>

#### [git remote remove] : 원격 저장소 삭제하기
추가한 원격 저장소를 삭제하는 명령이다.
```
git remote remove <원격 저장소 이름>
```
<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/08ff509e-8c9c-4cd6-8894-6ee23363af42" width="550" height="110"/>

- 삭제한 후 git remote 명령을 쳤을 때 아무것도 나오지 않는다면 성공적으로 삭제된 것이다.

<br/>

## 17. git push : 원격 저장소에 밀어넣기
push(푸시)는 로컬 저장소의 변경 사항을 원격 저장소에 밀어넣는 방법이다.<br/>
즉, <원격 저장소 이름>으로 <브랜치 이름>의 변경 사항을 푸시하는 명령이다.
```
git push <원격 저장소 이름> <브랜치 이름>
```

로컬 저장소 test-repo에 문자 A가 적힌 fileA.txt 파일을 생성 및 저장한 후, 스테이지에 추가 및 커밋한다.<br/>
다음 명령어로 푸시한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0a39c512-50db-448f-8395-88c9bcf598fa" width="550" height="200"/>

- `-u` 옵션은 처음 푸시할 때 한 번만 사용하면 되는데, 이 옵션과 함께 푸시하면 추후 간단히 git push(또는 git pull) 명령만으로 origin의 main 브랜치로
  푸시(또는 풀)할 수 있다.

fileA.txt 파일에 문자 B를 추가 및 저장한 후, 스테이지에 추가 및 커밋한다. 앞서 -u 옵션과 함께 푸시했기 때문에 단순히 git push만 입력해도 된다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/19400940-cd72-4ff3-83da-7e3518451d07" width="550" height="230"/><br/>
 
원격 저장소에 성공적으로 푸시된 것을 확인할 수 있다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/b071020a-4e2c-43da-9354-a033312b289c" width="750" height="250"/><br/>
 
<br/>

## 18. git fetch : 원격 저장소를 일단 가져만 오기
패치란 원격 저장소의 변경 사항을 로컬 저장소에 병합하지 않고 ‘일단 가져만 오는’ 방법이다.
```
git fetch
git fetch <원격 저장소 이름>
```

깃허브에서 직접 세 번째 커밋을 추가하고, 이를 로컬 저장소로 패치해보자.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/0b1490bd-e78f-4c75-ad9a-34b0ec7890b2" width="550" height="230"/>

- Your branch is behind ‘origin/main’ by 1 commit이라는 메시지를 볼 수 있다. 현재 브랜치는 origin/main 브랜치에 비해 커밋 하나가 뒤쳐진다는 의미이다.
  달리 말해, origin/main 브랜치는 현재 main 브랜치에 비해 한 커밋 앞서 있다는 의미이다.

패치 직후 main 브랜치가 origin/main 브랜치에 비해 커밋 하나가 뒤쳐지는 이유는 패치는 원격 저장소의 변경 사항을 origin/main 브랜치로 가져올 뿐
main 브랜치는 변함이 없기 때문이다. 즉, 패치는 원격 저장소의 변경 사항을 ‘일단 가지고 올 뿐’ 로컬 저장소의 브랜치로 **병합하지는 않는다**는 걸 알 수 있다.
```
[FETCH_HEAD] : 최근에 패치한 브랜치의 최신 커밋
```
패치한 결과를 로컬 저장소의 main 브랜치로 병합한다. main 브랜치로 체크아웃된 상태여야 한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/a8796bd4-e170-4684-b293-bfb24c32503d" width="550" height="220"/>

- git merge FETCH_HEAD 명령을 이용해도 무방하다.

<br/>

## 19. git pull : 원격 저장소를 가져와서 합치기
pull(풀)은 fetch(패치)와 merge(병합)을 동시에 하는 방식이다.
```
git pull
git pull <원격 저장소 이름>
```

깃허브에서 직접 네 번째 커밋을 추가하고, 변경 사항을 로컬 저장소로 pull(풀) 한다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/58df2f85-f362-468b-9fb2-ddb853a54010" width="550" height="220"/>

- git log 명령으로 로컬 저장소의 커밋 목록을 확인해보면, 앞서 깃허브에서 추가한 커밋이 main 브랜치에 병합된 것을 확인할 수 있다.

pull(풀)은 원격 저장소의 변경 사항을 로컬 저장소로 가져옴과 동시에 병합까지 해주는 방식임을 알 수 있다.
다시 말해, pull(풀)은 fetch(패치)와 달리 원격 저장소를 ‘가져와서 합치는’ 방식이다.

<br/>

## 20. git <명령> --help : 매뉴얼 페이지 보기
깃 명령 뒤에 --help를 치면 해당 명령에 대한 자세한 설명이 담긴 매뉴얼 페이지가 브라우저로 열린다.
```
git <명령> --help
```

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/e69d481a-2dff-4886-a949-309ec112a95a" width="550" height="70"/><br/>

브라우저에 다음과 같은 페이지가 열립니다.

<img src="https://github.com/silxbro/woowa-precourse-record/assets/142463332/d7d22a81-a058-47f4-9953-dc8036f6003c" width="550" height="350"/>

- 이 매뉴얼 페이지에는 git commit 명령에 대한 자세한 설명이 담겨 있다.
  git commit 명령은 무엇인지, 어떻게 사용해야 하는지, 이 명령과 함께 사용할 수 있는 옵션에는 어떤 것들이 있는지 등 자세한 설명이 적혀 있다.
  영어로 되어 있지만, 이보다 신뢰성 높고 자세한 자료는 없다고 보아도 무방하다.
