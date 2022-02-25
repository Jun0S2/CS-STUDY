# DB Optimizer

대용량 데이터베이스를 처리할 때, 튜닝과 선능 향상에 도움이 된다

SQL을 가장 빠르고 효율적으로 수행하는 처리 경로를 생성해주는 DBMS 내부의 핵심 엔진

## Optimizer

사용자가 요청한 SQL을 다양한 실행 방법들 중에서 최적의 실행 방법을 결정하는 것

옵티마이저가 최적의 실행 방법을 결정하는 방식에 따라 **규칙위반 옵티마이저(RBO, Rule Based Optimizer)** 와 **비용 기반 옵티마이저(CBO, Cost Based Optimizer)**로 구분된다.

** 현재 대부분의 데이터베이스는 비용 기반 옵티마이저만 제공한다

![Untitled](DB%20Optimiz%200c64f/Untitled.png)

이미지 출처 : [https://www.stechstar.com/user/zbxe/study_SQL/45014](https://www.stechstar.com/user/zbxe/study_SQL/45014)

## 규칙 기반 옵티마이저

- Oracle 8 이하의 버전에서 기본으로 설정된 옵티마이저
- **실행 속도가 빠른 순으로 규칙을 먼저 세워두고 우선순위가 앞서는 방법**으로 사용
- 판단 기준이 분명하여 사용자도 계측 가증
- 현실적인 통계 정보를 감안하지 않으면 판단에 오차 발생
- Hash join, partitioned tabled 등 사용 불가

[규칙 기반 옵티마이저의 우선순위](DB%20Optimiz%200c64f/%E1%84%80%E1%85%B2%E1%84%8E%E1%85%B5%E1%86%A8%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A1%204a73c.csv)

## 비용 기반 옵티마이저

- 여러 계획(최대 2천개)에 대한 비용을 산정해보고 그중에서 최소 비용으로 선택
- 판단 기준을 사용자가 미리 예측하기 어려움
- 실제 비용 기반의 정확한 판단
- Oracle 등에서 CBO를 기본으로 채택 (oracle 10이후부터 공식적으로 cbo만 사용)
- 비용 기반 옵티마이저는 여러 모드에 따라 최적의 비용을 구하는 방식이 달라짐

[비용 기반 옵티마이저의 모드](DB%20Optimiz%200c64f/%E1%84%87%E1%85%B5%E1%84%8B%E1%85%AD%E1%86%BC%20%E1%84%80%E1%85%B5%E1%84%87%E1%85%A1%20b8c8d.csv)

** 통계 정보는 DBMS에서 제공하는 통계 정보 사용. 사용자가 수동으로 직접 생성할 수도 있음

## 옵티마이저 동작 방식

![Untitled](DB%20Optimiz%200c64f/Untitled%201.png)

이미지 출처: [http://www.gurubee.net/lecture/2400](http://www.gurubee.net/lecture/2400)

- Parser : SQL문장을 이루는 개별 구성요소를 분석하고 파싱해서 파싱 트리를 만든다.( Syntax(문법), Semantic(의미) )
- Query Transformer : 파싱된 SQL을 좀 더 일반적이고 표준적인 형태로 변환한다.
- Estimator : 오브젝트 및 시스템 통계정보를 이용해 쿼리 수행 각 단계의 선택도, 카디널리티, 비용을 계산하고, 궁극적으로는실행계획 전체에 대한 총비용을 계산해 낸다.
- Plan Generator : 하나의 쿼리를 수행하는데 있어, 후보군이 될만한 실행계획들을 생성해 낸다.
- Row-Source Generator : 옵티마이저가 생성한 실행계획을 SQL 엔진이 실제 실행할 수 있는 코드(또는 프로시저 ) 형태로 포맷팅한다.
- SQL Engine : SQL을 실행한다.

Reference:

 [https://itwiki.kr/w/데이터베이스_옵티마이저](https://itwiki.kr/w/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%98%B5%ED%8B%B0%EB%A7%88%EC%9D%B4%EC%A0%80)

[https://www.stechstar.com/user/zbxe/study_SQL/45014](https://www.stechstar.com/user/zbxe/study_SQL/45014)

[https://coding-factory.tistory.com/743](https://coding-factory.tistory.com/743)

[http://www.gurubee.net/lecture/2400](http://www.gurubee.net/lecture/2400)