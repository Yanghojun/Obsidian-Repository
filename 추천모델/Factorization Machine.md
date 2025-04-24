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
## 시그마 기호 해석

![[Pasted image 20250425024242.png]]

이건 아래와 같은 반복을 의미해:

- 먼저 i=1i = 1i=1
    
    - j=2j = 2j=2 부터 nnn까지
        
- 그다음 i=2i = 2i=2
    
    - j=3j = 3j=3 부터 nnn까지
        
- ...
    
- 마지막은 i=n−1i = n-1i=n−1
    
    - j=nj = nj=n
        

즉, **모든 i<ji < ji<j인 조합**을 한 번씩 다 계산하는 거야.

---

## ✅ 예시로 계산해보자 (n = 3)
![[Pasted image 20250425024254.png]]

계산 순서:

- i=1i = 1i=1: j=2,3j = 2, 3j=2,3
    
- i=2i = 2i=2: j=3j = 3j=3
    
- i=3i = 3i=3: j=4j = 4j=4 이상이 없으니 생략
    

그러면 총 계산은:

⟨v1,v2⟩x1x2+⟨v1,v3⟩x1x3+⟨v2,v3⟩x2x3\langle \mathbf{v}_1, \mathbf{v}_2 \rangle x_1 x_2 + \langle \mathbf{v}_1, \mathbf{v}_3 \rangle x_1 x_3 + \langle \mathbf{v}_2, \mathbf{v}_3 \rangle x_2 x_3⟨v1​,v2​⟩x1​x2​+⟨v1​,v3​⟩x1​x3​+⟨v2​,v3​⟩x2​x3​

---

## ✅ 왜 이렇게 계산하냐?

- 모든 **feature 쌍 (i ≠ j)**에 대해 상호작용을 고려하되,
    
- (i,j)(i, j)(i,j)와 (j,i)(j, i)(j,i)는 중복이므로 **한 번만 계산**하려고 이렇게 씀
    
- 그래서 j=i+1j = i+1j=i+1 부터 시작하는 거야
    

---

## ✅ 코드로 표현하면?

```python
for i in range(n):
	for j in range(i + 1, n):
		interaction += dot(v[i], v[j]) * x[i] * x[j]`
```

