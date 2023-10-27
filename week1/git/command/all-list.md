# git command list
<br/>

|분류|명령어|기능|
|:---|:---|:---|
|git `init`|git init|로컬 저장소 만들기|
|git `status`|git status|작업 디렉터리 상태 확인하기|
|git `add`|git add <스테이지 추가 대상><br/>git add .|<스테이지 추가 대상>을 스테이지에 올리기<br/>모든 변경 사항을 스테이지에 올리기|
|git `commit`|git commit<br/>git commit **--message/-m** "<커밋 메시지>"|자세한 커밋 메시지와 함께 커밋하기<br/><커밋 메시지>로 커밋하기|
|git `log`|git log<br/>git log **--oneline**<br/>git log **--patch/-p**<br/>git log **--graph**<br/>git log **--branches**|커밋 목록 조회하기<br/>커밋 목록을 한 줄로 조회하기<br/>커밋별 변경사항 목록 조회하기<br/>커밋 목록을 그래프로 조회하기<br/>모든 브랜치의 커밋 목록 조회하기|
|git `tag`|git tag <태그><br/>git tag <태그> <커밋><br/>git tag<br/>git tag **--list/-l**<br/>git tag **--delete/-d** <태그>|<태그> 추가하기<br/><커밋>에 <태그> 추가하기<br/>태그 목록 조회하기<br/>태그 목록 조회하기<br/><태그> 삭제하기|
|git `diff`|git diff<br/>git diff **--staged**<br/>git diff <커밋> <커밋><br/>git diff <브랜치> <브랜치>|최근 커밋과 작업 디렉터리 비교하기<br/>최근 커밋과 스테이지 비교하기<br/><커밋>끼리 비교하기<br/><브랜치>끼리 비교하기|
|git `reset`|git reset **--soft** <되돌아갈 커밋><br/>git reset **--mixed** <되돌아갈 커밋><br/>git reset <되돌아갈 커밋><br/>git reset **--hard** <되돌아갈 커밋>|<되돌아갈 커밋>으로 soft reset하기<br/><되돌아갈 커밋>으로 mixed reset하기<br/><되돌아갈 커밋>으로 mixed reset하기<br/><되돌아갈 커밋>으로 hard reset하기|
|git `revert`|git revert <취소할 커밋>|<취소할 커밋>이 취소된 새로운 커밋 만들기|
|git `stash`|git stash<br/>git stash **--message/-m** "<메시지>"<br/>git stash **list**<br/>git stash **apply** <스태시><br/>git stash **drop** <스태시>|변경 사항 임시 저장하기<br/><메시지>와 함께 변경 사항 임시 저장하기<br/>임시 저장된 작업 내역 조회하기<br/>임시 저장된 작업 적용하기<br/>임시 저장된 작업 삭제하기|
|git `branch`|git branch<br/>git branch <브랜치><br/>git branch **--delete/-d** <브랜치>|브랜치 목록 조회하기<br/><브랜치> 만들기<br/><브랜치> 삭제하기|
|git `checkout`|git checkout <브랜치><br/>git checkout **-b** <브랜치>|<브랜치>로 체크아웃하기<br/><브랜치> 생성하고 체크아웃하기|
|git `rebase`|git rebase <브랜치>|<브랜치>로 재배치하기|
|git `clone`|git clone <원격 저장소>|<원격 저장소>를 복제하기|
|git `remote`|git remote **add origin** <원격 저장소 이름><원격 저장소><br/>git remote<br/>git remote **--verbose/-v**<br/>git remote **rename** <기존 이름> <바꿀 이름><br/>git remote **remove** <원격 저장소 이름>|<원격 저장소> 추가하기<br/>원격 저장소 이름 조회하기<br/>원격 저장소 이름과 경로 조회하기<br/>원격 저장소 이름 변경하기<br/>원격 저장소 삭제하기|
|git `push`|git push <원격 저장소 이름> <브랜치>|<원격 저장소 이름>에 <브랜치>를 밀어넣기|
|git `fetch`|git fetch <원격 저장소 이름>|원격 저장소를 일단 가져만 오기|
|git `pull`|git pull <원격 저장소 이름>|원격 저장소를 가져와서 합치기|
||git <명령> --help|<명령>에 대한 매뉴얼 페이지 보기|
