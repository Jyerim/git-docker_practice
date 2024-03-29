참고 사이트: https://git-scm.com/book/ko/v2
Git 1장

1.1 버전관리
버전관리: 파일 변화를 시간에 따라  기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템.

* Version Control System

-Revision Control System: Patch Set( 파일에서 변경되는 부분)을 관리

-CVCS 중앙집중식 버전관리: 
프로젝트를 여러명이 진행할 때 생기는 문제들을 해결하기 위해 개발된 버전 관리.
중앙 서버가 있고 client가 중앙서버에서 파일을 받아서 사용한다.
단점: 서버에 문제가 생기면 히스토리가 다 날라갈 수 있다.

-DVCS 분산 버전 관리 시스템:
서버에 문제가 생겨도 client에게 피해가 가지 않도록 client는 서버로부터 파일을 가져올때 저장소를 히스토리와 더불어 전부 복제한다. 서버에 문제가 생기면 이 복제물로 다시 작업을 시작할 수 있다. client가 모두 서버 복제본을 가지고 있으므로 서버를 복원할 수 있다. 

1.3 Git 기초
보통 버전관리 시스템들은 파일의 변화를 시간순으로 관리하며 파일들의 집합을 관리함.
but git은 데이터를 파일 시스템 스냅샷의 연속으로 취급하고 크기가 아주 작다.  

Git은 데이터를 스냅샷의 스트림처럼 취급한다.
Git은 커밋하거나 프로젝트의 상태를 저장할 때마다 파일이 존재하는 그 순간을 중요하게 여긴다. 파일이 달라지지 않았으면 Git은 성능을 위해 새로 저장하지 않고 이전 상태의 파일에 대한 링크만 저장한다. Git은 데이터를 스냅샷의 스트림처럼 취급한다.

.commit: 변경사항을 기록

* Git의 장점
1) 거의 모든 명령을 로컬에서 실행
네트워크에 있는 다른 컴퓨터가 필요없다. DVCS 방식을 이용하기 때문에 서버에서 히스토리 찾지 않고 로컬에서 조회가능. 즉, 오프라인 상태여두 commit가능! 

2) Git의 무결성
Git은 데이터를 저장하기 전에 항상 체크섬을 구하고 그 체크섬으로 데이터를 관리한다. 체크섬은 SHA-1 해시를 이용하여 만든다. 

3) Git은 데이터를 추가할 뿐
한번 데이터를 추가하면 (커밋하면) 되돌리거나 데이터를 삭제할 방법이 없다. 데이터를 잃어버리기 어렵다. 

-three state
.Committed: 데이터가 로컬 데이터베이스에 안전하게 저장되었다
.Modified: 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않음
.Staged: 현재 수정한 파일을 곧 커밋할 것이라고 표시한 상태

-three stage
.git directory: 프로젝트의 메터데이터와 객체 데이터베이스를 저장하는 곳, 다른 컴퓨터에 있는 저장소를 clone할 때 Git 디렉토리가 만들어진다. 

.Working Tree: 프로젝트의 특정 버전을 checkout한것, git directory 안에 압축된 데이터베이스에서 파일을 가져와서 워킹 트리를 만든다.

.Staging Area: git directory에 있다. 곧 커밋할 파일에 대한 정보를 저장한다. 

flow: working tree에서 파일 수정하면 staging area에 파일을 stage해서 커밋할 스냅샷을 만든다. staging area에 있는 파일들을 커밋해서 git directory에 영구적인 스냅샷으로 저장한다.

.체크섬: Git에서 사용하는 가장 기본적인 데이터 단위
.clone: 복제
.checkout: 사용
