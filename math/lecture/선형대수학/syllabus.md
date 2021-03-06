# 선형대수 - 이상화(한양대학교)

선형대수는 행렬을 이용하여 선형적인 문제를 해결하는 수학 분야이자, 전기/전자/컴퓨터공학의 원리를 표현하는 핵심적인 이론이다. 
단순히 행렬의 연산만을 다루는 것이 아니라, 공학적인 문제를 행렬의 형태로 정의하고 그 해답을 구하는 과정과 방법을 다루고 있다. 
특히, 전자/컴퓨터 공학에서는 다변수로 이루어진 복잡한 비선형적인 문제를 선형적인 식으로 근사하는 경우가 많은데, 근사화된 선형적인 시스템을 행렬식으로 표현하고 그 해를 구하는 방법을 선형대수에서 중점적으로 다루고 있다. 
선형대수를 통하여 벡터 공간에서의 다변수 문제를 선형적으로 정의하고 해결하는 방법을 배우며, 전자/컴퓨터공학에서 다루는 시스템의 최적으로 설계할 수 있다.



1.	선형성 정의 및 1차 연립방정식의 의미	
: 수학적 선형성을 정의하고, 1차 연립방정식을 행렬과 벡터로 표현하는 방법을 소개한다.	
2.	1차 연립방정식과 가우스소거법	
   : 1차연립방정식의 해를 기하학적 측면에서 소개하고, 가우스 소거법으로 해를 구하는 방법을 설명한다.
3.	LU 분할	
   : 가우스 소거법 과정을 통하여 행렬을 LU 분할할 수 있음을 설명하고, 이 때, 행을 교환하는 과정을 순열행렬로 표현하는 방법을 소개한다.
4.	역행렬과 전치행렬	
   :역행렬의 의미와 성질을 소개하고, 가우스-조단 방법으로 역행렬 구하는 방법을 학습한다.	
5.	벡터공간과 열벡터공간	
   : 벡터공간의 정의 및 의미를 소개하고, 행렬의 열벡터로 이루어진 열벡터 공간을 설명한다.	
6.	영벡터공간과 해집합	
   :영벡터 공간의 개념을 소개하고, 연립방정식에서 무수한 해를 갖는 방정식에서 벡터 해집합을 구하는 방법을 학습한다.	
7.	벡터의 선형독립과 기저벡터	
   : 벡터의 선형독립과 기저벡터에 대한 정의를 소개하고, 기저 벡터를 이용한 벡터 공간을 표현하는 방법을 학습한다.	
8.	벡터공간의 차원과 4가지 부벡터공간	
   : 벡터공간의 차원 개념을 소개하고, 행렬에서 4가지의 부벡터공간 (열벡터, 행벡터, 영벡터, 좌측영벡터공간)을 설명한다.	
9.	선형변환과 행렬	
   :선형변환과 행렬식의 의미를 소개하고, 다항식의 미분과 적분, 좌표의 회전 및 투영변환을 행렬식으로 유도하는 방법을 소개한다.	
10.	벡터의 직교성과 직선투영	
    : 벡터의 내적과 직교성을 정의하고, 4가지 부벡터공간의 직교성을 보여준다. 또한, 직선위로 벡터를 투영하는 투영행렬을 유도한다.
11.	벡터투영과 최소제곱법	
    :최소제곱법 문제를 소개하고, 이를 벡터의 투영으로 이해하여 해를 구하는 방법을 소개한다. 직선을 유추하는 문제를 통하여 예를 들어 본다.	
12.	1차연립방정식 풀이와 직교벡터 구하기	
    : 1차연립방정식의 3가지 경우에 대하여 해를 구하는 방법을 정리하고, 직교벡터를 구하는 Gram-Schmidt orthogonalization 방법을 설명한다.	
13.	일반최소제곱법과 QR 분할	
    :일반화된 최소제곱법을 간단하게 소개하고, 직교기저벡터를 이용한 QR 분할을 유도한다.	
14.	함수 공간	
    : 함수공간 또는 힐버트 공간을 정의하고, 벡터공간처럼 함수를 연산하는 방법을 설명한다. 또한 퓨리에 기저함수를 소개한다.	
15.	행렬의 판별식	
    : 행렬의 판별식을 정의하고, 가장 기본적인 성질을 소개한다.	
16.	판별식의 공식	
    : 행렬의 판별식을 구하는 여러 가지 방법과 공식을 유도한다.	
17.	판별식의 응용	
    :판별식을 이용하여 다양한 수학적 문제를 해결하는 응용사례를 살펴본다. 역행렬, 크래머 법칙, 부피를 판별식 개념으로로부터 유도한다.	
18.	고유값과 고유벡터 및 대각화	
    :행렬에서 고유값과 고유벡터를 정의하고, 행렬을 고유벡터 행렬과 고유값 대각행렬로 분할하는 방법을 유도한다.	
19.	차분방정식과 고유값	
    :차분방정식을 행렬식으로 유도하는 방법을 소개하고, 이를 고유값과 고유벡터로 변환하여 해를 구하는 방법을 설명한다.	
20.	동질최소제곱법의 해와 마르코프 행렬	
    :동질최소제곡법의 해를 고유벡터로 우도한다. 또한 마르코프 행렬을 소개하고, 이를 고유값과 고유벡터로 변환하여 해를 구하는 방법을 설명한다.	
21.	연립미분방정식과 행렬	
    :연립미분방정식을 행렬로 변환하고, 이를 고유값과 고유벡터로 푸는 방법을 소개한다. 아울러 지수함수에서 행렬이 지수에 들어가는 경우를 정의한다.	
22.	복소행렬과 에르미트 행렬	
    :복소수로 이루어진 행렬을 소개하고 에르미트 행렬의 정의 및 성질을 설명한다. 고유벡터의 직교성, 실수 등을 유도한다.	
23.	특이값 분할 (SVD)	
    :SVD 분할을 소개하고, 그 유용성을 설명한다.