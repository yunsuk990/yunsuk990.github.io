---
layout: post
date: 2025-03-14
title: "Git Branch"
tags: [git, ]
categories: [Development, Git, ]
---


### 브랜치


---


소프트웨어를 개발할 때 하나의 소프트웨어에 대해 여러 멤버가 동시에 기능 추가를 하거나 버그 수정을 하는 등의 경우가 있습니다. 또, 복수의 릴리스 버젼이 존재하는 상태로, 각각을 보수해야 한다고 하는 일도 있습니다.


이와 같이 여러 사람이 동일한 소스코드를 기반으로 서로 다른 작업을 할 때에는 각각 서로 다른 버전의 코드가 만들어 질 수 밖에 없습니다. 이를 위해 여러 개발자들이 동시에 다양한 작업을 할 수 있게 만들어 주는 기능이 브랜치 입니다.



#### 브랜치란?


브랜치란 독립적으로 어떤 작업을 진행하기 위한 개념입니다. 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있습니다.


![0](/assets/img/2025-03-14-Git-Branch.md/0.png)


또, 브랜치를 다른 브랜치와 병합함으로써, 작업한 내용을 다시 새로운 하나의 브랜치로 정리할 수 있습니다.


여러 명이서 동시에 작업을 할 때에 다른 사람의 작업에 영향을 주거나 받지 않도록, 먼저 메인 브랜치에서 자신의 작업 전용 브랜치를 만듭니다. 그리고 작업이 끝난 멤버는, 메인의 브랜치에 자신의 브랜치의 변경 사항을 적용합니다. 이렇게 하면 다른 멤버의 작업에 영향을 받지 않고 자신의 작업을 진행할 수 있습니다. 또한 작업 단위로 이력을 남기면 문제가 발생한 경우에 원인이 되는 작업을 찾아내거나 그에 따른 대책을 세우기 쉬워집니다.


![1](/assets/img/2025-03-14-Git-Branch.md/1.png)



#### 브랜치 생성


issue1이라는 브랜치를 만듭니다.


![2](/assets/img/2025-03-14-Git-Branch.md/2.png)



{% raw %}
```shell
$ git branch // 분기 목록 확인
$ git branch [branchname] // 브랜치 생성
```
{% endraw %}


- **`git branch issue1`**


#### 브랜치 전환


새로 만든 issue1 브랜치에 commit을 추가하려면, 해당 브랜치로 이동해야합니다.


![3](/assets/img/2025-03-14-Git-Branch.md/3.png)



{% raw %}
```shell
$ git checkout [option][branch] // 해당 브랜치로 전환
							-b: //브랜치를 생성하고 전환
```
{% endraw %}


- **`git checkout -b issue1`**
- **`git  add myfile.txt`**
- **`git commit -m “add 설명 추가”`**

![4](/assets/img/2025-03-14-Git-Branch.md/4.png)







> **HEAD**  
> 현재 사용중인 분기의 시작을 나타내는 이름. 기본적으로 master의 시작을 나타냄.   
> ~(칠다) : 몇 세대 전의 부모 지정 ex) HEAD~2  
> ^(캐럿) : 브랜치의 병합으로 부모가 복수 있는 경우, 몇 번째 부모인지 지정 ex) HEAD^








#### <u>브랜치 병합</u>


issue1 브랜치에 변경한 내용을 master 브랜치에 통합합니다.


![5](/assets/img/2025-03-14-Git-Branch.md/5.png)



{% raw %}
```shell
$ git merge [branchname]  // 지정된 브랜치와 병합
```
{% endraw %}



브랜치를 HEAD가 가리키는 브랜치로 병합합니다. 


![6](/assets/img/2025-03-14-Git-Branch.md/6.png)

- **`git checkout master`**
- **`git merge issue1`**

master 브랜치가 가리키는 commit이 issue1과 같은 위치를 이동했습니다. 이 병합은 fast-forward (빨리감기) 병합입니다.


![7](/assets/img/2025-03-14-Git-Branch.md/7.png)

- **`git checkout master`**
- **`git merge issue1`**

master 브랜치가 가리키는 commit이 issue1과 같은 위치를 이동했습니다. 이 병합은 fast-forward (빨리감기) 병합입니다.

undefined

#### 브랜치 삭제


issue1 브랜츼 내용이 master에 통합되었으므로 삭제합니다.


![8](/assets/img/2025-03-14-Git-Branch.md/8.png)


![9](/assets/img/2025-03-14-Git-Branch.md/9.png)



{% raw %}
```shell
$ git branch -d [branchname]  //브랜치 삭제
```
{% endraw %}


- **`git branch -d issue1`**


#### <u>병렬로 작업</u>


두 개의 분기 (브랜치)를 만들고 병렬로 작업해봅니다.


![10](/assets/img/2025-03-14-Git-Branch.md/10.png)


![11](/assets/img/2025-03-14-Git-Branch.md/11.png)

- **`git branch issue2`**
- **`git branch issue3`**
- **`git checkout issue2`**

![12](/assets/img/2025-03-14-Git-Branch.md/12.png)


![13](/assets/img/2025-03-14-Git-Branch.md/13.png)

- myfile.txt 수정
- **`git add myfile.txt`**
- **`git commit -m “commit 설명 추가”`**

![14](/assets/img/2025-03-14-Git-Branch.md/14.png)


![15](/assets/img/2025-03-14-Git-Branch.md/15.png)

- **`git checkout issue3`**
- myfile.txt 수정
- **`git add myfile.txt`**
- **`git commit -m “pull 설명 추가”`**


#### 병합에서 충돌 해결

- 작업이 완료된 주제 브랜치는 결국 통합 브랜치에 통합
- 통합 방법
	- `merge`: 변경 내용의 이력은 그대로 남아 있지만, 이력이 복잡해집니다.
	- `rebase`: 이력은 단순해지지만, 원래의 커밋으로부터 변경 내용이 변경됩니다. 따라서 원래 커밋을 움직이지 않는 상태로 만들 수 있습니다.


#### merge로 병합하기


![16](/assets/img/2025-03-14-Git-Branch.md/16.png)


![17](/assets/img/2025-03-14-Git-Branch.md/17.png)

- **`git checkout master`**
- **`git merge issue2`**
- **`git merge issue3`** ⇒ 자동 병합 실패

같은 파일의 같은 행을 다른 내용으로 변경했기 때문에 충돌이 발생합니다.



{% raw %}
```shell
$ git merge issue3
Auto-merging myfile.txt 
CONFLICT (content): Merge conflict in myfile.txt 
Automatic merge failed; fix conflicts and then commit the result.

$ vi myfile.txt
<<<<<<< HEAD
myfile
=======
hello
pull 설명 추가
>>>>>>> issue3
```
{% endraw %}


- 충돌 부분을 수정하여 다시 commit

![18](/assets/img/2025-03-14-Git-Branch.md/18.png)


![19](/assets/img/2025-03-14-Git-Branch.md/19.png)

- **`git add myfile.txt`**
- **`git commit -m "issue3 브랜치 병합"`**


#### rebase로 병합하기


![20](/assets/img/2025-03-14-Git-Branch.md/20.png)


![21](/assets/img/2025-03-14-Git-Branch.md/21.png)



{% raw %}
```shell
git reset --hard HEAD~ // 원하는 분기로 이동
```
{% endraw %}


- HEAD~ :

![22](/assets/img/2025-03-14-Git-Branch.md/22.png)


![23](/assets/img/2025-03-14-Git-Branch.md/23.png)

- **`git checkout issue3`**
- **`git rebase master`**
- 충돌 부분을 수정하여 다시 commit
- **`git add myfile.txt`**
- **`git rebase —continue`**

![24](/assets/img/2025-03-14-Git-Branch.md/24.png)


![25](/assets/img/2025-03-14-Git-Branch.md/25.png)

- **`git checkout master`**
- **`git merge issue3`**

[bookmark](https://backlog.com/ja/git-tutorial/stepup/01/)


[bookmark](https://yozm.wishket.com/magazine/detail/2827/)

