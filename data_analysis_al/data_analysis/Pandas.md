# Pandas

* Pandas는 ndarray(NumPy)를 기본 자료구조로 이용
* ndarray > Series > DataFrame



## Series

> 동일한 데이터타입의 복수 개의 성분으로 구성되는 자료구조 (1차원)

* 1차원 배열의 값(values)에 각 값에 대응되는 인덱스(index)를 부여할 수 있는 구조를 가짐
* 인덱스(index), 값(values)으로 구성

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
  from datetime import datetime, timedelta
  
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
      [ int(x) for x in np.random.normal(50, 5, (10,))],
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

* 2차원 리스트를 매개변수로 전달, 행방향 인덱스(index)와 열방향 인덱스(column)가 존재

* 열(columns), 인덱스(index), 값(values)으로 구성

* Series의 집합으로 구성 (각각의 column이 Series)
* 속성
  * `df.shape`
  * `df.size` : 모든 요소의 수
  * `df.ndim`
  * `df.index.name`
  * `df.columns.name`
* 메소드(함수)
  * `display()` : 전체출력
  * `head(n)` : 처음부터 n개의 행만 출력, default = 5
  * `tail(n)` : 끝부터 n개의 행만 출력, default = 5
  * `df['열이름']` : 해당되는 열을 확인
  * `read_csv('파일경로')` : csv 파일 읽기
  * `read_sql(sql, con=conn)` : sql문 읽기
  * `df.describe()` : df 안에 있는 숫자연산이 가능한 column에 한해서 숫자형 데이터의 통계치를 계산
    기본 분석 함수 => count, 평균, 표준편차, 최대, 최소, 사분위
  * `df.info()` : 각 column마다 데이터 타입, 각 데이터의 아이템 개수를 출력
  * `df.drop(column명, axis, inplace)` :  행(row) 혹은 열(column)을 삭제



### DataFrame을 생성하는 방법

* 리스트, 시리즈, 딕셔너리, ndarray, 또다른 DataFrame으로 생성

1. python의 list와 dictionary로 만듬 (key가 column)

   * 리스트로 생성

   ```python
   data = [
       ['1000', 'Steve', 90.72],
       ['1001', 'James', 78.09],
       ['1002', 'Doyeon', 98.43]
   ]
   df = pd.DataFrame(data)
   
   # 생성된 프레임에 열(columns)을 지정
   df = pd.DataFrame(data, columns= ['학번', '이름', '성적'])
   ```

   

   * 딕셔너리로 생성
     * 생성 시, 데이터의 개수가 맞지 않으면 Error발생

   ```python
   import pandas as pd
   
   data = {'names': ['이순신','이산','장금이'],
          'years': [2018,2019,2020],
          'points': [3.5,4.2,2.8]}
   df = pd.DataFrame(data)
   display(df)	# DataFrame을 출력
   ```




* CSV, 텍스트, Excel, SQL, HTML, JSON 등 다양한 데이터파일을 읽고 데이터 프레임을 생성할 수 있음

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
   # Django에서 사용했던 ORM방식도 있음
   sql = 'select btitle, bauthor, bprice from book'
   
   df = pd.read_sql(sql, con=conn)
   display(df)
   ```



4. json 파일을 이용해서 DataFrame을 생성

   ```python
   import numpy as np
   import pandas as pd
   import json
   
   # 일반적인 파일처리 순서: 파일열기 - 파일쓰기 - 파일닫기
   # with구문을 사용하면 resource의 close처리(해제처리)가 자동처리됨
   with open("./data/json/books_column.json", "r", encoding="utf-8") as file:
       dict_books = json.load(file) # json 데이터를 python의 dictionary로 저장
   print(dict_books)
   df = pd.DataFrame(dict_books)
   display(df)    
   ```



5. open api를 이용해서 DataFrame을 생성

   ```python
   # network 연결을 통해서 open api를 호출 - urllib module 필요
   import numpy as np
   import pandas as pd
   import json
   import urllib
   
   # 영화진흥위원회의 일일박스오피스 open api를 호출하여 dataframe 생성
   key = '455939c85db1448ab4485ed5578847d0'
   openapi_url = f'http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key={key}&targetDt=20200909'
   
   load_page = urllib.request.urlopen(openapi_url) # response객체 return 
                                                   # <http.client.HTTPResponse object at 0x00000150F8D28308>
   
   # load_page.read() : json 객체 (object.read())
   # json.loads() : dictionary 추출
   json_page = json.loads(load_page.read())
   
   print(json_page) # 이걸 분석해서 dataframe을 생성
   dict_movie = json_page['boxOfficeResult']['dailyBoxOfficeList']
   df = pd.DataFrame(dict_movie)
   ```

* `json.load()`  vs  `json.loads()`
  * `json.load()` : json파일을 불러와서 Python dictionary로 변환
  * `json.loads()` : json String을 불러와서 Python dictionary로 변환



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

   

   

## DataFrame을 JSON파일로 저장

* 4가지의 서로 다른 형식이 존재함 (columns, records, index, values)
* unicode로 파일을 생성한 후 데이터를 저장해야 한글이 정상처리 됨

```python
import json
df = ... # dataFrame

# 1. columns: df의 column이 json의 key값으로 들어감 {{}}
with open("./data/json/books_columns.json", "w", encoding='utf-8') as file:
    df.to_json(file, force_ascii=False, orient="columns")

# 2. records [{}]
with open("./data/json/books_records.json", "w", encoding='utf-8') as file:
    df.to_json(file, force_ascii=False, orient="records")

# 3. index {{}}
with open("./data/json/books_index.json", "w", encoding='utf-8') as file:
    df.to_json(file, force_ascii=False, orient="index")

# 4. values [[]]
with open("./data/json/books_values.json", "w", encoding='utf-8') as file:
    df.to_json(file, force_ascii=False, orient="values")
```



## Column Indexing

* 컬럼 데이터 추출 - slicing 안됨 

  * `df['컬럼명']` : Series로 return, **View**
  * `df[['컬럼명', '컬럼명']]` : 2개이상의 column(열) 추출, DataFrame으로 return, fancy indexing 사용
  * `df['컬럼명', '컬럼명']`, `df['컬럼명' : '컬럼명']` : Error!! slicing 안됨 

* 컬럼 데이터 변경

  * 1개의 컬럼 변경: 단일값, ndarray, list를 이용해서 수정
  * 2개 이상의 컬럼 변경:  단일값, ndarray, list를 이용해서 수정. 단, Series의 수가 맞아야함

* 새로운 컬럼 추가

  * scalar, ndarray, list, Series를 이용해서 추가
  * 단, Series로 추가 시, index를 매칭시켜야 함.
  * Series vs List
    * Series의 경우 다양한 수의 데이터를 추가할 수 있음.
      : index 기반으로 데이터가 추가되기 때문에
    * List의 경우 원소의 수가 정확하게 맞아야 함.
      : 그렇지 않으면 에러발생

  ```python
  df['나이'] = 30
  df['나이'] = [20, 30, 25, 42] #원소수가 맞아야함
  df['나이'] = pd.Series([20, 30, 25, 42],
                      index=['one', 'two', 'three','four']) # 원소수가 달라도 됨
  ```

  * 연산을 통해서 새로운 컬럼 추가

  ```python
  # 마지막에 '장학생 여부' 라는 column을 추가
  # 만약 학점이 3.0 이상이면 True, 그렇지 않으면 False
  df['장학생여부'] = df['학점'] >= 3.0
  ```

* 컬럼데이터 삭제

  * `drop()` 사용
  * inplace=True => 원본을 지우고, return값 없음
  * inplace=False=> 원본을 보존하고 삭제된 결과를 리턴(DataFrame), default값

  ```python
  # 1개의 컬럼
  new_df = df.drop('학년', axis=1, inplace=False)
  
  # 2개 이상의 컬럼
  new_df = df.drop(['학점', '등급'], axis=1, inplace=False)
  ```

  

## Row Indexing

* `df.loc[]` 사용

  * 숫자 인덱스가 아닌 부여한 인덱스를 사용

  ```python
  df.loc['one']           # 단일 row 추출, Series - indexing
  df.loc['one':'three']   # slicing 가능
  df.loc['three':]        # slicing 가능 
  df.loc['three':-1]      # Error, index 혼합해서 사용 불가
  df.loc[['two', 'five']] # fancy indexing 가능
  ```

  

* `df.iloc[]` 사용

  * 무조건 숫자 인덱스로 사용 ( <class 'pandas.core.indexes.range.RangeIndex'> )