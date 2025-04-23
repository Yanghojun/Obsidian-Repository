# 모델 구조
![[Pasted image 20250423235711.png]]
- BI - Encoder

![[Pasted image 20250423235912.png]]
- Context Feature[^1]

# 학습
![[Pasted image 20250424003446.png]]
- Contrastive Learning 방식: 비슷한 건 가깝게, 다른건 멀게
	- positive pair: 주문으로 연결된 유저 - 가게
	- negative pair: 배치 내 주문으로 연결되지 않은 유저 - 가게 pair
- In batch 방식: 한 배치 안에 다른 샘플들을 자동으로 음성 샘플 취급



[^1]: 추천 시스템에서의 Context Feature란 **상황**을 알려주는 정보를 뜻함

