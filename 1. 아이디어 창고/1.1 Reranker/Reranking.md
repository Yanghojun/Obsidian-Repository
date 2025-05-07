요새는 Reranking을 어떤 방식으로 하지?
1. 문서를 bert 모델로 임베딩 후 GNN을 활용해 Reranking. 2024 -> https://arxiv.org/abs/2405.18414
2. 네이버 DAN24
	- list-wise

Reranking 알고리즘 -> [참고](https://yjoonjang.medium.com/re-ranker-%EB%AA%A8%EB%8D%B8-%ED%95%99%EC%8A%B5%EC%9D%84-%EC%9C%84%ED%95%9C-%EB%8B%A4%EC%96%91%ED%95%9C-loss%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-feat-learning-to-rank-listnetloss-lambdaloss-1a18b9697efb)	
1. Pointwise Ranking
2. Pairwise Ranking (RankNet)
3. Listwise Ranking (ListNet)
4. ListMLELoss
5. PListMLELoss
6. LambdaLoss
7. RankLLM
