레이블을 어떻게 만드는가?
	쿼리당 50개 relevant 문서
	HCX-L 모델 (네이버 LLM)으로 list-wise ranking 매김
	논문으로 복잡하게 설명되어 있는데, 이해하려면 시간이 좀 걸릴 것. 코드도 없음

RankNet을 어떻게 활용하는가?
	$s_{base}$로 overall semantic score
	$s_{TCL}$로 용어 특화 score
	Label 구성은 어떻게 한거지?
		HCX-L로 쿼리와 관련있는 50개 문서에 대한 ranking score 매김.
		Q. 이미 ranking score를 매겼는데 이를 ranknet으로 다시 학습시키는 이유는?