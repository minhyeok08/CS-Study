# RDBMS

### RDBMS란?

- RDBMS는 관계형 모델을 기반으로 한 데이터베이스 관리 시스템

- 즉, 서로 연관있는 DB를 관리하는 시스템

- 외래키를 사용하여 연관관계임을 나타냄.

### 특징

- 데이터를 Column과 Row형태로 저장.

- 데이터 분류와, 정렬, 탐색 속도가 상대적으로 빠름.

- SQL 쿼리문을 통해 데이터를 관리.

- 스키마를 통해 데이터의 구조와 제약 조건을 정의.

- 수직적 확장(Scale-up) 
    - 하드웨어 성능을 향상시키는 방법

    - 구현 간단, 기존 어플리케이션 코드를 변경하지 않아도됨
    - 성능향상에 한계
    - 비용이 높음



- MySQL, Oracle, PostgreSQL 등

### 장점

- 규격화된 스키마를 통해 데이터를 저장하기 때문에 명확한 데이터 구조를 보장.

- 각 데이터를 중복없이 저장

### 단점

- 테이블간 관계를 갖고 있기 때문에 SQL 쿼리문에 많은 JOIN이 포함될 수 있음.

- 성능 향상을 위해 Scale-Up만 사용 가능 => 비용 증가

- 정해진 스키마로 인해 데이터의 유연성이 떨어짐

- 확장성이 떨어지며, 대량의 데이터를 처리하는데 있어 비효율적일 수 있습니다.

- 또한, 고정된 스키마를 가지고 있어 유연성이 떨어집니다.

### 사용

- 데이터 구조가 명확하며 변경될 여지가 없으며 명확한 스키마가 중요한 경우

- 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템

<br>

# NOSQL(Not only SQL)

### NOSQL이란?

관계형 모델이 아닌 다른 모델을 사용하는 데이터베이스 관리 시스템

### 등장 배경

데이터가 기하급수적으로 증가함에 따라 Scale-Up 방식의 RDBMS로 이들을 관리하기엔 비용이 많이 들고, 보다 빠른 처리속도가 필요하여 이를 해결하기 위해 등장.

### 특징

- 데이터 간의 관계가 없다.

- 테이블이 독립적이며, 테이블간의 관계를 맺고 있지 않아 JOIN이 불가능.

- 스키마가 없기 때문에 데이터의 추가 삭제가 자유로움.

- Scale-Out 방식으로 서버 확장이 용이.

- 대용량 데이터를 처리하는데 뛰어나다.

- 여러 대의 서버로 구성되어 있어 서버의 에러가 발생하더라도 서비스가 가능.

- 여러 대 서버에 분산하여 데이터를 저장

- 수평적 확장(Scale-Out)
    - 서버 자체를 추가하여 시스템을 확장하는 방법
  
    - 복수의 서버를 통해 처리 능력을 향상
    - 높은 확장성
    - 비용 효율적
    - 어플리케이션 아키텍쳐 변경 필요 가능성
    - 데이터 분산과 동기화 등의 이슈 가능성

### 장점

- 빅 데이터 처리에 효과적

- 자유로운 데이터 구조

- 언제든 저장된 데이터를 조정, 새로운 필드 추가 가능

- 데이터 분산 용이

### 단점

- 데이터 중복 발생 가능, 중복된 데이터가 변경될 경우 모든 컬렉션에서 수정 필요 => 테이블 업데이트시 속도 느림
- 스키마가 없기 때문에 명확한 데이터 구조가 없다
- Key-Value 형태의 NOSQL DB에서 Key 값에 대한 입출력만 지원

### 사용

- 정확한 데이터 구조를 알 수 없고 데이터가 변경/확장이 될 수 있는 경우

- Update가 많이 이루어지지 않는 시스템

- Database를 Scale-out 해야 되는 시스템

<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdnlAgh%2FbtrMDRv02qB%2F9uRKREjBvGrSkok0UBF5x1%2Fimg.png" width="800" height="400">

### NOSQL 종류

## Key-Value DataBase

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcLHLU3%2Fbtrl1KWUzKh%2FqmxrYHWowRdRySXwfff02K%2Fimg.png" width="400" height="300">

- Key와 Value가 한 쌍으로 저장되는 구조

- 속도가 빠르며 분산 저장에 용이

- 액세스 속도는 빠르지만 Scan에 용이하지 않음

- Riak, Redis, Voldmort, Oracle NoSQL Database 등

## Document DataBase

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoZyvF%2FbtrQZPA0Mvb%2FTaLqQJDpZdLDr2qJPIlUUK%2Fimg.png" width="400" height="300">

- 테이블 스키마 유동적

- 레코드마다 다른 스키마 가능

- 데이터 저장시 Key-Value 사용, 보통 XML / JSON 같은 document 형식의 데이터를 레코드에 저장

- 트리형 구조로 레코드를 저장하거나 검색하는데 효과적

- DB 종류 : MongoDB, Couch DB, Azure Cosmos DB

## Wide-Column Database

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FlW9mG%2FbtrQ2RxlJfu%2FGMusAuBNgliLjpCLFShlHK%2Ftfile.svg" width="800" height="300">

- 행마다 키와 해당 값을 저장할 때 각각 다른 값의 다른 수의 스키마를 가질 수 있다.

- Column Family 2 의 Column2의 Row key1에 해당하는 값에 스키마들이 각각 다름(t1,t2,t3)을 확인할 수 있다.

ex) 

    Column Family : 사용자 정보
    Column 2 : 이메일
    Row Key 1 : 사용자 ID
    t1 : 개인 이메일
    t2 : 업무 이메일
    t3 : 기타 이메일

- 대량의 데이터의 압축, 분산처리, 집계 쿼리(Sum, Count, Avg 등) 및 쿼리 속도 우수

- DB 종류 : Hbase, Google BigTable, Vertica

## Graph Database

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdTIk7P%2FbtrQ3Thp4mL%2FFrvV8LFghqHlHjYQhieW81%2Fimg.png" width="400" height="300">

- 데이터를 노드로 표현하며 노드 사이의 관계를 엣지로 표현.

- RDBMS 보다 성능이 좋고 유연하며 유지보수에 용이하다.

- DB 종류 : Neo4j, BlazeGraph, OrientDB, Titan, AllegroGraph
