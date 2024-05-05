# 몽고 DB

- MongoDB는 고성능, 고가용성 및 쉬운 확장성을 제공하는 NoSQL, Document 지향 데이터베이스.

### 특징

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCF1rm%2Fbtsahyt431Y%2Fv4aVy5NGoMP56ViTSs0RbK%2Fimg.png" width="800" height="200">

- 데이터를 배열 및 중첩 Document와 같은 복잡한 데이터 유형을 효율적으로 저장할 수 있는 유연한 JSON과 유사한 형식인 BSON(Binary JSON)으로 저장

#### Document (RDB의 행)

- MongoDB에서의 기본 데이터 단위로 관계형 데이터베이스의 행과 유사합니다.

- document는 BSON 형식에 저장된 필드와 값 쌍으로 구성됩니다.

#### Collection (RDB의 테이블)

- MongoDB의 컬렉션은 Document의 그룹이며 관계형 데이터베이스의 테이블과 유사.

- 컬렉션은 단일 데이터베이스 내에 존재하며 스키마를 강제하지 않으므로 컬렉션 내의 Document는 다른 필드와 구조를 가질 수 있다.

#### Database

- MongoDB 인스턴스는 여러 개의 데이터베이스를 호스트할 수 있으며 각각의 데이터베이스는 컬렉션의 컨테이너로 작용.

- 데이터베이스는 디스크의 별도 파일에 데이터를 저장하며 각 데이터베이스에는 고유한 이름 공간이 있다.

### 사용처

- MongoDB는 웹 응용프로그램과 인터넷 기반을 위해 설계된 데이터베이스 관리 시스템.

- 다양한 웹사이트 및 서비스의 백엔드 소프트웨어로 선택되고 있다.

- eBay, Foursquare, New York Times, Google, Facebook 등 수많은 주요 웹사이트와 서비스에서 사용되고 있다.