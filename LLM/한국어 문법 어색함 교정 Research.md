# 문제 정의
sLLM이 생성한 데이터가 어색한지 여부를 판단하는 Metric 있을거라 생각.
이런게 있어야, 한국말을 잘 하는 LLM 학습이 가능했을 것.
이 Metric을 활용해 점수가 낮은 가게 한줄평만 filtering 해서 재추론을 진행하던지 할 수 있을 것.

- ㄴㄻㄹ
	ㅇㄴㄴㅁ니라널
# 방법
1. 한줄평 Task 데이터셋 구축 후 Fine Tuning.
	- 데이터셋을 어떻게 만들거나 활용하는지? -> [한국어 QA 데이터셋](https://korquad.github.io/category/1.0_KOR.html) 참고
	- [여러 NLP Task에 대한 Dataset 모은 Git-한국어포함]([https://github.com/hyunwoongko/nlp-datasets). GLUE, KLUE 주목


[OpenKoLLM Leaderboard](https://huggingface.co/blog/leaderboard-upstage) 에서 쓰는 metric들 존재.






# 궁금한 점

> [!NOTE]
> 텍스트 생성 성능 Test 할 때, Term이 정확히 일치해야만 정답으로 간주하면서 평가하진 않을것. 이 모호성을 가지고 어떻게 Evaluation 하는지?
> 
> Answer
> Question에 대해 Answer을 여러개 배치하고, 모델이 하나라도 맞추면 부분점수를 주는 방식


> [!NOTE]
> 문법 Check를 어떻게 하는지? 이것도 여러 답안중에 부분점수를 주는 방식으로 하는지? 혹은, 이것보다 더 추상적인 Task인 가게 리뷰글 같은 Task(이런걸 Open domain Question이라 하는듯)를 어떻게 평가하는지?
> 
> Answer
> [Evaluating Open-Domain Question Answering in the Era of Large Language Models](https://arxiv.org/abs/2305.06984) 논문 보면 좋을 듯
> 

