# OS 3주차

# 가상 메모리

## 0️⃣ 스와핑 / 메모리 할당

### 스와핑

> 현재 사용되지 않는 프로세스들을 보조기억장치의 일부 영역으로 쫓아내고 그렇게 생긴 빈 공간에 새 프로세스를 적재하는 것
> 

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled.png)

- 프로세스들이 요구하는 메모리 주소 공간의 크기 > 실제 메모리 크기 ⇒ 프로세스 동시 실행 가능!

### 메모리 할당

프로세스는 메모리의 빈 공간에 할당되어야한다!

연속 메모리 할당 방식 3가지 ⇒ 최초적합 / 최적적합 / 최약적합

**최초적합(First-fit)**

운영체제가 메모리 내의 빈 공간을 순서대로 검색하다 적재할 수 있는 공간을 발견하면 그 공간에 프로세스를 배치하는 방식

⇒ 검색 최소화, 빠른 할당 가능

**최적적합(Best-fit)**

운영체제가 빈 공간을 모두 검색해본 뒤, 적재 가능한 가장 작은 공간에 할당하는 방식

**최악적합(Worst-fit)**

운영체제가 빈 공간을 모두 검색해본 뒤, 적재 가능한 가장 큰 공간에 할당하는 방식

<aside>
💡 **외부 단편화 문제로 인해 위 연속 메모리 할당 방식은 비효율적이다!**

</aside>

`**외부 단편화**`
프로세스들이 실행되고 종료되길 반복하며 메모리 사이사이에 빈 공간이 발생하게 되는데, 그 공간들이 다른 프로세스를 할당하기엔 부족한 크기일 경우 메모리가 낭비되는 현상

해결방법 1 ⇒ 메모리 압축

여기저기 흩어져 있는 빈 공간들을 하나로 모으는 방식

프로세스를 적당히 재배치해 흩어져있는 작은 공간들을 하나의 큰 공간으로 만드는 방법

(많은 오버헤드 발생)

해결방법 2 ⇒ 가상메모리 기법, 페이징

현재 운영체제들이 많이 선택하는 방식

## 1️⃣ 가상메모리 / 페이징

### 가상메모리

> 실행하고자 하는 프로그램을 일부만 메모리에 적재해 실제 물리 메모리보다 큰 프로세스를 실행할 수 있게 하는 기술
> 

가상메모리 관리 기법

- 페이징
- 세그멘테이션

### 페이징

> 프로세스의 논리 주소 공간을 페이지라는 일정 단위로 자르고, 메모리의 물리 주소 공간을 프레임이라는 페이지와 동일한 일정한 단위로 자른 뒤, 페이지를 프레임에 할당하는 가상 메모리 기법
> 

** 물리 주소 : 실제 메모리 내의 주소

** 논리 주소 : CPU가 바라보는 주소

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%201.png)

⇒ 연속 메모리 할당 방식에 비하면 조금 더 균일한 크기를 갖게 되어 외부 단편화는 거의 발생하지 않는다! 

**페이징에서의 스와핑** 

메모리에 적재될 필요가 없는 페이지들은 보조기억장치로 ㄱㄱ

실행에 필요한 페이지들은 메모리로 ㄱㄱ

- 페이지 단위의 스왑 인 = 페이지 인
- 페이지 단위의 스왑 아웃 = 페이지 아웃
- 프로세스를 실행하기 위해 모든 페이지가 적재될 필요 X
- 물리 메모리보다 큰 프로세스도 실행 가능

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%202.png)

<aside>
💡 **여기서 또 다른 문제 발생!**

1. 프로세스를 이루는 페이지가 어느 프레임에 적재되어있는지 CPU가 일일이 알기 어려움
2. 프로세스가 메모리에 불연속적으로 배치되어 있다면 CPU입장에서 이를 순차적으로 실행할 수 없음
3. CPU입장에서 다음에 실행할 명령어 위치를 찾기가 어려워짐

그러니까..
**`페이지 테이블`**을 사용하자!

</aside>

**페이지 테이블**

> 물리 주소에 불연속적으로 배치되더라도 논리 주소에는 연속적으로 배치되도록 하는 방법
> 

⇒ 페이지 번호와 프레임 번호를 짝지어 주는 일종의 이정표

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%203.png)

- 프로세스마다 페이지 테이블이 있다
- CPU는 그저 논리 주소를 순차적으로 실행하면 됨 (페이지 테이블에 의해 페이지 - 프레임 짝지어져 있으니 CPU가 바라보는 논리 주소에서 사용되는 페이지대로 쭉 읽기만 하면 되는 것임)

<aside>
💡 이렇듯 우리는 페이징을 통해 외부단편화 문제를 해결할 수 있었지만 **`내부 단편화`** 문제를 가져올 수도 있다

</aside>

**내부 단편화**

> 프로세스 크기가 5이고, 페이지 크기가 2라고 하자. 이때 마지막 페이지의 경우, 절반의 크기가 낭비된다. (2-2-1) 이러한 상황에서 낭비가 발생하는 경우를 내부 단편화라고 한다.
> 

하나의 페이지 크기보다 작은 크기로 발생

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%204.png)

<aside>
💡 그러면 프로세스마다 페이지 테이블을 가진다고 했는데, 어디에 있지?? 어떻게 찾지??

바로 **`PTBR`** 이 도와준다!

</aside>

**PTBR**

> CPU 내의 프로세스 테이블 베이스 레지스터가 각 페이지 테이블이 적재된 주소를 가리킨다
> 

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%205.png)

<aside>
💡 근데 위 사진처럼 페이지 테이블이 메모리에 있으면?
⇒ **메모리 접근 시간 2배!** 
    ( 1. 페이지 테이블 참조 / 2. 페이지 참조)

그니까 **`TLB`**를 사용하자!

</aside>

**TLB**

> 자주 참조하는 페이지 테이블의 일부를 가져와 저장하는 캐시 메모리로, 캐시 메모리에 찾고자하는 페이지 테이블이 있을 때는 메모리에 2번 접근할 필요가 없어진다
> 

<aside>
💡 더 나아가서..
페이지 테이블을 통해 어떻게 주소가 변환되는지

즉, 논리 주소가 어떻게 물리 주소로 변환되는지 알아보자

</aside>

## 2️⃣ 페이징에서의 주소 변환

CPU가 특정 주소에 접근하고자 할 때 어떤 정보가 필요할까?

1. 어떤 페이지/프레임에 접근하고 싶은지
2. 접근하려는 주소가 그 페이지 or 프레임으로부터 얼마나 떨어져 있는지

**페이징 시스템에서의 논리 주소**

- 페이지 번호 : 접근하고자 하는 페이지의 번호
- 변위 : 접근하고자 하는 그 주소가 그 페이지에서 얼만큼 떨어져 있는지에 대한 정보

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%206.png)

**주소 변환**

<페이지 번호, 변위> ➡️ 페이지 테이블 ➡️ <프레임 번호, 변위>

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%207.png)

 ⇒ 1번 프레임 10번지

페이지 테이블에 있는 더 많은 정보

- 페이지 테이블 엔트리(PTE) : 페이지 테이블 각각의 행
- 유효 비트 : 현재 해당 페이지에 접근 가능한지 여부 (0, 1)
    
    만일 유효 비트가 0인 페이지에 접근하려고 한다면?
    → ‘페이지 폴트’라는 인터럽트 발생
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%208.png)
    
- 보호 비트 : 페이지 보호 기능을 위해 존재하는 비트 (0- 읽기 /1 - 읽기, 쓰기)
- 참조 비트 : CPU가 이 페이지에 접근한 적이 있는지 여부 (0, 1)
- 수정 비트 : CPU가 이 페이지에 데이터를 쓴 적이 있는지 여부 (0, 1)

## 3️⃣ 페이지 교체 알고리즘

우리는 기존에 적재된 불필요한 페이지를 선별해 보조기억장치로 내보내고 프로세스들에게 적절한 수의 프레임을 할당해야한다! 

**요구 페이징**

> 처음부터 모든 페이지를 적재하지 않고 필요한 페이지만을 메모리에 적재하는 기법 ⇒ **요구되는 페이지만 적재하기**
> 

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%209.png)

<aside>
💡 요구 페이징 시스템이 안정적으로 작동하려면 해결해야할 문제?
**- 페이지 교체
- 프레임 할당**

</aside>

### 페이지 교체 알고리즘

> 요구 페이징 기법으로 페이지들을 적재하다보면 언젠간 메모리가 가득 차게 된다. 당장 실행에 필요한 페이지를 적재하려면 적재된 페이지를 보조기억장치로 내보내야하는데 이때 어떤 페이지를 내보낼까?? 를 결정하는 것이 **`페이지 교체 알고리즘`**이다
> 

좋은 페이지 교체 알고리즘이란?

⇒ 페이지 폴트가 적어야한다!

`**페이지 참조열**`

CPU가 참조하는 페이지들 중 연속된 페이지를 생략한 페이지열

1. **FIFO 페이지 교체 알고리즘**
    - 가장 단순한 방식
    - 메모리에 가장 먼저 올라온 페이지부터 내쫓는 방식
    - 오래 머물렀으면 나가라!
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2010.png)
    
    <aside>
    💡 프로그램 실행 내내 사용될 페이지는 먼저 적재되었다고 해서 내쫓아선 안 된다! ⇒ FIFO 보완책 등장
    
    </aside>
    
2. **2차 기회 페이지 교체 알고리즘**
    
    기본적으로는 오래 머문 페이지를 내보내는 FIFO알고리즘이지만, 참조 비트에 따라 기회를 한 번 더 주게 된다.
    
    - 참조 비트 1 → 기회 O
        
        참조 비트 0으로 초기화 후 적재 시간을 현재 시간으로 설정
        
    - 참조 비트 0 → 내쫓기
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2011.png)
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2012.png)
    

1. **최적 페이지 교체 알고리즘**
    
    CPU에 의해 참조되는 횟수를 고려하여 앞으로의 사용 빈도가 가장 낮은 페이지를 교체하는 알고리즘
    
    - 자주 사용될 페이지는 오래 메모리에 남아야함
    - 오래 사용되지 않을 페이지는 없어도 됨
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2013.png)
    
    <aside>
    💡 앞서봤던 FIFO에 비해 페이지 폴트가 적게 발생함!
    
    가장 낮은 페이지 폴트율을 보장하지만 앞으로 오랫동안 사용되지 않을 페이지를 예측하는 건 불가능하기 때문에 실제 구현이 어렵다. 따라서, 다른 페이지 교체 알고리즘 성능을 평가하기 위한 하한선으로 간주된다.
    
    </aside>
    
2. **LRU (Least-Recently-Used) 페이지 교체 알고리즘**
    
    가장 오래 사용되지 않은 페이지를 교체하는 알고리즘
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2014.png)
    

## 4️⃣ 프레임 할당

### 스레싱

> 프로세스가 실행되는 시간보다 페이징에 더 많은 시간을 소요하여 성능(CPU 이용률)이 저해되는 문제
> 

각 프로세스가 필요로 하는 최소한의 프레임 수가 보장되지 않았기 때문에 발생한다.

⇒ 각 프로세스가 필요로 하는 최소한의 프레임 수를 파악하고 프로세스들에게 적절한 프레임을 할당해주어야한다!

### 프레임 할당

1. 균등 할당
    - 가장 단순한 할당 방식
    - 모든 프로세스들에게 균등하게 프레임을 할당하는 방식
2. 비례 할당
    - 프로세스의 크기를 고려하는 방식
    - 프로세스 크기에 비례하여 프레임 할당
    - 막상 실행해보면 고려한 것과 다를 수 있음 (결국 프로세스가 필요로 하는 프레임 수는 실행해봐야 알 수 있음
3. 작업 집합 모델
    - 프로세스가 실행하는 과정에서 배분할 프레임 결정
    - CPU가 특정시간 동안 주로 참조한 페이지 개수만큼만 프레임 할당
4. 페이지 폴트 빈도 기반
    - 프로세스가 실행되는 과정에서 배분할 프레임 결정
    - 페이지 폴트율에 상한선과 하한선을 정하고, 그 내부 범위 안에서만 프레임 할당

## 5️⃣ 세그멘테이션

페이지는 프로세스를 일정한 간격으로 자르는 단위였다. 페이징 말고도 기준을 세워서 논리적인 내용 단위인 세그먼트로 자를  수 있는 세그멘테이션 방법도 있다.

### **세그멘테이션**

세그멘테이션은 하나의 프로세스를 세그먼트의 집합이라고 생각한다.

> 세그먼트란?
> 
> 
> **세그먼트는 메모리의 거의 어느 곳에나 위치할 수 있고, 프로그램 실행을 위해 필요한 공간과 데이터를 처리하는 명령어들을 위한 프로그램이나 메모리의 부분**
> 

마찬가지로 쪼개는 개념이지만, 페이지처럼 일정한 단위로 쪼개는 것이 아니라 같은 역할을 하는 논리적인 단위로 쪼개기 때문에 세그먼트들의 크기는 일정하지 않다.

- 메모리에 할당 하는 방법은 페이징과 방법이 같다. 레지스터를 통해서 논리 주소를 물리 주소로 매핑해줌으로써 변경하는 방식이다.
- 페이지 테이블이 있었듯이 세그먼트도 세그먼트 테이블이 있다.
- 주소를 변환하는 방법도 페이징 방법과 같다.
    
    논리 주소는 <세그먼트 번호, 변위 비트>로 이루어진다. 세그먼트 테이블에 논리 주소 값이 들어가면 세그먼트 번호는 세그먼트 테이블의 인덱스 값으로 인식을 하게 됩니다. 세그먼트 번호를 토대로 세그먼트 테이블에 들어가서 시작 위치와 한계 값을 파악하게 된다.
    

# 파일 시스템

파일과 디렉터리를 관리하는 운영체제 내의 프로그램

## 0️⃣ 파일과 디렉터리

### 파일

- 보조기억장치에 저장된 관련 정보의 집합
- 의미 있고 관련 있는 정보를 모은 논리적 단위
- 파일을 실행하기 위한 정보 + 부가 정보 (= 속성, 메타 데이터)
- 파일의 속성
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2015.png)
    
- 파일 연산을 위한 시스템 호출
    
    파일 생성/삭제/열기/닫기/읽기/쓰기 등
    

### 디렉터리

- 윈도우에서는 폴더
- 여러 계층으로 파일 및 폴더를 관리하는 트리 구조 디렉터리
- ‘경로’의 개념을 가짐
    
    파일/디렉터리의 위치, 이름을 특정 지을 수 있는 정보
    
    - 절대 경로 → 루트 디렉터리에서 자기 자신까지 이르는 고유한 경로
    - 상대 경로 → 현재 디렉터리에서 자기 자신까지 이르는 경로
- 디렉터리 연산을 위한 시스템 호출
    
    디렉터리 생성/삭제/열기/닫기/읽기 등
    
- 디렉터리 엔트리
    
    각 엔트리(행)에 담기는 정보
    
    - 디렉터리에 포함된 대상의 이름
    - 그 대상이 보조기억장치 내에 저장된 위치를 유추할 수 있는 정보
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2016.png)
    

## 1️⃣ 파티셔닝과 포매팅

파티셔닝과 포매팅을 통해서 파일과 디렉터리에 접근해 파일시스템을 이용할 수 있게 된다

### 파티셔닝

> 저장 장치의 논리적인 영역을 구획하는 작업
> 
- 파티셔닝에 의해 나눠진 영역들을 파티션이라고 부른다

### 포매팅

> 파일 시스템을 설정해서 어떤 방식으로 파일을 관리할지 결정하고 새로운 데이터를 쓸 준비하는 작업
> 
- 파일 시스템은 포매팅할 때 결정됨
- 파일 시스템에는 여러 종류가 있고, 파티션마다 다른 파일 시스템을 설정 가능
- 포매팅까지 완료하여 파일 시스템을 설정했다면 파일, 디렉터리 생성 가능

## 2️⃣ 파일 할당 방법

- 포매팅까지 끝난 하드 디스크에 파일을 저장하기
- 운영체제는 파일/디렉터리를 블록 단위로 읽고 쓴다
    
    즉, 하나의 파일이 보조기억장치에 저장될 때에는 여러 블록에 걸쳐 저장됨
    
- 파일을 보조기억장치에 할당하는 방법 ⇒ 연속 할당 / 불연속 할당
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2017.png)
    

### 연속 할당

이름 그대로 보조기억장치 내 연속적인 블록에 파일 할당

- 연속된 파일에 접근하기 위해 파일의 첫번째 블록 주소와 블록 단위의 길이만 알면 된다
- 디렉터리 엔트리 : 파일 이름 & 첫번째 블록 주소 & 블록 단위 길이 명시

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2018.png)

<aside>
💡 구현이 단순하지만 **외부 단편화**를 야기할 수 있다
(아래 사진에서 빈 블록이 있지만 길이가 7인 파일은 할당할 수 없음)

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2019.png)

그래서 오늘날 주로 사용되는 건 **불연속 할당**이다

</aside>

### 불연속 할당 (연결 할당)

각 블록의 일부에 다음 블록의 주소를 저장하여 각 블록이 다음 블록을 가리키는 형태로 할당

- 파일을 이루는 데이터 블록을 연결 리스트로 관리
- 불연속 할당의 일종 : 파일이 여러 블록에 흩어져 저장되어도 무방

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2020.png)

블록 오른쪽 위에 -1 표시 → 한 파일의 끝임을 나타냄

<aside>
💡 하지만 여전히 **단점**이 존재한다!
- 반드시 첫 번째 블록부터 하나씩 읽어들여야 해서 접근 속도가 느리다
- 오류 발생 시 해당 블록 이후 블록은 접근이 어렵다

</aside>

### 불연속 할당 (색인 할당)

파일의 모든 블록 주소를 색인 블록이라는 하나의 블록에 모아 관리하는 방식

- 파일 내 임의의 위치에 접근하기 용이
- 색인 블록 안에 어떤 블록을 읽어야 할지 나타나있기 때문에 디렉터리 엔트리는 <파일이름, 색인 블록 주소>로 이루어진다

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2021.png)

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2022.png)

### FAT(File Allocation Table) 파일 시스템

- 연결 할당의 단점을 보완한 연결 할당 기반 파일 시스템
- 각 블록에 포함된 다음 블록 주소를 한데 모아 테이블로 관리
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2023.png)
    
- FAT가 메모리에 캐시될 경우 연결할당의 단점(느린 임의 접근 속도)개선 가능
- 디렉터리 엔트리

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2024.png)

예시) /home/minchul/a.sh 를 읽는 과정 → 9-8-11-13

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2025.png)

### 유닉스 파일 시스템

- 색인 할당 기반 파일 시스템
- 색인 블록 == i-node
    
    파일의 속성 정보와 15개의 블록 주소 저장 가능
    
    ![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2026.png)
    

예시) /home/minchul/a.sh 를 읽는 과정 → 98-12-13

![Untitled](OS%203%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%202fd43f716439412b9a07bcfbe49aa798/Untitled%2027.png)

## 3️⃣ 저널링 파일 시스템

백업 및 복구 능력이 있는 파일 시스템

파일시스템의 변화에 대한 흔적을 남기기 때문에 시스템 손상으로 인해 복구를 진행할 때 그만큼 빠르게 복구 처리를 할 수 있다.

### 저널링이란?

> 스토리지에 데이터를 저장하기 전에 저널 영역에 데이터의 변경 이력을 저장하고, 스토리지 데이터 변경 내역을 저장하는 활동
> 
- 목적 : 스토리지의 장애복구 과정을 빠른 시간에 원활하게 처리할 수 있도록 하기 위함
- 기본적으로 파일시스템은 파일을 실행하기 위한 정보 + 부가 정보 (= 속성, 메타 데이터)로 이루어져있지만, 저널링 파일 시스템에서는 추가적으로 저널링 유무에 따라 저널링 모드 설정이 가능하다.

### 동작방식

사용자가 어떤 내용을 입력 또는 수정하면 그 내용을 바로 하드디스크 드라이브에 저장하는 것이 아닌 해당 작업을 했다라는 내용을 기록한다. 그리고 어떤 이유로 갑자기 비정상적 종료가 될 시 해당 기록을 확인하여 복구할 수 있다.

### 장단점

장점 ⇒ 빠른 복구 가능

단점 ⇒ 파일 시스템을 업데이트할 때마다 로깅에 따른 오버헤드와 I/O 작업이 많아진다

## 4️⃣ 마운트

윈도우 컴퓨터엔 C드라이브가 예외 없이 존재한다. 이러한 디스크는 운영체제와 독립적이다. 디스크를 운영체제와 연결하고, 사용할 수 있도록 하는 걸 `**마운트**`라고 한다.

### 마운트

> 운영체제에 파일 시스템을 연결하는 것. 이를 통해 사용자가 파일 시스템에 존재하는 파일에 엑세스할 수 있게 된다.
> 
- 디스크를 마운트할 때 운영체제는 디스크의 파티션 테이블에서 파일 시스템에 대한 정보를 읽고 마운트 지점을 정한다.
    
    ** 마운트 지점 : C드라이브(윈도우)처럼 디스크를 나타내는 이름
    
    ![https://blog.kakaocdn.net/dn/umHH7/btrSYm4O1er/eEr1kBc4SFgklOq4kPkQu1/img.png](https://blog.kakaocdn.net/dn/umHH7/btrSYm4O1er/eEr1kBc4SFgklOq4kPkQu1/img.png)
    
    리눅스의 파일 시스템들이 특정 디렉토리에 마운트되어 있는 모습
    

윈도우와 맥 OS는 컴퓨터에 연결된 모든 디스크를 자동으로 마운트 한다. 

ex) 윈도우에 USB를 꽂으면 사용자는 따로 마운트 작업을 하지 않아도 알아서 컴퓨터가 이를 감지하고 D, E 등 드라이브로 마운트 해서 사용자가 접근할 수 있음. 

반면 리눅스는 마운트 지점을 직접 구성하거나 마운트 명령어를 이용해 수동으로 디스크를 마운트해야 한다.