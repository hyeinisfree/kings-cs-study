# RDBMS VS NoSQL

DB : 일정한 규칙, 혹은 규약을 통해 구조화 되어 저장되는 데이터 모음

DBMS : DB를 제어, 관리하는 통합 시스템

## RDBMS

RDBMS는 관계형 데이터베이스 관리 시스템을 의미합니다. RDB는 관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스

관계형 데이터베이스(RDB)는 구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체

관계를 나타내기 위해 외래 키(foreign key) 사용.

이러한 테이블간의 관계에서 외래 키를 이용한 테이블 간 Join이 가능

구조 : 레코드- 테이블- 데이터 베이스

## NoSQL

Not Only SQL.(SQL계열의 쿼리 언어도 사용 가능하다) 

유연한 데이터모델을 갖춘 고성능 비관계형 데이터베이스 

NoSQL 비용을 고려하여 여러 대의 데이터에 분산하여 저장하는 Scale-Out을 목표로 등장하였습니다.

구조(document) : 도큐먼트 - 컬렉션 -데이터베이스

## cf> Scale-Up vs Scale-Out

<img width="200" alt="scale up" src="https://user-images.githubusercontent.com/46683113/172126209-dce775eb-3d7c-4dad-9ffc-b9cb4b571d58.png">


<img width="200" alt="scale out" src="https://user-images.githubusercontent.com/46683113/172126246-2b469297-5881-470e-9e96-2b54960efe2f.png">


scale-up 은 하나의 서버 능력을 증강하는 것이다 scale-out는 비슷한 장비를 추가해서 확장하는 방식이다. 

## NoSQL의 종류

1. Key-Value Database

- Key-Value Database는 데이터가 Key와 Value의 쌍으로 저장된다. Key는 Value에 접근하기 위한 용도로 사용되며, 값은 어떠한 형태의 데이터라도 담을 수 있다. 심지어는 이미지나 비디오도 가능하다. 또한 간단한 API를 제공하는 만큼 질의의 속도가 굉장히 빠른 편이다.
- 트렌젝션 로깅, 클라우드기반솔루션 밀리초의 응답시간을 필요로하는 부분 (게이밍, 광고기술애플리케이션)
- 대표적인 NoSQL Key-Value Model로는 Redis, Riak, Amazon Dynamo DB 등이 있다.
    - ex > Redis : 인메모리 데이터베이스(주메모리에 저장하는것, 빠르다. / 휘발성이지만 스냅샷으로 저장가능). 기본적인 데이터타입은 문자열 , 최대 512MB저장, set, hash 지원. 채팅시스템, 다른 데이터베이스 앞단에 두어 사용사는 캐싱계층, 단순한 키-값이 필요한 세션정보 관리, 정렬된 셋 자료구조를 이용하느 실시간 순위표 서비스 등에 사용.

2. Document Database

- Documnet Database 데이터는 Key와Document의 형태로 저장된다. Key-Value 모델과 다른 점이라면 Value가 계층적인 형태인 도큐먼트로 저장된다는 것이다. 객체지향에서의 객체와 유사하며, 이들은 하나의 단위로 취급되어 저장된다. 다시 말해 하나의 객체를 여러 개의 테이블에 나눠 저장할 필요가 없어진다는 뜻이다.
- 주요한 특징으로는 객체-관계 매핑이 필요하지 않다. 객체를 Document의 형태로 바로 저장 가능하기 때문이다. 또한 검색에 최적화되어 있는데, 이는 Key-Value 모델의 특징과 동일하다. 단점이라면 사용이 번거롭고 쿼리가 SQL과는 다르다는 점이다. 도큐먼트 모델에서는 질의의 결과가 JSON이나 xml 형태로 출력되기 때문에 그 사용 방법이 RDBMS에서의 질의 결과를 사용하는 방법과 다르다.
- 대표적인 NoSQL Document Model로는 MongoDB, CouthDB 등이 있다.
    - ex > MongoDB : 빅데이터저장, 고가용성, 샤딩, 레플리카셋 지원 다양한 도메인의 db를 기반으로 분석하거나 로깅등을 구현할때 강함. document를 생성할 때마다 유니크한 ObjectID를 생성해 인덱스로 사용.

3. Wide Column Database

- Column-family Model 기반의 Database이며 이전의 모델들이 Key-Value 값을 이용해 필드를 결정했다면, 특이하게도 이 모델은 키에서 필드를 결정한다. 키는 Row(키 값)와 Column-family, Column-name을 가진다. 연관된 데이터들은 같은 Column-family 안에 속해 있으며, 각자의 Column-name을 가진다. 관계형 모델로 설명하자면 어트리뷰트가 계층적인 구조를 가지고 있는 셈이다. 이렇게 저장된 데이터는 하나의 커다란 테이블로 표현이 가능하며, 질의는 Row, Column-family, Column-name을 통해 수행된다.
- 대표적인 NoSQL Column-family Model로는 HBase(Hadoop database), Hypertable 등이 있다.
    
     <img width="1047" alt="Hbase" src="https://user-images.githubusercontent.com/46683113/172126583-5dd10274-8765-4d9f-952e-221a34f0dc59.png">
    
    출처 : [https://www.joinc.co.kr/w/man/12/hadoop/hbase/about](https://www.joinc.co.kr/w/man/12/hadoop/hbase/about)
    

4. Graph Database

- Graph Model Model에서는 데이터를 Node와 Edge, Property와 함께 그래프 구조를 사용하여 데이터를 표현하고 저장하는 Database입니다. 개체와 관계를 그래프 형태로 표현한 것이므로 관계형 모델이라고 할 수 있으며, 데이터 간의 관계가 탐색의 키일 경우에 적합하다. 페이스북이나 트위터 같은 소셜 네트워크에서(내 친구의 친구를 찾는 질의 등) 적합하고, 연관된 데이터를 추천해주는 추천 엔진이나 패턴 인식 등의 데이터베이스로도 적합하다.
- 노드(node): 추적 대상이 되는 사람, 기업, 계정 등 의 실체를 대표한다. 관계형 데이터베이스의 레코드, 관계, 로우, 도큐먼트 데이터베이스의 도큐먼트와 개념이 거의 동등하다.
- 엣지(edge): 그래프(graph)나 관계(relationship)이라고도 하며 노드를 다른 노드에 연결하는 선이며 관계를 표현한다.
- 프로퍼티(property): 노드의 정보와 밀접한 관련이 있다. 이를테면 위키백과가 노드 중에 하나라면 위키백과의 어떠한 관점이 주어진 데이터베이스에 밀접한 관련이 있느냐에 따라 웹사이트, 참고 문헌, w로 시작하는 낱말과 같은 프로퍼티에 묶여있을 수 있다.
- 대표적인 NoSQL Graph Model로는 Neo4J가 있다.
    
<img width="632" alt="graph model" src="https://user-images.githubusercontent.com/46683113/172126701-0069bc03-952c-4067-b7b4-781f09b0218f.png">

<img width="650" alt="비교" src="https://user-images.githubusercontent.com/46683113/172126959-cb3b801e-01dc-49c1-96f9-92c429237e3c.png">


출처 :  

희진쓰의 서버 사이드 기술 블로그 ([https://khj93.tistory.com/entry/Database-RDBMS와-NOSQL-차이점](https://khj93.tistory.com/entry/Database-RDBMS%EC%99%80-NOSQL-%EC%B0%A8%EC%9D%B4%EC%A0%90))

그래픽 데이터베이스란 ([https://wikidocs.net/50716](https://wikidocs.net/50716))