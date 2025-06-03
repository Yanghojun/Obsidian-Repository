
참고: https://www.youtube.com/watch?v=o-pZk5R0TZg

# 어디에 쓸 수 있을까?
검색 시스템에서 검색어 Query와 잘 맞는 Item을 추천해주고 싶다!
방법
- Pretrained Embedding으로 Query, Item Description에 대한 embedding을 각각 생성 후 Dot Product를 통해 가장 유사한 Item을 추천한다!

근데 이걸로 충분한가? 그렇지 않다.
- Brand가 얼마나 중요한지
- 여자인지 남자인지
- 어떤 신발인지 등
고려해야 할 정보가 많다!

Pretrained Embedding을 통한 유사도, 브랜드, 성별, 어떤 신발인지 등의 정보를 종합적으로 판단해서 추천할 수 있는 모델 -> **Two Tower Model**

![[Pasted image 20250603182248.png]]

# 모델 구조 참고
![[Pasted image 20250603182531.png]]
                                                     
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

