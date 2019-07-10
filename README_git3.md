3장 GIT Branch

3.1 branch란 무엇인가
코드를 통채로 복사하고 나서 원래 코들와는 상관없이 독립적으로 개발을 진행할 수 있다. git에서는 브랜치를 만들어 작업하고 나중에 merge하는 방법을 권장한다.

* Git이 데이터를 저장하는 방식
일련의 스냅샷 형태로 기록함. 
https://git-scm.com/book/en/v2/images/commit-and-tree.png

* Git branch 만들기
git의 HEAD 포인터는 초기값으로 master branch를 가리키고 있다. 

-git branch branch_name
// branch를 생성하였지만 HEAD는 아직 master branch를 가리키고 있다. 
// git log --decorate 을 통해 브랜치가 어떤 commit을 가리키는지 알 수 있다.

- git checkout branch_name
// HEAD 포인터가 branch를 가리키게함
// master branch와 testing branch가 존재할때 testing branch로 수정, 커밋을 한 다음 master branch로 돌아오면, testing branch에서 수행했던 것과는 별개로 master branch의 시점으로 돌아와 작업을 수해할 수 있다. 두 작업내용은 서로 독립적으로 존재한다. 때가 되면 두 브랜치를 Merge하면 된다. 

- git checkout -b 1ss53 
// 브랜치를 생성하면서 checkout까지 한번에 처리함

- git log --oneline --decorate --graph --all 
// 현재 브랜치가 가리키고 있는 히스토리가 무엇이고 어떻게 갈라져 나왔는지 보여준다. 

- git의 branch는 현재 가리키고 있는 커밋과 이전 커밋에 대한 포인터를 가지고 있다. 이전 커밋의 정보를 저장하기 때문에 Merge할떄 어디서부터 합쳐야하는지 안다.  

3.2 branch와 merge의 기초

* Merge
master branch에서 갈라져 나온 hotfix branch를 통해 문제를 해결한 후 두 브랜치를 merge해야한다.
1) Fast-forward 
A 브랜치에서 다른 B 브랜치를 Merge 할 때 B 브랜치가 A 브랜치 이후의 커밋을 가리키고 있으면 그저 A 브랜치가 B 브랜치와 동일한 커밋을 가리키도록 이동시킬 뿐이다.
- git checkout master
  git merge hotfix // merge branch가 hoxfix branch를 가리키게 만듦
- git branch -d hoxfix // hoxfix branch를 삭제함

2) 3-way Merge (Recursive strategy)
A branch와 B branch가 조상-후손 관계가 아니고 나뉘어져 나온 개별적 branch인 경우, 각 branch가 가리키는 커밋 두개와 공통 조상 하나를 사용하여 merge한다.
3-way merge의 결과를 별도의 커밋으로 만들고 나서 해단 브랜치가 그 커밋을 가리키도록 이동시킨다. 
- git checkout master
  git merge iss53
- git branch -d iss53

3) 충돌의 기초
-3-way merge가 실패하는 경우
merge하는 두 브랜치에서 같은 파일의 한 부분을 동시에 수정하고 merge하면 git은 해당 부분을 merge하지 못한다. 
git status를 통해 어떤 파일을 merge할 수 없는지 알 수 있다.

3.3 branch management
-git branch
// 현재 모든 branch를 보여줌
- git branch --merged
//merge된 브랜치 목록 보여줌, *붙은 branch가 현재 checkout해서 작업하는 branch
- git branch --no-merged
// merge되지 않은 브랜치 목록 보여줌

3.4 branch workflow
1) long-running branch
testing하는 branch를 두고 안정화된 것들만 master branch에 merge시키는 형태

2) Topic branch
topic branch가 많다. 다양한 풀이법을 해보기 위해 여러 branch를 두고 진행한 후 괜찮은 아이디어만 merge시키고 나머지 버린다.

3.5 Git remote branch
1) remote Refs는 리모트 저장소에 있는 포인터인 레퍼런스다.
- git ls-remote [remote]
// 모든 리모트 Refs 조회 가능
- git remote show [remote]
// 모든 리모트 브랜치와 그 정보를 보여준다. 

2) remote tracking branch는 리모트 브랜치를 추적하는 레퍼런스이며 브랜치이다. 로컬에서 임의로 움직일 수 없고 리모트 저장소에 마지막으로 연결했던 순간에 브랜치가 무슨 커밋을 가리키고 있었는지를 나타낸다. 

-리모트 트래킹 브랜치의 이름은 remote_name/branch_name
ex. git 서버가 있고 이 서버의 저장소를 하나 clone하면 git은 자동으로 origin이라는 이름을 붙인다. origin으로부터 저장소 데이터를 모두 내려받고 master브랜치를 가리키는 포인터를 만든다. 이 포인터를 origin/master라고 부르고 멋대로 조종할 수 없다. 그리고 git은 로컬의 master 브랜치가 origin/master을 가리키게 한다. 이제 이 master 브랜치에서 작업을 시작할 수 있다. 
. git clone -o remote_name// 사용자가 정한대로 remote 이름 생성.

* Fetch 후에 생기는 origin/serverfix 브랜치는 수정 불가능하다. 
- git merge origin/serverfix
//따라서 새로 받은 브랜치의 내용을 Merge해야하는데 이 명령을 사용한다.
-git checkout -b severfix origin/serverfix
// merge하지 않고 리모트 트래킹 브랜치에서 시작하는 새 브랜치를 만들때 이용, origin/servefix에서 시작하고 수정할 수 있는 serverfix라는 로컬 브랜치가 만들어진다. 

3) 정보 동기화하기
- git fetch origin
리모트 서버로부터 저장소 정보 동기화
현재 로컬의 저장소가 갖고 있지 않은 새로운 정보가 있으면 모두 내려받고, 받은 데이터를 로컬 저장소에 업데이트 하고 나서, origin/master 포인터의 위치를 최신 커밋으로 이동시킨다.

4) push 하기
로컬의 브랜치를 서버로 전송하려면 쓰기 권한이 있는 리모트 저장소에 push해야한다. 
- git push remote_name branch_name
ex. git push origin serverfix


5) 브랜치 추적 (사이트 참고)
초기값: 서버로부터 저장소를 clone하면 git은 자동으로 master branch를 origin/master 브랜치의 트래킹 브랜치로 만든다. 
설정: git checkout -b <branch> <remote>/<branch>

6) pull 하기
pull: fetch+merge

7) 리모트 브랜치 삭제
-git push origin --delete serverfix
서버에서 브랜치 하나가 사라진다.

3.6 Rebase하기
한 브랜치에서 다른 브랜치로 합치는 방법, 브랜치를 선형으로 만들어준다. 

-git checkout experiment(branch_name)
 git rebase master(branch_name)
// master이 가리키는 커밋을 experiment가 가리키는 커밋이 가리키게한다. 
-> git rebase master(basebranch) server(topicbranch)

-git checkout master
 git merge experiment
//그리고 나서 master branch를 Fast-forward 시킨다.

*rebase: 브랜치의 변경사항을 순서대로 다른 브랜치에 적용하면서 합친다.
 merge: 두 브랜치의 최종결과만을 가지고 합친다.

- git branch -d client // 브랜치 통합후 필요 없어지면 삭제.

- Rebase의 위험성
이미 공개 저장소에 Push한 커밋을 Rebase하지 마라

- Rebase 한 것을 다시 Rebase하기
위의 문제를 해결해줄 수 있다
