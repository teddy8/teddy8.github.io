---
layout: post   
title:  " C++ STL 맵(map), 셋(set) "
categories: C/C++
comments: true
tags: c++ c stl map set 맵 셋 multimap multiset
author: teddy8  
---
* content
{:toc}

## map, set

---

주로 이럴 때 사용합니다.

```
[map]
삽입과 동시에 정렬해야할 때
많은 데이터를 보관해야 하고, 검색이 빨라야 할 때
데이터 삽입, 삭제가 적을 때

key와 value의 쌍을 원소로 저장하며,(pair 사용) key는 중복될 수 없다. (중복 key를 저장해야 한다면 multimap)
데이터가 적다면 메모리 낭비와 검색시 오버헤드가 존재한다.

[set]
삽입과 동시에 정렬해야 할 때
많은 데이터를 보관해야 하고, 검색이 빨라야 할 때
많은 데이터가 중복 되어서는 안 되며 빠른 검색으로 key의 존재 여부를 신속하게 알고 싶을때
(중복 key를 저장해야 한다면 multiset)

```

예제 소스코드(1)

``` c++
#include <iostream>
#include <map>

using namespace std;

int main()
{
	map<int, int> room_map;	
	int n;						
	int max = 0;				
	int compareNum = -1;				
	int count = 0;

	cin >> n;

	for (int i = 0, s, k; i < n; i++) {
		cin >> s >> k;

		if (room_map.find(s) != room_map.end() &&
			room_map.find(s)->first < s) {
			continue;
		}

		room_map[k] = s;
	}

	for (map<int, int>::iterator i = room_map.begin(); i != room_map.end(); i++) {
		if (compareNum < i->second) {
			compareNum = i->first;
			count++;
			cout << i->first << " " << i->second << " compareNum = " << compareNum << endl;
		}
	}
	cout << count;

	return 0;
}
```

예제 소스코드(2)

``` c++

#include <iostream>
#include <set>
using namespace std;

int main()
{
	multiset<int> rope;
	int max = -1;			
	int n;				

	cin >> n;

	for (int i = 0, k; i < n; i++) {
		cin >> k;
		rope.insert(k);
	}
	
	multiset<int>::reverse_iterator ri = rope.rbegin();
	int i = 1;

	while (ri != rope.rend()) {
		if (max < *ri * i) {
			max = *ri * i;
		}
		ri++;
		i++;
	}

	cout << max << endl;
	return 0;
}

```
