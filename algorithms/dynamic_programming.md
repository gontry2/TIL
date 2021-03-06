# 다이나믹 프로그래밍(동적계획법)

> 한 번 계산한 문제는 다시 계산하지 않도록 하는 알고리즘

* 메모리 공간을 약간 더 사용하여 연산속도를 비약적으로 증가시킬 수 있음
* 보통 '다이나믹'은 프로그램을 실행하는 도중이라는 의미를 갖지만 여기서는 아님
* 대표적인 예: 피보나치 수열
  * 피보나치 수열: 이전의 두항의 합을 현재의 항으로 설정하는 특징이 있는 수열
  * 재귀함수로 구현 시, O(2^n)의 시간복잡도를 갖는다 (지수시간 소요)
* 다이나믹 프로그래밍의 사용조건
  1. 큰 문제를 작은문제로 나눌 수 있다
  2. 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다
* 탑다운 방식 - **메모이제이션(캐싱)**
  * 다이나믹 프로그래밍을 구현하는 방법 중의 한 종류로 탑다운 방식이다
  * 한번 구한 결과를 메모리 공간에 메모해두고(list, dict) 같은 식을 다시 호출하면 메모한 결과를 그대로 가져오는 기법
  * 재귀함수로 구현한다
  * 시간복잡도 O(N)
* 바튼업 방식
  * 다이나믹 프로그래밍을 구현하는 방법 중의 나머지 하나
  * 결과저장용 리스트를 **DP테이블**이라고 한다
  * 반복문을 사용해서 구현한다
  * 시간복잡도 O(N)
  * 재귀함수(메모이제이션, 탑다운방식)은 스택크기가 한정되어 있을 수 있으므로 반복문으로 처리하는 것이 더 좋다 (recursion depth 재귀함수 깊이와 관련된 오류가 발생할 수 있다)
* 다이나믹 프로그래밍과 분할정복(퀵정렬)
  * 큰 문제를 작게 나누어 처리한다는 점에서 동일하다
  * 하지만 다이나믹 프로그래밍은 문제들이 서로 영향을 미치고 있다.
    * 즉, 한 번 해결했던 문제를 다시금 해결한다
    * 그렇기 때문에 이미 해결된 부분 문제에 대한 답을 저장해 놓고, 이 문제는 이미 해결이 됐던 것이니까 다시 해결할 필요가 없다고 반환하는 것이다



### 실전문제

1. 1로만들기
2. 개미전사
3. 바닥공사
4. 효율적인 화폐구성

