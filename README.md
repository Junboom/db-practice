# db-practice

## 1. Query

### Hard Parsing / Soft Parsing

> 쿼리가 들어오면 문법 체크 먼저 실행
>
> 의미(시멘틱) 체크
>
> 파싱(주체 -> 옵티마이저) 결과에 따라 쿼리가 실행 됨
>
> 옵티마이저 성능 최적화가 가장 중요하다.
>
> RBO / CBO
>> 사용자에게 보여지는 방식
>> Rule Base Optimizer: 약속된 규칙을 기반으로 작성함(우선순위 등).
>> Cost Base Optimizer: 통계를 내서 가지고 있음. 유연하다.
>> 데이터가 뭉쳐있을 때 통계에 따라 판단하고 분배함.
>
> 논리 Join
>> inner join과 outer join 모두 결과가 다르다.
>> cross join: 양쪽 테이블 모두.
>> left outer join: 왼쪽 데이터가 모두 나온다.
>
> 물리 Join
>> Nested Loop Join: 단순히 for문 이라고 생각하면 된다. 하나씩 비교해서 찾는다. 주로 OLTP에서 사용. 이미 알고 있기 때문에 하나의 쿼리만 실행하면 됨.
>> Sort Merge Join: 하나씩 비교하는 것이 아니라 한 번에 가지고와서 비교한다.
>> Hash Join: Hash 함수를 사용하여 Hash 값을 미리 만들고, Hash 값에 의해서 찾는 방식. CPU를 많이 쓰지만, 메모리를 많이 쓰지 않는다. 가장 나중에 나왔다.
>> 데이터 내부적으로 데이터를 가져오기 때문에 쿼리에 영향을 주지 않지만, 성능에 영향을 준다.
>
> OLTP / OLAP
>> OLTP: 많은 데이터가 쌓여있을 때 나에 대한 데이터만 처리함(게임, 이커머스 등).
>> OLAP: 전체적인 통계
>
> optimizer가 판단해서 어떤 join을 선택할 지 판단해서 실행된다.
>
> inner (merge) join 등으로 hint를 주어 강제로 물리 join을 사용할 수 있지만, 오류가 발생할 가능성이 있기 때문에 지양하고 있다.
>
> Query 방식
>> *(all)을 사용하는 것도 성능에 영향을 준다. 따라서 자신이 쓸 테이블만 사용.


## 2. Index - 성능

### 성능에 가장 많이 영향을 주는 것은 Index이다.

> B Tree / B+ Tree
>> B+ Tree: 범위 검색을 위한 노드가 추가된 B Tree.
>> B Tree + Leaf => B+ Tree
>> Linked List로 연결되어 있다.
