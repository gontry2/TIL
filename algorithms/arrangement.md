# 정렬

> 연속된 데이터를 기준에 따라서 정렬하기 위한 알고리즘

* 이진탐색(Binary Search)의 전처리 과정
* 선택정렬, 삽입정렬, 퀵정렬, 계수정렬을 다룸
* 오름차순 -- `reverse`  O(N) --> 내림차순



### 1. 선택정렬

> 매번 '가장 작은 것을 선택'

* N-1번 반복, 스와프 사용
* O(N^2)
* 비효율적, N >= 10,000 성능저하



### 2. 삽입정렬

> 정렬되어 있는 데이터 리스트에서 적절한 위치를 찾은 후에, 그 위치에 삽입

* 리스트의 데이터가 거의 정렬되어 있다면 매우 빠름, O(N)
* O(N^2)



### 3. 퀵정렬

> 기준을 설정한 다음 큰 수와 작은 수를 교환한 후 리스트를 반으로 나누는 방식으로 동작

* 가장 많이 사용 (with 병합정렬)
* pivot 사용 -> 호어분할(Hoare Partition): 리스트에서 첫번째 데이터를 피벗으로 정한다.
* 3 파트
* 재귀 함수 형태로 구현, 탈출 조건? 현재 리스트의 데이터 개수가 1개인 경우
* 최악 O(N^2), 평균 O(NlogN)
* 최악의 경우란? 이미 데이터가 정렬되어 있는 경우



### 4. 계수정렬

> '데이터의 크기범위가 제한되어 정수 형태로 표현할 수 있을 때' 매우 빠른 정렬 알고리즘 (with 기수정렬)

* 가장 큰 Data - 가장 작은데이터 <= 1,000,000
* 시간복잡도 = 공간복잡도 = O(N+K)
* 데이터의 크기가 한정되어 있고, 데이터의 크기가 많이 중복되어 있는 경우



### 5. 정렬라이브러리 (with 병합정렬)

* sorted(), sort()
* O(NlogN)

