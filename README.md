1. server에 대한 이해

모든 컴퓨터나 노트북이 서버가 될 수 있지만 보통 우리는 클라이언트로 사용한다. 서버컴퓨터가 따로 있긴하다. 우리는 보통 정보를 요청하는 입장으로만 사용했어 하지만 나도 정보를 제공하고 싶을 수 있자나 그러면 내 컴퓨터에 그 사진들을 올려놓고 다른 컴퓨터들이 정보를 접속해서 확인할 수 있도록 할 수 있다. 내 컴퓨터가 서버역할을 하는 서버 컴퓨터가 된다. 
근데 사용자들이 언제 접속해서 정보를 확인하고 싶은지 모르니깐 보통 서버로 사용하는 컴퓨터들은 24시간 켜놓고 사양도 좋아야한다. 

2. 실행환경과 시스템 기반
개발한 애플리케이션을 릴리스하여 최종 사용자가 이용할 수 있도록 하려면 시스템 기반을 구축하고 그 위에 애플리케이션 실행환경을 마련해야한다. 

1) 실행환경
과거: 자사에서 데이터센터나 기계실을 보유하여 온프레스 환경에서 가동시키던 서버들을 
현재: 클라우드 상의 가상 인스턴스로 옮기고 데이터베이스나 네트워크와 같은 클라우드 서비스를 이용함으로써 실행환경의 구축 범위가 극도로 줄어듦. 
클라우드는 분산환경에서 가동시키는 것이 기본. 

2) 인프라 (시스템 기반)
- 하드웨어:
서버 장비 본체나 데이터를 저장하기 위한 storage, 전원 장치
- 네트워크: 
시스템 이용자가 원격지에서 액세스할 수 있도록 서버들을 연결하기 위한 요구사항. 
- OS:
하드웨어나 네트워크 장비를 제어학 위한 기본 소프트웨어로, 하드웨어의 리소스나 프로세스를 관리함.
클라이언트 OS는 window나 MacOS가 있다. 서버 OS는 Window Server, Unix, Linux등이 있다. 서버 OS는 시스템을 고속 및 안정적으로 가동시키기 위해 필요한 기능으로 특화되어 있다.
-미들웨어:
서버 OS 상에서 서버가 특정 역할을 다하기 위한 기능을 갖고 있는 소프트웨어

.리소스: 사용될 수 있는 어떤 항목을 의미함, 프린터나 메모리, 디스크 드라이브와 같은 장치들이 리소스가 될 수 있다. 커다란 시스템의 일부를 이루는 하드웨어, 소프트웨어, 또는 데이터의 한 구성요소를 말한다. 예를 들어, 네트웍 리소스는 네트웍 상에서 활용 가능한 서버나 프린터 등을 지칭한다. 소프트웨어 리소스에는 프로그램, 유틸리티, 또는 심지어 프로그램 내의 작은 구성요소를 지칭할 수 있다. 데이터 리소스는 액세스 할 수 있는 파일이나 데이터베이스 등이 포함된다.
.프로세스: 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램

3. 기존 vs docker
Virtual dox: 
- cpu나 기타자원들을 가상화해서 컴퓨터를 새로 만드는 것( OS를 가상화 or CPU의 가상화), 서버 기능을 실행시키려면 OS의 실행부터 시작하기 때문에 시간이 걸리고 용량도 많이 차지한다.
Docker: 
- linux의 container기술을 이용하여 가상화하지 않고 process만 격리해서 빠르게 수행, CPU나 메모리는 딱 프로세스가 필요한 만큼만 추가로 사용함
- OS 따로 깔지 않고도 VM 설치한 것과 동일한 효과를 낸다. 이미 움직이고 있는 OS 상에서 프로세스를 실행시키는 것과 거의 똑같은 속도로 빨리 실행시킬 수 있다. 
- 기존 개발환경 공유, real machine에서 돌리는 것과 거의 동일한 효과

4. Docker 개념
- 애플리케이션 실행 환경을 작성 및 관리하기 위한 컨테이너 기반의 오픈소스 가상화 플랫폼
- 다양한 프로그램과 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해준다. 
- docker는 이미지를 만들고 그것을 공유 및 실행시킨다. docker의 이미지는 실행 환경에서 움직이는 컨테이너의 바탕이 된다. 
<image>
 이미지는 애플리케이션의 실행에 필요한 모든 것을 포함하고 있다. 컨테이너는 이미지를 실행한 상태라고 볼 수 있고 추가되거나 변하는 값은 컨테이너에 저장된다. 
 보통 하나의 이미지에 하나의 애플리케이션만 넣어두는 것을 권장한다. 
 이미지는 겹쳐서 사용할 수 있다. 같은 이미지에서 여러개의 컨테이너를 생성할 수 있고 컨테이너의 상태가 바뀌거나 컨테이너가 삭제되더라도 이미지는 변하지 않고 그대로 남아있다. 
 이미지를 통해 한 서버에 여러개의 컨테이너를 실행할 수 있고 수십,수백대의 서버도 문제없다.

- 하나의 Linux 커널을 여러개의 컨테이너에서 공유하고 있다. 컨테이너 안에서 작동하는 프로세스들을 구획화해놓았기 때문에 각 컨테이너는 독립된 공간으로 관리되며 그룹이 다르면 프로세스나 파일에 대한 액세스가 안됨, 하려면 네트워크를 통해서 해야함
<container>
1) 프로세스의 구획화
똑같은 그룹에서 작동하는 프로세스만 액세스할 수 있도록 프로세스를 분리. 다른 그룹에서 프로세스에 접근이 불가
2) 네트워크 구획화
그룹은 하나하나에 IP주소가 할당되어 있다. 다른 그룹에서 프로세스에 접근하기 위해서는 네트워크를 경유해야만 한다.
3) 파일 시스템의 구획화 
그룹에서 사용하는 파일 시스템을 구획화함으로써 조작할 수 있는 명령이나 파일 등을 제한다.

5. Docker 명령
1) Docker 이미지 조작
구문. 이미지명: 태크명

2) 이미지 다운로드 (docker image pull)
구문. docker image pull (옵션) 이미지명:태그명 
//태그명 생략하면 latest를 취득함.
// docker image pull -a centos    -> 모든 태그의 docker 이미지 취득
// docker image pull URL           -> URL 지정하여 이미지 취득

3) 이미지 목록 표시 (docker image ls) 
구문. docker image ls (옵션) 리포지토리명
// docker image ls  

4) 이미지 상세 정보 확인(docker image inspect)
구문. docker image inspect 이미지명:태그명
// 이미지 ID, 작성일, docker 버전, CPU 아키텍처 등이 표시됨

5) 이미지 태그 설정(docker image tag)
구문. docker image tag <Docker Hub 사용자명>/이미지명:태그명
// 태그 붙인 이미지와 원래 이미지의 IMAGE ID는 같다, 바뀌지 않는다.

6) 이미지 검색(docker search)
구문. docker search (옵션) 검색 키워드

7) 이미지 삭제(docker image rm)
구문. docker image rm (옵션) 이미지명
       docker image prune (옵션) // 사용하지 않은 docker image를 삭제할 때 사용

8) docker hub에 로그인(docker login)
구문. docker login (옵션) (서버)
// username, password

9) 이미지 업로드(docker image push)
구문. docker image push 이미지명: 태그명

10) docker hub에서 로그아웃(docker logout)
구문. docker logout 서버명 
// 서버명을 지정하지 않았다면 docker hub에 액세스함.   
