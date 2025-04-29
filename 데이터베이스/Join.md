항상 헷갈리는 개념이니 `leftjoin`, `innerjoin`을 비교하며 설명하겠다.

- leftjoin
	- left 테이블의 모든 데이터를 보존하면서, 다른 테이블의 컬럼을 이어 붙인다.
	- left 테이블에만 있는 데이터라면 추가된 컬럼은 Nan 처리 된다.
	- right 테이블에만 있는 데이터라면 최종 결과에선 사라진다.
- innerjoin
# LeftJoin
# InnerJoin