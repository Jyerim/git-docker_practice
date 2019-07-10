linux로 c언어 하기: https://modoocode.com/14
2.2 Git의 기초-수정하고 저장소에 저장하기

*modify만 하면-> unstaged 상태
 add하면 -> staged 상태
 commit하면 -> directory에 들어가지
* status
-Untracked file(관리 대상이 아님): working directory에 있는 파일 중 스냅샷에도 staging area에도 포함되지 않은 파일. 처음 저장소를 clone하면 모든 파일은 tracked이면서 unmodified 상태이다. 
-Tracked file( 관리 대상 파일): 이미 스냅샷에 포함되어 있던 파일. 

*git status
- unstaged인 상태와 staged 상태인 file 보여줌
- modify후에 git add file명 해주면 -> staged로 바꿀 수 있음

* git diff
-unstaged인 상태 파일의 수정한 내용을 보여준다
- staged인 상태 파일의 수정 내용을 보기위하여 git diff --cached 사용

* git commit
git commit -m 'commit message 입력'

* Staging Area 생략하기
git commit -a -m 'add new benchmarks'
//-a 옵션을 추가하면 tracked 상태의 파일을 자동으로 Staging Area에 넣는다. git add따로 안해줘도됨

* 파일 삭제하기
-git rm 명령으로 Tracked 상태의 파일을 삭제한 후에(Staging Area에서 삭제하는것) 커밋해야한다. 이 명령은 워킹 디렉토리에 이쓴 파일도 삭제하기 때문에 실제로 파일도 지워짐.

2.3 커밋 히스토리 조회
git log: 저장소의 커밋 히스토리를 시간순으로 보여줌. 가장 최근의 커밋이 가장 먼저나온다.
*옵션
-p: 각 커밋의 diff 결과를 보여준다// git log -p -2: 최근 두개의 결과만 보여줌
--stat: 각 커밋의 통계 정보를 조회할 수 있다. 
--pretty: 히스토리 내용을 어떤형식으로 보여줄지 결정
ex. git log --pretty=oneline// 각 커밋을 한 라인으로 보여줌

* author: 원래 작업을 수행하는 원작자
  commiter: 마지막으로 이 작업을 적용한(저장소에 포함시킨) 사람이다.

2.4 되돌리기
한번 되돌리면 다시 복구할 수 없다. 
* 완료한 커밋을 수정하고 싶을 때: 파일 수정 작업을 하고 Staging Area에 추가한 다음 --ammend 옵션 사용하여 재커밋
git commit --ammend
ex. $ git commit -m 'initial commit'
    $ git add forgotten_file //빠트린 파일 추가해서 
    $ git commit --amend // 하나의 커밋에 기록되게 추가해줌

* 파일 상태를 unstage로 변경하기
git reset HEAD file명

* Modified 파일 되돌리기
git checkout --file명

2.5 리모트 저장소
리모트 저장소: 인터넷이나 네트워크 어딘가에 있는 저장소


2.6 태그
태그: 커밋을 참조하기 쉽도록 알기쉬운 이름을 붙이는 것
한번 붙인 태그는 브랜치처럼 위치가 이동하지 않고 고정된다. 
- lightweight tag: 이름만 붙일 수 있다.
- Annotated tag: 이름을 붙일 수 있다. 태그에 대한 설명도 포함할 수 있다. 서명도 넣을 수 있다. 이 태그를 만든 사람의 이름, 이메일, 태그 만든 날짜정보도 포함 시킬 수 있다.
ex. $ git tag -a tag_name -m "explanation of tag"
 
일반적으로 Release branch에서 annotated tag사용, 로컬에서 일시적으로 사용하는 Topic branch는 lightweight tag사용.

-나중에 tag할 수도 있다. 체크섬을 이용한다.
ex. git tag -a tag_name 체크섬

-tag 공유하기 
git push branch_name tag_name

-tag checkout 하기
