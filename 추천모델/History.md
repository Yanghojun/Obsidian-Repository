# Graph Collaborative Filtering Models for Recommendations
2017 GC-MC: Graph 기반 AutoEncoder로 숨겨진 user - item interaction을 찾아냄
2018 PinSage: GraphSage를 이용해서 좋은 추천 결과를 만듦
2019 NGCF: 협업 시그널과 모델간 수식화를 High order connectivities by message-passing 으로 진행
2020 LightGCN: 높은 성능 유지하며, 연산 경량화

그러나 아직도 이웃 정보가 너무 많아서 explosion 되는 문제 해결중. (출처. 2024 Linear-Time Graph Neural Networks for Scalable Recommendations)
이것때문에 GNN 기반 추천 시스템이 challenge 상태.


# GHRS: Graph-based Hybrid Recommendation System with
- CF 기반 연구는 user - item interaction에 집중하기에 cold start에 약함
- CBF (content based filtering)으로 user, item information을 활용해야함
- CF, CBF를 결합한 Hybrid 방식 사용
	- ![[Pasted image 20250514173100.png]]
	  user-item 연결로 뽑은 Feature, user side information(성별 같은)을 concat. (combined Features 확인)
