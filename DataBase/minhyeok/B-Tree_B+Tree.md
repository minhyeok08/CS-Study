# B-Tree

- B-Tree는 이진 트리에서 발전되어 리프 노드들이 모두 같은 레벨을 가질 수 있도록 자동으로 밸런스를 맞추는 자료구조.

- 정렬된 순서를 보장한다.

- B-트리는 하나의 노드에 여러 개의 정보를 담을 수 있다.

### 규칙

- 노드는 최대 M개 부터 M/2개 까지의 자식을 가질 수 있다.

- 노드에는 최대 M−1개 부터 [M/2]−1개의 키가 포함될 수 있다.

- 노드의 키가 x개라면 자식의 수는 x+1개이다.

- 최소차수는 자식수의 하한값을 의미, 최소차수가 t라면 M=2t−1을 만족. (최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개.)

<br>

<img src="https://velog.velcdn.com/images%2Femplam27%2Fpost%2Fddbae2c9-da94-457d-bad8-77ff6791255b%2FB%ED%8A%B8%EB%A6%AC%20%EA%B8%B0%EB%B3%B8%20%ED%98%95%ED%83%9C.png" width="800" height="300">

### 검색

<img src="https://velog.velcdn.com/images%2Femplam27%2Fpost%2Fb7df8287-2524-4ec0-ad03-b969a8830c8e%2FB%ED%8A%B8%EB%A6%AC%20%EA%B2%80%EC%83%89%201.png" width="800" height="600">

<img src="https://velog.velcdn.com/images%2Femplam27%2Fpost%2Fe20bdef7-e106-4c89-9560-d7f57154dce1%2FB%ED%8A%B8%EB%A6%AC%20%EA%B2%80%EC%83%89%202.png" width="800" height="600">

### 삽입



## 링크

https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Tree



