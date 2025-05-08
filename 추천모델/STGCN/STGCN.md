[논문리뷰영상](https://www.youtube.com/watch?v=R8s5Kh5eKm8&t=1149s)
[코드](https://github.com/VeritasYin/STGCN_IJCAI-18/tree/master)

Spatio Temporal Graph Convolutional Networks: A Deep Learning Framework for Traffic Forecasting

Spatio Temporal: 시공간

통행량 예측하는 모델.
도로는 graph 형태로 되어있으니 graph 쓴다.
# 데이터 구성
사용 데이터: PeMSD7
PeMSD7
- 노드: 고속도로 센서 228개. (아마 지하철역에 센서가 붙어있는듯)
- 노드간 연결: 실제 도로 간 연결
	- 지하철 역 228개의 lat, lon 이용해서 adjacency matrix 구성
	  ![[Pasted image 20250508105714.png]]
	  도로 간 연결이라기 보단, 거리순으로 (228 * 228) matrix 만든게 이해는 잘 안감.
	  연결을 거리순으로 추상화(?) 시킨듯

![[Pasted image 20250508102513.png]]> recast is crucial for ur- ban traffic control and guidance. Due to the high nonlinearity and complexity of traffic flow, tradi- tional methods cannot satisfy the requirements of mid-and-long term predic
