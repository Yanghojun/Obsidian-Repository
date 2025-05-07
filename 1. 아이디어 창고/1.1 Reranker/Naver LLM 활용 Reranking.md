레이블을 어떻게 만드는가?
	쿼리당 50개 relevant 문서
	HCX-L 모델 (네이버 LLM)으로 list-wise ranking 매김
	논문으로 복잡하게 설명되어 있는데, 이해하려면 시간이 좀 걸릴 것. 코드도 없음

RankNet을 어떻게 활용하는가?
	**취지: 모델이 질의 - 문서 간 기본적 맥락 파악하면서 질의 토큰과 유사한 토큰에 집중시키기 위함** (https://d2.naver.com/helloworld/0556679)
	$s_{base}$로 overall semantic score
	$s_{TCL}$로 용어 특화 score
	Label 구성은 어떻게 한거지?
		RankNet을 활용한 학습 방법 요약
			1. Query + 후보 답변 N개 생성
			2. LLM을 이용해 후보들에 대해 Pairwise 비교 라벨 생성
				- A문서가 B문서보다 연관도가 높은 문서라면 데이터 구성 -> (A문서, B문서 Label=1), (A문서, B문서, Label=0)
			3. BERT 모델에 입력해서 스코어 생성
				- BERT 모델 입력은 `<CLS>QUERY<SEP>문서 A 정보<SEP>` 과 같은 형식
				- BERT 모델 출력은 Score
			4. RankNetLoss로 학습 (BERT 모델이 생성한 문서 A 스코어, BERT 모델이 생성한 문서 B 스코어가 있을 때 **어떤 문서가 더 높은 순위를 갖게 할지를 학습**)
				- 어떤 문서가 
			5. Cross Entropy Loss로 학습
			6. 학습된 모델로 Rerank 수행
		HCX-L로 쿼리와 관련있는 50개 문서에 대한 ranking score 매김.
		Q. 이미 ranking score를 매겼는데 이를 ranknet으로 다시 학습시키는 이유는?