| 참고: https://velog.io/@kida/FM-Factorization-Machine

SVM이 Sparse한 고차원 데이터에 약하자, 해결하기 위해 나온 모델

![[Pasted image 20250425023059.png]]
연속형, 범주형 타입을 모두 사용 가능

# 수식
![[Pasted image 20250425023251.png]]
degree=2는 상호작용을 2개까지만 모델링 하기 위함. (두 변수의 관계만 고려하는 경우)
예로 나이, 성별, 장르 3개의 feature가 있을 때 나이 - 장르, 나이 - 성별 등을 상호작용 시키는 것이다.
degree=2이기 때문에 나이-성별-장르 를 모두 상호작용 하진 않는다.
degree=3으로 올리면 가능하다.

## 학습해야하는 파라미터
W0: bias
W1: 1차 가중치
W2: 2차 가중치

# Q&A (GPT)

이중 시그마의 계산
-> https://chatgpt.com/c/680a6ec9-c0a4-8003-91ab-5a2cc724a6a6
