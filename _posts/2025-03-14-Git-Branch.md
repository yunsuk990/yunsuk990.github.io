---
layout: post
date: 2025-03-14
title: "Git Branch"
tags: [git, ]
categories: [Development, Git, ]
---


## 브랜치


---


[BackLog_Git](https://backlog.com/ja/git-tutorial/stepup/01/)


#### <u>브랜치 생성</u>


![0](/assets/img/2025-03-14-Git-Branch.md/0.png)


![1](/assets/img/2025-03-14-Git-Branch.md/1.png)



{% raw %}
```kotlin
git branch : 분기 목록 확인
git branch [branchname] : 브랜치 생성
```
{% endraw %}


- **`git branch issue1`**


#### <u>브랜치 전환</u>


![2](/assets/img/2025-03-14-Git-Branch.md/2.png)


![3](/assets/img/2025-03-14-Git-Branch.md/3.png)



{% raw %}
```kotlin
git checkout [옵션][branch] : 해당 브랜치로 전환
							-b: 브랜치를 생성하고 전환
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


![5](/assets/img/2025-03-14-Git-Branch.md/5.png)

- **`git checkout master`**
- **`git merge issue1`**

![6](/assets/img/2025-03-14-Git-Branch.md/6.png)

- **`git checkout master`**
- **`git merge issue1`**


{% raw %}
```kotlin
git merge [branchname] : 지정된 브랜치와 병합
```
{% endraw %}




#### <u>브랜치 삭제</u>


![7](/assets/img/2025-03-14-Git-Branch.md/7.png)


![8](/assets/img/2025-03-14-Git-Branch.md/8.png)



{% raw %}
```kotlin
git branch -d [branchname] : 브랜치 삭제
```
{% endraw %}


- **`git branch -d issue1`**


#### <u>병렬로 작업</u>


![9](/assets/img/2025-03-14-Git-Branch.md/9.png)


![10](/assets/img/2025-03-14-Git-Branch.md/10.png)

- **`git branch issue2`**
- **`git branch issue3`**
- **`git checkout issue2`**

![11](/assets/img/2025-03-14-Git-Branch.md/11.png)


![12](/assets/img/2025-03-14-Git-Branch.md/12.png)

- myfile.txt 수정
- **`git add myfile.txt`**
- **`git commit -m “commit 설명 추가”`**

![13](/assets/img/2025-03-14-Git-Branch.md/13.png)


![14](/assets/img/2025-03-14-Git-Branch.md/14.png)

- **`git checkout issue3`**
- myfile.txt 수정
- **`git add myfile.txt`**
- **`git commit -m “pull 설명 추가”`**


#### <u>병합에서 충돌 해결</u>

- 작업이 완료된 주제 브랜치는 결국 통합 브랜치에 통합
- 통합 방법
	- `merge`: 변경 내용의 이력은 그대로 남아 있지만, 이력이 복잡해짐
	- `rebase`: 이력은 단순해지지만, 원래의 커밋으로부터 변경 내용이 변경된다. 따라서 원래 커밋을 움직이지 않는 상태로 만들 수 있음


#### merge로 병합하기


![15](/assets/img/2025-03-14-Git-Branch.md/15.png)


![16](/assets/img/2025-03-14-Git-Branch.md/16.png)

- **`git checkout master`**
- **`git merge issue2`**
- **`git merge issue3`** ⇒ 자동 병합 실패

같은 파일의 같은 행을 다른 내용으로 변경했기 때문에 충돌이 발생



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

![17](/assets/img/2025-03-14-Git-Branch.md/17.png)


![18](/assets/img/2025-03-14-Git-Branch.md/18.png)

- **`git add myfile.txt`**
- **`git commit -m "issue3 브랜치 병합"`**


#### rebase로 병합하기


![19](/assets/img/2025-03-14-Git-Branch.md/19.png)


![20](/assets/img/2025-03-14-Git-Branch.md/20.png)



{% raw %}
```shell
git reset --hard HEAD~ : 원하는 분기로 이동
```
{% endraw %}


- HEAD~ :

![21](/assets/img/2025-03-14-Git-Branch.md/21.png)


![22](/assets/img/2025-03-14-Git-Branch.md/22.png)

- **`git checkout issue3`**
- **`git rebase master`**
- 충돌 부분을 수정하여 다시 commit
- **`git add myfile.txt`**
- **`git rebase —continue`**

![23](/assets/img/2025-03-14-Git-Branch.md/23.png)


![24](/assets/img/2025-03-14-Git-Branch.md/24.png)

- **`git checkout master`**
- **`git merge issue3`**
