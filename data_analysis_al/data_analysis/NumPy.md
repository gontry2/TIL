# NumPy (Numeric Python)

> 행렬이나 벡터와 같은 다차원 데이터의 연산을 쉽게 처리할 수 있도록 지원하는 파이썬 라이브러리.
>
> 데이터 구조 외에 수치 계산을 위한 효율적인 기능을 제공한다.



## ndarray

* numpy에서 제공하는 n차원 배열

* python의 리스트와 유사하나 python과 다르게 모두 같은 타입을 사용해야함

* python의 list 보다 메모리 효율이나 실행속도에서 우위

* `arr = np.array([(1, 2, 3), (4, 5, 6)], dtype=np.float64)`

* 속성

  * `ndim`: 차원의 개수
  * `shape`: 차원의 개수와 각 차원의 요소를 tuple로 표현
  * `size`: 요소의 총 개수

* 메소드

  * `len(array)`: 첫번째 차원의 요소 개수를 리턴. (1차원은 size, len() 결과값이 동일함)
  * `reshape(shape)`: 차원을 변경함. View 형태로 만들어짐. -1을 하면 알아서 계산해서 넣으라는 뜻
  * `ravel()`: ndarray의 모든 요소가 포함된 1차원 vector를 view형태로 리턴
  * `arr.reshape((2, -1)).copy()`: list 형태로 만들어짐. 원소의 개수가 같지 않으면 일어나지 않음(cf. resize())
  * `astype(dtype)`: dtype을 변경함. float64 -> int32: 소수점 이하 버림
  * `resize(shape)`:  reshape와 유사. view가 아닌 원본이 변경됨. 원본의 개수가 달라도 됨(0으로 채워지거나 버림처리됨. cf. reshape())

* 생성방법

  * python의 list활용. 

    ```python
    list = [[1,2,3],[4,5,6]] #[(1,2,3), (4,5,6)] 가능 2 x 3 ndarray
    arr = np.array(list, dtype=np.float64)
    ```

  * `zeros(shape)`, `ones(shape)`, `full(shape, value, dtype=np.float64 )`, `np.empty(shape)`

    ```python
    import numpy as np
    arr = np.zeros((3, 4)) # 0으로 채운 numpy array를 만들어요.
                           # shape을 명시해야해요
                           # dtype은 np.float64로 지정.
    
    arr = np.ones((2, 5)) # 1으로 채운 numpy array를 만들어요.
    arr = np.full((3, 5), 5, dtype=np.float64)
    arr = np.empty((3, 3)) # 3 x 3 ndarray를 생성하는데 초기값을 주지않음
                           # 내가 원하는 shape의 공간만 설정
                           # 생성 속도가 빠름(cf. zeros())
    ```

  * ` np.zeros_like(arr, dtype=np.float64)`, ` np.ones_like(arr, dtype=np.float64)`

  * `arange(start, stop, step)`

    * python의 range와 유사. 
    * 주어진 범위 내에서 지정한 간격으로 연속적인 원소를 가진 ndarray를 생성. 
    * stop은 exclusive

  * `linspace(start, stop, num)`:

    * start~stop의 범위에서 num개의 숫자를 균일한 간격으로 생성해서 ndarray를 만드는 함수
    * stop은 inclusive
    * 원소 간의 간격 구하는 식: (stop-start)/(num-1)



* 생성방법 - 랜덤값 기반으로 생성
  * `np.random.normal(mean, std, shape)`: 정규분포 확률밀도함수에서 실수 표본을 추출해서 ndarray생성(평균과 표준편차 활용)
  * `np.random.rand(d0, d1, d2...)`: 실수를 추출하는데, [0, 1) (0이상 1미만)범위에서 추출하고 균등분포로 추출
  * `np.random.randn(d0, d1, d2...)`: 실수를 추출, 표준정규분포에서 난수를 추출함. 평균이 0 표준편차가 1
  * `np.random.randint(low, high, shape)`: 균등분포 확률밀도함수에서 난수를 추출하는데 정수값을 난수로 추출
  * `np.random.random(shape)`: [0, 1) 균등분포에서 실수 난수를 추출!! np.random.rand(d0, d1, d2....)와 동일, 인자만 다름



## 랜덤관련 함수

1. 난수의 재현

   * 랜덤값이 계속 똑같이 나오게 하는 함수. 실제로는 특정 알고리즘의 결과물이기 때문에 초기값을 고정해주면 된다.

     ```python
     np.random.seed(10)
     arr = np.random.randint(0, 100, (10,))
     ```

2. `shuffle(arr)`

   * ndarray의 순서를 랜덤하게 바꿔줌
   * return하는 것이 아니라 ndarray자체가 변형됨

3. `choice()`

   * ndarray안에서 일부를 무작위로 선택하는 기능 (sampling)

   * `np.random.choice(arr, size, replace, p)`

     * arr: 정수(0~정수의 ndarray 자동생성) 혹은 ndarray
     * size: 정수값, 샘플의 숫자
     * replace: Boolean(True, False), True: 한번 선택한 데이터를 다시 샘플링 할 수 있음
     * p: 각 데이터가 샘플링될 확률을 가지고 있는 ndarray

     ```python
     arr = np.random.choice(5, 10, replace=True, p=[0.2, 0, 0.3, 0.4, 0.1])
     ```

     

## Indexing & Slicing

1. 1차원배열
   * arr[3] : indexing
   * arr[1:4] : slicing
   * arr[:-1] :  처음(인덱스 0) : 끝에서 첫번째
   *  arr[1: -1:2]: 1부터: 끝에서 첫번째까지의 배열 중 간격 2
2.  2차원 배열
   * arr[1, 2]
   * arr[1] [2]
   * arr[2, :] : indexing과 slicing같이 사용
   * arr[1:3, :] : 1행, 2행 두개의 행을 가져옴
   * arr[1:3, :2] : 1행, 2행 중 0열 1열의 원소값 가져옴
3.  **Boolean Indexing**
   * ndarray의 각 요소의 선택여부, True, False로 구성된 boolean mask를 이용하여 지정하는 방식
   * boolean mask의 True에 해당하는 index만을 조회하는 방식
     * arr % 2 : 각각의 원소에 스칼라연산 => broad casting
     * arr % 2 == 0 : [True, False, ...] => boolean mask
     * arr[arr%2 == 0] : boolean mask를 씌워서 true인 것만 인덱싱 => boolean indexing
4.  **Fancy Indexing**
   * ndarray에 index배열을(list) 전달하여 배열요소를 참조하는 방식
   * 일반적인 2차원 배열의 인덱싱과 슬라이싱
     * arr[2, 2]: schalar 결과값 #10
     * arr[1:2, 2]: slicing, indexing 1차원 결과값 #[6]
     * arr[1:2, 1:2]: slicing 2차원 결과값 #[[5]]
   * Fancy Indexing
     * arr[[0,2], 2] : index 배열 #[2, 10]
     * arr[[0,2], 2:3] : 2차원배열 #[[2] [10]]
     * 주의> 행과 열에 동시에 fancy indexing을 적용할 수 없다 ( arr[[0, 2],[1, 3]] )
     * `np.ix_`: 행과 열에 동시에 fancy indexing 사용할 수 있도록 하는 함수 ( arr[np.ix_( [0, 2], [1, 3] )] )



## 사칙연산과 행렬곱

* python에서 list를 `+` 연산자를 사용해서 연산하면 concatenation
* ndarray에서 `+` 연산자는 vector, matrix 연산

1.  **사칙연산**

   * shape이 같아야 한다

   * list + list

   * list + 정수(schalar):

     * shape이 안맞는 경우, ndarray가 broad casting을 수행(행렬곱연산은 브로드캐스팅이 일어나지 않음)

     * 기본적으로 자신을 복제하기 때문에 원소수가 맞지 않으면 실행할 수 없음
     * 2 x 3 ndarray에 1 x 2 연산의 경우 실행할 수 없음

     

2. **행렬곱연산**

   * 두 행렬간의 행렬곱은 `np.dot()`, `np.matmul()`로 수행 가능

   * `np.dot(A, B)`에서 A행렬의 열 vector와 B행렬의 행 vector의 size가 같아야 함 ( 2 x 3 dot 3 x 2)

   * 만약 크기가 다르다면? `reshape()`, `resize()`를 이용해서 맞춰준 후 연산

   * **행렬곱 연산을 하는 이유?** 

     * 만약에 행렬곱 연산이 없으면 matrix 연산은 같은 크기로만 수행해야함

     * 하지만 행렬곱 연산을 이용해 행렬곱 조건만 만족시키면, 다양한 크기의 행렬을 연속적으로 이용해서 특정작업을 수행할 수 있음

     * 머신러닝, 이미지처리(CNN)에서 많이 사용

     * 예) 입력 : 32 x 32 matrix (이미지파일-흑백) 

       ​      출력 : 32 x 10 matrix (다양한 처리가 적용된 이미지)

       ​      행렬곱 : (32 x 32) dot (32 x 128) dot (128 x 64) dox (64 x 10) = (32 x 10)

       

## 전치행렬(Transpose)

* 전치행렬은 원본행렬의 행은 열로, 열은 행으로 바꾸는 행렬을 의미한다
* 전치행렬의 표현은 윗첨자로 T를 이용한다
* `T` : 전치행렬 return
* 1차원 vector는 2차원 vector로 reshape() 한 후에 처리한다 ( arr.reshape(1,4).T )



## 순환자(Iterator)

* for문이 아닌 순환자를 사용하는 이유? 

  * 3차원 이상일 경우 로직이 복잡해진다(중첩 for문)

  *  `c_index` : C언어에서 사용하는 index기법을 사용, 1차원 vector에 사용

    ```python
    import numpy as np
    
    arr = np.array([1,2,3,4,5])
    it = np.nditer(arr, flags=['c_index'])
    
    while not it.finished: # iterator가 지정하는 위치가 끝이 아닐동안 반복
        idx = it.index # iterator가 현재 가리키는 곳의 index숫자를 가져옴
        print(arr[idx], end=' ')
        it.iternext() # iterator를 다음 요소로 이동시키는 작업
    ```

  * `multi_index`: tuple형식으로 index 반환, 다차원 vector에 사용

    ```python
    arr = np.array([[1,2,3], [4,5,6]])
    it = np.nditer(arr, flags=['multi_index'])
    
    while not it.finished:
        idx = it.multi_index
        print(arr[idx], end=' ')
        it.iternext()
    ```

    

## 비교연산

* 사칙연산과 마찬가지로 비교연산도 같은 index끼리 수행됨
  * arr1 == arr2 : boolean mask  # [False, True, ...]
* `array_equal()`: 2개의 ndarray가 같은 데이터를 갖고 있는 지 비교할 때 사용
  * np.array_equal(arr1, arr2) # True



## 집계함수 & axis (축)

* 집계함수를 사용하는 이유?
  * 로직으로 연산을 수행하는 것보다 훨씬 성능이 좋다 ( `%%time`로 측정 가능 )
* 집계함수
  * `arr.sum()`, `np.sum(arr)` : 합
  * `np.cumsum(arr)` : 누적합. [ 1 3 6 .. ] 1차원 vector형태
  * `np.mean(arr)` : 평균
  * `np.max(arr)` : 최대값
  * `np.min(arr)` : 최소값 
  * `np.argmax(arr)` : 최대값의 순번(index)
  * `np.argmin(arr)` : 최소값의 순번(index)
  * `np.std(arr)` : 표준편차
  * `np.exp(arr)` : 자연상수.. 2.71828183의 승
  * `np.log10(arr)` : 상용로그 

* Numpy의 집계함수는 axis를 기준으로 계산이 됨
  * 만약 axis를 지정하지 않으면, None으로 지정되어 함수의 대상범위를 전체 ndarray로 지정함
  * 1차원은 축 1개, 2차원은 축 2개, 3차원은 축 3개
  * 1차원인 경우, axis=0은 가로방향(1)
  * 2차원의 경우(2 x 3), axis=0은 세로방향(3), axis=1은 가로방향(2)
  * 3차원의 경우(2 x 2 x 3), axis=0은 depth(2 x 3), axis=1은 세로방향(2 x 3), axis=2는 가로방향(2 x 2)



## 정렬

* Numpy array는 axis를 기준으로 정렬하는 `sort()` 함수를 제공
* 만약 axis를 지정하지 않으면 -1값으로 지정 => 마지막 axis(열)
* `arr.sort()` : 원본을 정렬. return값은 None
* `np.sort()` : 정렬된 결과 ndarray를 return
  * np.sort(arr) : 오름차순 정렬(default)
  * np.sort(arr)[::-1] : 역순으로 정렬
* 2차원 ndarray의 정렬
  * np.sort(arr, axis=0) : 세로방향 오름차순 정렬
  * np.sort(arr, axis=1) : 가로방향 오름차순 정렬



## 원소 추가 & 제거

1. 원소(행,열) 추가

   * `arr.append()`

   * `np.concatenate((arr1, arr2), axis)`

     * ndarray에 row(s) 혹은 column(s)을 추가하기 위한 함수

       ```python
       import numpy as np
       
       arr = np.array([[1, 2, 3], [4, 5, 6]], dtype=np.int32)
       new_arr = np.array([4, 5, 6], dtype=np.int32)
       result = np.concatenate((arr, new_arr), axis=0)
       print(result)
       
       >> [[1 2 3]
           [4 5 6]
           [7 8 9]]
       ```

2. 원소(행,열) 삭제

   * `np.delete()`

     * axis를 기준으로 행과 열을 삭제

     * 만약 axis를 지정하지 않으면 1차원배열로 변환 후 삭제

     * 새로운 배열을 return, 원본변경 없음

       ```python
       import numpy as np
       
       np.random.seed(1)
       arr = np.random.randint(0, 10, (3, 4))
       >> [[5 8 9 5]
        	[0 0 1 7]
        	[6 9 2 4]]
       
       result = np.delete(arr, 1) #1차원 vector로 변환 후, 인덱스(1)삭제
       >> [5 9 5 0 0 1 7 6 9 2 4]
       
       result = np.delete(arr, 1, axis=0) # 행단위로 삭제, 두번째 행 지움
       >> [[5 8 9 5]
        	[6 9 2 4]]
       
       ```

       