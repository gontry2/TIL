# 선형대수학(linear algebra)

> 행렬과 벡터를 배우는 수학의 한 분야
>
> 덧셈과 상수곱 구조를 갖고있는 벡터공간과 그 위에 정의되고 벡터공간의 연산 구조를 보존하는 함수인 선형사상에 관한 학문

* 선형대수는 어떤 함수(function, mapping, operator, transformation)가 **선형**함수일 때 그 함수의 성질을 배우는 것이다.
* 선형은 다음 두 식으로 정의한다
  * f(kp) = kf(p)
  * f(p+q) = f(p)+f(q)
* 정비례함수( y = ax ), 미분, 적분
* 비선형함수: 이차함수, 삼각함수, 로그함수, 지수함수 등
* 선형대수의 핵심: 고유값, 고유벡터, 닮음변환



### 선형대수학을 배우면?

* 방대한 양의 데이터나 복잡한 시스템을 비교적 간단하게 표현하고,

* 최소한의 타이핑으로 컴퓨터 계산이 가능해진다

* 왜냐면 선형대수학은 연립방정식을 손쉽게 풀기위해 생겨난 것이기 때문이다.

* 선형대수학 공부를 마치고나면 아래와 같은 능력치를 얻게된다.

  * 연립일차방정식을 행렬을 이용하여 풀 수 있음
  * 행렬식과 역행렬을 구할 수 있음
  * 벡터공간의 성질과 예를 알 수 있음
  * 어떤 함수가 선형변환인지 아닌지를 구분할 수 있음
  * 행렬의 고유값을 구하여 행렬을 대각화할 수 있음

  

## 벡터의 기초

### 1. 벡터: 수의 순서쌍

> 벡터란 크기와 방향을 가진 양, 순서가 정해져 있음 ( 집합과 다름 )

* 한 개의 수로 이루어진 순서쌍: 1차원 벡터 = 스칼라(실수, 크기만 갖고 방향은 없는 양)
* 두 개의 수로 이루어진 순서쌍: 2차원 벡터
* 세 개의 수로 이루어진 순서쌍: 3차원 벡터
* 각각의 수: 벡터의 `성분`

### 2. 벡터의 상등

* 두 벡터가 서로 같다 = 각각의 성분이 같다
* = 순서, 차원이 같다



## 벡터의 기본연산 (합, 실수배, 내적)

### 3. 벡터의 덧셈(뺄셈)

* 차원이 같은 벡터끼리만 가능하다

* 영벡터(모든 성분이 0)는 벡터의 덧셈에 대한 항등원이다

* 벡터의 덧셈의 속성

  * 교환법칙
  * 결합법칙
  * 덧셈의 항등원 영벡터 존재
  * a의 덧셈에 대한 역원 -a이 존재

  

* 항등원: 임의의 연산에서, 어떤 수에 대하여 연산을 한 결과가 처음의 수와 같도록 만들어 주는 수. 예를 들어 a+0=0+a=a가 되도록 하는 0은 덧셈에 대한 항등원이고, *aㆍ1＝1ㆍa＝a*가 되도록 하는 *1*은 곱셈에 대한 항등원이다.

* 역원: 두 원소를 연산한 결과가 단위 원소일 때, 한편에 대하여 다른 편을 이르는 말. *a+b=b+a=0*이면 *b*는 *a*의 덧셈에 대한 역원이고, *a×b=b×a=1*이면 *b*는 *a*의 곱셈에 대한 역원이다.

### 4. 벡터의 실수배(스칼라배)

* 벡터의 모든 성분에 같은 수를 곱하는 것
* 벡터의 실수배의 속성
  * 0과 임의의 벡터와의 곱은 영벡터
  * 임의의 실수와 영벡터와의 곱은 영벡터
  * 1은 벡터의 실수배의 항등원
  * -1과 주어진 벡터와의 곱은 그 벡터의 역벡터(덧셈의 역원)
  * 벡터의 실수배와 벡터의 덧셈에 대한 분배법칙
  * 실수의 합과 벡터의 실수베에 대한 분배법칙
  * 실수의 곱과 벡터의 실수배에 대한 결합법칙

### 5. 벡터의 내적(Inner product, 스칼라곱, scalar product)

* 벡터에서 서로 대응하는 성분끼리 곱한 다음, 그것들을 모두 더한 것 ( 벡터 X 벡터 )
* 벡터의 내적의 결과물은 벡터가 아닌 스칼라이다
* 서로 다른 차원의 벡터끼리는 계산할 수 없다
* 벡터의 크기: 자기 자신과의 내적의 제곱근(유클리드 거리)
* **직교(orthogonal)** : 영벡터가 아닌 두 벡터의 내적이 0 (각도가 90도)
* 내적의 속성(성질)
  * 자기 자신과의 내적은 그 벡터의 크기의 제곱과 같다
  * 자기 자신과의 내적은 언제나 0 또는 양의 실수
  * 자기 자신과의 내적이 0이면, 그 벡터는 영벡터
  * 벡터의 내적의 교환법칙
  * 벡터의 내적과 벡터의 덧셈에 대한 분배법칙
  * 벡터의 실수배와 내적에 대한 결합법칙
  * 두 벡터의 내적이 0이면 직교하거나 두 벡터의 크기의 곱이 0
  * 내적의 또다른 정의 (|a||b|cos(각도))



## 벡터와 수학의 다른 영역과의 관계

### 6. 벡터와 좌표

* 벡터의 표현법과 좌표의 표현법이 같다

### 7. 벡터와 복소수

* 복소수의 덧셈, 뺄셈, 실수배는 2차원 벡터의 그것과 같다
* 복소수의 곱셈은 벡터의 내적과는 다른연산이다
* 2차원 벡터는 좌표평면 위의 한 점 = 복소평면 위의 한 복소수

### 8. 벡터와 함수

* 함수를 벡터로 표현할 수 있다
* 이차함수의 덧셈과 3차원 벡터의 덧셈은 똑같은 연산
* **동형(isomorphic)**, **동형사상(isomorphism)**





### 9. 벡터의 노름(norm)

* 벡터의 크기 = 이동거리 = 노름(norm)

* L1 노름과 L2 노름이 있다

  ​	![image-20200903134836394](C:\Users\user\Desktop\룰루\공부\TIL\math\image-20200903134836394.png)

  

* 가장 가까운 거리를 계산할 때는 **유클리드 거리**, 네비게이션과 같이 도로를 이동해서 최단거리를 계산할 때는 **맨하튼 거리**를 사용하면 된다.
* 아래의 그림에서 녹색만 유클리드 거리이다

![image-20200903135014956](C:\Users\user\Desktop\룰루\공부\TIL\math\image-20200903135014956.png)

* L2 Norm (유클리드 노름)

  * 두 개의 데이터가 얼마나 유사한지를 판단하는 하나의 기준이 된다 (거리)

  ![image-20200903135743408](C:\Users\user\Desktop\룰루\공부\TIL\math\image-20200903135743408.png)

  * **코사인유사도**: 거리가 아닌 패턴, 방향의 유사도를 판단할 때 사용한다

    * 두 벡터가 이루는 각

    * 코사인 유사도는 -1 이상 1 이하의 값을 가진다.

    * 두 벡터의 방향이 완전히 같다면 1, 완전히 반대라면 -1, 서로 독립적인 경우 0

      ![image-20200903140621626](C:\Users\user\Desktop\룰루\공부\TIL\math\image-20200903140621626.png)



## +) word2vec

> 단어를 벡터처럼 다루는 방법
>
> 맥락으로 단어를 예측하거나 단어로 맥락을 예측하는 문제를 마치 지도학습처럼 푸는 것(실제로는 비지도학습)

* 텍스트로 벡터로 전환해야 알고리즘에 넣고 계산할 수 있다.

* 텍스트의 데이터 표현방식 중에 dense representation이 있다. (<-> sparse representation)

  * 우리가 정한 개수의 차원으로 대상을 대응시켜서 표현하는 방식
  * 단어의 의미를 최대한 담는 벡터를 만들려는 알고리즘
  * 대응(임베딩)하는 방식은 머신러닝을 통해 학습한다
  * word2vec는 이 값들을 학습하는 방법론 중에 하나이다.

  