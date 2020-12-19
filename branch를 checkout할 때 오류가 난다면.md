# branch를 checkout할 때 오류가 난다면...

 업데이트된 원본 저장소로 부터 fork되어있는 내 저장소 데이터를 업데이트하기 위해 branch를 추가하고 checkout하려는 데 아래와 같은 에러메시지가 발생한다.

>$ git checkout master
>
>error: pathspec 'master' did not match any file(s) known to git.

## 원인

해당 에러는 master한 이름의 branch에 연결하지 못했다는 의미이다. 분명 나에게는 master branch가 있는데  왜 안되는 건지 의아할 것이다. 조금만 생각해보면 이전에 fork한 원본 저장소의 데이터를 불러오기 위해 master branch를 한 번도 checkout하지 않은 상태에서 upstream 원격 저장소 주소를 추가하고 나의 로컬 저장소로 fetch했었다. 그러면서 master라는 이름의 브랜치가 두 개 (origin/master, upstream/master) 가 생겼다.

그렇기 때문에 fetch이 후 실제 branch 정보들이 내 로컬로 저장이 되면서 같은 이름의 branch가 존재하게되었고 결과적으로 git은 어떤 곳에 연결해야 하는지 분명하지 않아 에러가 발생한 것이다.

## 해결

도움말을 보면 다음과 같은 내용이 있다.

If <branch> is not found but there does exist a tracking branch in exactly one remote (call it <remote>) with a matching name, treat as equivalent to

​     $ git checkout -b <branch> --track <remote>/<branch>

평소에 git checkout branch_name을 할 때는 같은 이름의 branch 이름이 하나이기 때문에 자동으로 remote와 연결된다는 것이다. 

즉, 명시적으로 checkoute할 master를 어떤 저장소의 master와 연결할지 명시주면 된다.

**$ git checkout -b master --track origin/master**





## (정리) fork한 저장소를 원본 저장소의 데이터의 최신으로 동기화하기

 1.먼저 로컬로 clone한 프로젝트에서 터미널을 열어 현재 github 저장소의 원격 주소의 목록을 확인한다.

​	git remote -v

​	origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)

​	origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

​	clone한 저장소의 원격 주소만이 있을 것이다.



2. 로컬로 clone한 프로젝트에서 터미널을 열어 원본(upstream) 저장소의 github 주소를 추가한다.

   git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

   

3. 잘 추가됐는지 확인

​	git remote -v

​	origin   https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)

​	origin   https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)

​	upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)

​	upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)



4. 동기화하기위해 원본을 fetch

   git fetch upstream

   

5. 내 로컬 master branch를 checkout

   git checkout -b master --track origin/master

   

6. 최종 동기화하기 (나의 upstream/master와 master를 합치기(merge))

   git merge upstream/master

   

7. push하기

   git push



## (정리) fork한 저장소에서 원본저장소로 PR(Pull Request 하기)

 1.브랜치를 새로 만든다.

​	**git checkout -b 브랜치명**

2. 수정한 데이터를 add, commit 후 push

   push할 때는 브랜치이름을 꼭 명시해 주어야한다.

   **git push origin 브랜치명** 

   // 브랜치명 브랜치의 수정 내역을 origin으로 push한다.



3. fork한 저장소 웹페이지에 가보면 Compare & pull request 버튼이 활성화되어 있다.

   클릭하여 메시지를 써주고 PR를 생성한다.



4. 관리자가 merge했다면 업데이트된 원본 저장소와 로컬테이터를 동기화 해준다.

   **git pull remote이름**

   remote이름은 (원본저장소 이름)

   --> git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git  였다면 remote이름은 upstream

   

   그리고 브랜치는 삭제해준다.

   **git branch -d 브랜치명**



자신은 수정사항없이 다른사람이 하던 최신 작업을 이어서 하고 싶을 때는 **git pull remote이름** 으로 동기화하여 **1번~4번**을 반복하면 된다.