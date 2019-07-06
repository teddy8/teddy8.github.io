---
layout: post   
title:  " C++ STL 벡터(vector) "
categories: C/C++
comments: true
tags: c++ c stl vector 벡터
author: teddy8  
---
* content
{:toc}

## vector
---
주로 이럴 때 사용합니다.
```
동적 배열처럼 사용할 때
중간에 삽입, 삭제를 거의 하지 않을 때
검색을 거의 하지 않을 때
랜덤 액세스를 자주 할 때
```

주요 함수
```
[iterators]
begin
end
rbegin : 역 순차열의 첫 번째 원소를 가리키는 반복자
rend : 역 순차열의 마지막 원소를 가리키는 반복자

[Element Access]
at : n번째 원소를 참조할 때
operator[] : n번째 원소를 참조할 때 (at보다 빠름)
front : 첫 번째 원소 리턴
back : 마지막 원소 리턴

[Capacity]
empty : 원소 존재 유무 반환
size : 원소 개수
max_size : 담을 수 있는 원소의 최대 개수 리턴
resize : 크기 변경
capacity : vector에 할당된 메모리의 크기 리턴
reserve : 지정한 크기 만큼의 메모리 미리 할당
shrink_to_fit : 사용되지 않는 capacity size 제거

[Modifiers]
clear : 모든 원소 제거
assign : 기존 원소 모두 제거 후 임의의 n개 원소 할당
insert : 삽입
erase : 삭제
push_back : 끝에 삽입
pop_back : 마지막 원소 제거
swap : v1, v2있고 두 개를 swap 할 때
```

예제 소스코드(1)
``` c++
#include <iostream>
#include <vector>

using namespace std;

int main() {
	vector<int> vec;
	vec.push_back(10);  // 맨 뒤에 10 추가
	vec.push_back(20);  // 맨 뒤에 20 추가
	vec.push_back(30);  // 맨 뒤에 30 추가
	vec.push_back(40);  // 맨 뒤에 40 추가

	for (vector<int>::size_type i = 0; i < vec.size(); i++) {
		std::cout << "vec 의 " << i + 1 << " 번째 원소 :: " << vec[i] << std::endl;
	}
}
```
예제 소스코드(2)
``` c++
vector<string> record = {
  {"Enter uid1234 Muzi"},
  {"Enter uid4567 Prodo"},
  {"Leave uid1234"},
  {"Enter uid1234 Prodo"},
  {"Change uid4567 Ryan"}
};
```
예제 소스코드(3)
``` c++
#include <iostream>
#include <vector>
using namespace std;
int main() {

vector<int> vec(N, 0);

for(int i=0;i<N;i++)
	scanf("%d",&vec[i]);

for (vector<int>::size_type i = 0; i < vec.size(); i++)
	std::cout << vec[i] << std::endl;

```
예제 소스코드(4)
``` c++
// 2차원배열 선언방법 arr[6][5]
vector<vector<int>> arr(6, vector<int>(5, 0));
```