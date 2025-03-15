---
layout: post
date: 2025-03-15
title: "Git Commit 수정하기"
tags: [git, ]
categories: [Development, Git, ]
---


#### 마지막 Commit 수정


`amend` 옵션을 지정하여 Commit을 수행하면 동일한 브랜치 바로 앞의 Commit에 내용을 추가하고 주석을 수정할 수 있습니다.



{% raw %}
```shell
git commit --amend
```
{% endraw %}



**주요 이용 장면**

- 이전에 Commit된 새 파일을 나중에 추가
- 마지막 Commit 내용 수정

[object Promise]

- sample.txt 수정
- `git add sample.txt`
- `git commit --amend`

[object Promise]



#### 과거의 Commit을 무시


`revert` 로 내용을 상쇄하는 commit을 만들 수 있습니다.


**주요 이용 장면**

- 과거에 공개한 commit을 안전하게 상쇄

[object Promise]



{% raw %}
```shell
$ git revert HEAD
 [master d47bb1d] Revert "pull 설명 추가" 
1 files changed, 1 insertions(+), 2 deletions(-)
```
{% endraw %}



[object Promise]



#### Commit 버리기


`reset` 을 사용하면 더 이상 필요하지 않는 commit을 버릴 수 있습니다. 모드를 지정하여 인덱스와 작업 트리의 내용을 반환 여부를 지정할 수 있습니다.


| 모드명   | HEAD 위치 | 색인      | 작업트리    |
| ----- | ------- | ------- | ------- |
| soft  | 변경      | 변경하지 않음 | 변경하지 않음 |
| mixed | 변경      | 변경      | 변경하지 않음 |
| hard  | 변경      | 변경      | 변경      |

undefined
**주요 이용 장면**

- 변경된 인덱스의 상태를 되돌리기 (mixed)
- 최근의 commit을 완전히 버리기 (hard)
- commit만  버리기 (soft)

[object Promise]


reset을 사용하여 commit을 삭제합니다.



{% raw %}
```shell
$ git reset --hard HEAD~~
```
{% endraw %}



[object Promise]

