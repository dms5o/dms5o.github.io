---
title:  "[C++] std::sort의 사용자 정의 함수 compare"
excerpt: "sort의 정렬 기준을 내 맘대로, vector/pair를 사용해서"
date:   2023-02-25
last_modified_at: 2023-02-25
categories:
  - Cpp
toc: true
toc_sticky: true
---

## compare 함수 정의문  
const는 생략해도 되지만 기본으로 해주자.  
#### Vector + Vector (2차원 벡터)  
```c++
bool compare(const vector<int> &a, const vector<int> &b) {
	/*함수 내용*/
}

int main() {
	vector<vector<int>> vec;
	/*값 할당*/
	sort(vec.begin(), vec.end(), compare);
}
```
<br>

#### Vector + pair 클래스  
```c++
bool compare(const pair<int, int> &a, const pair<int, int> &b) {
	/*함수 내용*/
}

int main() {
	vector<pair<int, int>> vec;
	/*값 할당*/
	sort(vec.begin(), vec.end(), compare);
}
```
<br>

#### Vector + struct 구조체
```c++
struct st {
	/*변수 선언*/
};

bool compare(const st &a, const st &b) {
	/*함수 내용*/
}

int main() {
	vector<st> vec;
	/*값 할당*/
	sort(vec.begin(), vec.end(), compare);
}
```
<br>
<br>

## compare 함수 정의문 예제
#### 오름차순 - 두 번째 원소 기준으로, 같으면 첫 번째 원소 기준으로
*백준 11651번 참고*  
```c++
 //2차원 벡터
bool compare(vector<int> a, vector<int> b) {
	if (a[1] == b[1]) // 두 번째 원소가 같으면
		return a[0] < b[0]; //첫 번째 원소 기즌으로 오름차순
	else
		return a[1] < b[1]; //두 번째 원소가 증가하는 순서로
}
```
```c++
 //Vector + pair
bool compare(pair<int, int> a, pair<int, int> b) {
	if (a.second == b.second)
		return a.first < b.first;
	else
		return a.second < b.second;
}
```
<br>

#### 오름차순 - 첫 번째 원소 기준으로, 같으면 입력 순서대로
*백준 10814번 참고*  
1. stable_sort 사용

```c++
bool compare(const pair<int, string> &a, const pair<int, string> &b) {
	return a.first < b.first; //첫 번째 원소 기준으로 오름차순
}

int main() {
	vector<pair<int, string>> vec;
	/*값 할당*/
	stable_sort(vec.begin(), vec.end(), compare); //stable_sort: 입력 순서 유지
}
```

2. 구조체 사용

```c++
struct st {
	int idx, age; //idx: 입력 순서 저장, age: 첫 번째 원소
	string name; //name: 두 번째 원소
};

bool compare(const st &a, const st &b) {
	if (a.age == b.age) // 첫 번째 원소가 같으면
		return a.idx < b.idx; //입력순서 기즌으로 오름차순
	else
		return a.age < b.age; //첫 번째 원소가 증가하는 순서로
}

int main() {
	vector<st> vec;
	/*값 할당*/
	sort(vec.begin(), vec.end(), compare);
}
```
<br>

<br>
<br>