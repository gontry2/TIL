# Pandas

* Pandas는 ndarray(NumPy)를 기본 자료구조로 이용
* ndarray > Series > DataFrame



## Series

> 동일한 데이터타입의 복수 개의 성분으로 구성되는 자료구조 (1차원)

* 속성

  * `values` >> [-1.  4.  5. 99.] ndarray
  * `index` >> RangeIndex(start=0, stop=4, step=1)
  * `dtype` >> float64
  * `name`
  * `index.name`

* indexing, slicing, boolean indexing, fancy indexing, numpy 집계함수 사용 가능

  ```python
  import numpy as np
  import pandas as pd
  from datetime import date, datetime, timedelta
  
  s = pd.Series([1, -8, 5, 10],
               dtype=np.float64,
               index=['a', 'c', 'c','e']) # Series 생성 시 index를 별도로 지정가능(list)
  print(s['c'])         # indexing => 2개가 Series로 return
  print(s[1:3])         # slicing => 2개가 Series로 return
  print(s['c':'e'])     # slicing => 3개가 Series로 return
                        # => 숫자 index/ 문자 index 차이가 존재함
  print(s[ s % 2 == 0]) # boolean indexing => 짝수만 출력
  print(s[[0, 2, 3]])   # fancy indexing
  print(s.sum())        # numpy 집계함수
  
  # A공장의 2020-01-01부터 10일간 생산량을 Series로 저장
  # 생산량은 평균이 50이고 표준편차가 5인 정규분포에서 랜덤하게 생성(정수로 처리)
  start_day = datetime(2020, 1, 1)
  factory_A = pd.Series(
      [ int(x) for x in np.random.normar(50, 5, (10,))],
      index=[start_day+timedelta(days=x) for x in range(10)]
  )
  
  ```

* series `+` series: 인덱스를 기반으로 행렬합, 겹치지 않는 인덱스는 NaN 리턴

*  insert & delete

  ```python
  s = pd.Series([1, 2, 3, 4])
  s[4] = 100
  s = s.drop(2)
  ```

* python의 dictionary로 Series만들 수 있음 (key가 index)

* 숫자 index는 기본으로 사용이 가능



## DataFrame

> 엑셀(Database)에서 Table과 같은 개념 (2차원)

* Series의 집합으로 구성 (각각의 column이 Series)
* 속성
  * `df.shape`
  * `df.size` : 모든 요소의 수
  * `df.ndim`
  * `df.index.name`
  * `df.columns.name`
* 메소드(함수)
  * `display()` : 전체출력
  * `head()` : 처음부터 5개의 행만 출력
  * `tail()` : 끝부터 5개의 행만 출력
  * `read_csv('파일경로')` : csv 파일 읽기
  * `read_sql(sql, con=conn)` : sql문 읽기



### DataFrame을 생성하는 방법

1. python의 dictionary로 만듬 (key가 column)

   * 생성 시, 데이터의 개수가 맞지 않으면 Error발생

   ```python
   import pandas as pd
   
   data = {'names': ['이순신','이산','장금이'],
          'years': [2018,2019,2020],
          'points': [3.5,4.2,2.8]}
   df = pd.DataFrame(data)
   display(df)	# DataFrame을 출력
   ```

   

2. csv 파일을 이용해서 DataFrame을 생성

   ```python
   import pandas as pd
   data = pd.read_csv('./data/student.csv')
   display(data)
   ```

   

3. Database를 이용해서 DataFrame을 생성

   ```python
   # pymysql모듈 설치(python으로 MySQL database를 사용할 수 있도록 도와줌)
   import pymysql.cursors
   import pandas as pd
   
   # pymysql이라는 module을 이용해서 데이터베이스에 연결
   conn = pymysql.connect(host='localhost',
                         user='user',
                         password='password',
                         db='library',
                         charset='utf8')
   
   # db에 접속되면 sql문을 실행시켜서 db로부터 데이터를 가져온다
   sql = 'select btitle, bauthor, bprice from book'
   
   df = pd.read_sql(sql, con=conn)
   display(df)
   ```

   

## MySQL로 DB구축하기

1. MySQL 설치

2. cmd창의 MySQL설치 경로\bin 폴더로 이동 후 `$mysqld` 입력하여 가동

3. 종료를 원하면 다른 cmd창을 키고 bin 폴더로 이동 후 `$mysqladmin -u shutdown` 입력하여 종료

4. root 유저권한으로 mysql 시스템 접속 `$mysql -u root`

   ```bash
   # 5. 새로운 사용자 생성
   mysql> create user data identified by "data";
   
   # 6. database 생성
   mysql> create database library;
   
   # 7. 생성한 데이터베이스(library)에 대한 사용권한을 새롭게 생성한 data 사용자에게 부여
   mysql> grant all privileges on library.* to data;
   
   # 지금까지 작업한 권한부여 작업을 flush
   # grant 테이블을 reload함으로 변경사항을 바로 적용해주는 명령어
   # grant 명령어 사용해서 사용자를 추가하거나 권한을 변경한 경우에는 굳이 실행할 필요는 없음
   mysql> flush privileges;
   
   # 8. 제공받은 파일(_BookTableDump.sql)을 bin 폴더에 저장 후 다음의 명령어 입력
   mysql> mysql -u data -p library <_BookTableDump.sql
   ```

9. 데이터베이스 구축 완료. 

   

   