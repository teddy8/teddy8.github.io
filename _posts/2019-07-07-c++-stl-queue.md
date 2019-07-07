---
layout: post   
title:  " C++ STL 큐(queue) "
categories: C/C++
comments: true
tags: c++ c stl queue 큐 deque priority 덱 
author: teddy8  
---
* content
{:toc}

## queue

---

주로 이럴 때 사용합니다.

```
앞과 뒤에서 삽입, 삭제를 자주 할 때 ( 중간에서의 삽입, 삭제는 좋지 않음 )
검색을 거의 하지 않을 때
랜덤 액세스를 해야할 때
서버처럼 받은 패킷들을 차례대로 처리할 때 (이 경우는 deque가 아닌 자체 자료구조를 만들어 사용하기도 함)
```

예제 소스코드(1)

``` c++
#include <iostream>
#include <queue>
using namespace std;

int main()
{
	queue<pair<int, int>> q;

	q.push(make_pair(1, 2));

	int a = 2, b = 3;
	pair<int, int> p = make_pair(a, b);
	q.push(p);

	cout << q.front().first << ' ' << q.front().second;       
	cout << q.back().first << ' ' << q.back().second;          
														  
	while (!q.empty())
	{
		pair<int, int> n = q.front();
		q.pop();

		cout << n.first << ' ' << n.second << '\n';            
															  
	}

	cout << q.size();                                         

	q.push(make_pair(4, 5));
	q.push(make_pair(5, 6));

	queue<pair<int, int>> emt;
	swap(q, emt);

	cout << q.size();
}
```

예제 소스코드(2)

``` c++

#include <iostream>
#include <queue>
using namespace std;

struct room {
	int start;
	int end;
	room(int start, int end) :start(start), end(end) {};
};

bool operator < (room r1, room r2) {
	if (r1.end != r2.end)			
		return r1.end > r2.end;		
	else
		return r1.start > r2.start;
}

int main()
{
	priority_queue<room> pQue;
	int n;						
	int compareNum = -1;		
	int count = 0;

	cin >> n;

	for (int i = 0, s, k; i < n; i++) {
		cin >> s >> k;
		pQue.push(room(s, k));
	}

	while (!pQue.empty()) {
		room r = pQue.top();
		pQue.pop();

		if (compareNum <= r.start) {
			compareNum = r.end;
			count++;
		}
	}

	cout << count;
	return 0;
}

```
