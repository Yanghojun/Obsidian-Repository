| 참고: https://velog.io/@kida/FM-Factorization-Machine

SVM이 Sparse한 고차원 데이터에 약하자, 해결하기 위해 나온 모델

![[Pasted image 20250425023059.png]]
연속형, 범주형 타입을 모두 사용 가능

# 수식
![[Pasted image 20250425023251.png]]
## 수식 설명
$w_0$: 스칼라
$w$: $[w_1, w_2, w_3, ... , w_n]$ 로 이루어진 벡터
$i$: feature index. 예로 i=0이면 USER 원핫인코딩 벡터 중 A 관련한 스칼라 값
$\sum^{n}_{i=1}w_ix_i$: `nn.Linear`로 구현되는 선형결합
$V \in R^{n \times k}$: n x k matrix. element인 **v는 $R^k$ 벡터임**.
- $v \in R^{k}$: 임베딩 벡터





degree=2는 상호작용을 2개까지만 모델링 하기 위함. (두 변수의 관계만 고려하는 경우)
예로 나이, 성별, 장르 3개의 feature가 있을 때 나이 - 장르, 나이 - 성별 등을 상호작용 시키는 것이다.
degree=2이기 때문에 나이-성별-장르 를 모두 상호작용 하진 않는다.
degree=3으로 올리면 가능하다.


> [!NOTE] $x_i$, $x_j$는 스칼라인가 벡터인가?
> 스칼라일 것.
> 수식은 데이터 샘플 1개에 대해 적는것이 일반적임
> 그러니 $X$는 데이터 1개인 입력 `벡터`
> $x_i$는 벡터에 대한 element이므로 `스칼라`



## 학습해야하는 파라미터
W0: bias
W1: 1차 가중치
W2: 2차 가중치

# Q&A (GPT)

이중 시그마의 계산
-> https://chatgpt.com/c/680a6ec9-c0a4-8003-91ab-5a2cc724a6a6
