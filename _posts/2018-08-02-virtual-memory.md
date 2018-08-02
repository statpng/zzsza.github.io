---
layout: post
title:  "가상 메모리 이해하기"
subtitle:   "가상 메모리 이해하기"
categories: development
tags: os
comments: true
---

가상 메모리에 대해 작성한 글입니다

---

## 가상 메모리
	- 가상 메모리는 거의 Demand Paging을 사용(다른 방법도 있지만..) 
		- valid 비트 : 메모리에 없으면 0, 있으면 1 
	- backing 스토어와 메모리를 왔다갔다 하는 것은 유사
	- swapping : 프로세스 단위
	- demang paging : 페이지 단위
	- 메인 메모리에 올라와있는지에 따라 어떤 것은 빠르게 어떤 것은 느리게 읽혀짐. 평균적으론 얼마일까?를 나타내는 값
	- p: probability of a page fault = page fault rate
		- local : 지역에 모여있다
		- 컴퓨터는 반복문이 많아 근처를 읽을 확률이 큼
	- 공간적 지역성 : 1000번째를 읽은 후 근접 부분을 읽을 확률이 큼
	- 쫓겨난 페이지. 희생양 
		- 수정되었으면 1
	- First-In First-Out (FIFO)
	- 페이지 참조 열. 몇 번째 페이지를 읽으려고 하는가?
		- 연속된 페이지에선 page faults가 일어나지 않음
		- 따라서 이어지는 숫자는 스킵하는 것이 Page reference string

---

- (1) First-In First-Out (FIFO)
			- 7 0 1 -> 2 0 1 -> 2 3 1 -> 2 3 0 -> ... 
		- 상식에 어긋나는 일
	- 최적 알고리즘 (제일 좋음)
	- 앞으로 가장 오랜 기간동안 사용이 안될 것을 victim으로!
			- 7 0 1 -> 2 0 1 -> 2 0 3 -> 2 4 3 -> ... 
			- 레디큐 안에 프로세스가 여러 개 있을 때, 작업 시간이 제일 작은 것을 선택
			- 작업 시간이 제일 작은 것은 실제로 알 수 없음
	- Rule: Replace the page that has not been used for the longest period of time
	- 과거를 보고 미래를 짐작하는 알고리즘
	- 최근에 가장 적게 사용된 것을 victim으로!(근사화)
	- 대부분 LRU를 사용
		- 저번 학기에 공부를 잘한 사람은 이번 학기에 공부를 잘할 확률이 높다..?
			- 7 0 1 -> 2 0 1 -> 2 0 3 -> 4 0 3 -> ...
- 프레임 : 물리 메모리를 일정한 크기로 나눈 블록, 메모리 단편화 문제를 해결하기 위해 고안된 기법
	- Degree of multiprogramming : 메인 메모리에 올라온 프로세스의 개수
	- 적절한 수를 어떻게 알 수 있을까?
		- 정적 할당 
		- 동적 할당 
	- 프로세스에 맞게 할당
	- etc
		- 프로세스가 35 byte 1 페이지는 10 byte일 경우, 이 프로세스는 4개의 페이지가 필요. 마지막 5 byte를 버려야 함

- [양희재 교수님 운영체제 강의](http://kocw.net/home/search/kemView.do?kemId=978503)
- [introduction to Operating System](https://www.slideshare.net/LukaXavi/introduction-to-operating-system-10938506)



