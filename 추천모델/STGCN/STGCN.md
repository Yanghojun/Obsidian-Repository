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
	  도로를 기준으로 1, 0 으로 연결시켜놓고, 거리로 weight를 준 걸로 받아들여야 할 듯.

![[Pasted image 20250508102513.png]]
위 그림에서 SVM, ARIMA 같은 모델은 왼쪽 테이블 데이터(각 센서 별 time 정보) 사용하는것.
본 모델은 Graph 기반 모델이기에 각 센서가 연결된 **spatial 정보**도 사용.
# 모델 해석
![[Pasted image 20250508111756.png]]
- Spatial Graph-Conv: 일반적인 GCN -> 노드 feature에 대한 representation을 만드는 Weight를 얻는다!
	- Node feature, Adjacency matrix 를 입력으로 받아서 연산 진행
	  예시코드
```python
import torch
import torch.nn.functional as F
from torch_geometric.nn import GCNConv
from torch_geometric.data import Data

# 예시 데이터 생성
# 노드 수
num_nodes = 4
# feature 수
num_features = 2

# 노드 특징 행렬 (4개의 노드, 2개의 특징)
node_features = torch.tensor([[1, 2], 
                              [2, 3], 
                              [3, 4], 
                              [4, 5]], dtype=torch.float)

# 인접 행렬 (예: 4개의 노드 간의 연결)
adjacency_matrix = torch.tensor([[0, 1, 1, 0], 
                                  [1, 0, 1, 1], 
                                  [1, 1, 0, 1], 
                                  [0, 1, 1, 0]], dtype=torch.float)

# 데이터 객체 생성
edge_index = adjacency_matrix.nonzero(as_tuple=True)
data = Data(x=node_features, edge_index=edge_index)

# 그래프 컨볼루션 신경망 클래스 정의
class GCN(torch.nn.Module):
    def __init__(self):
        super(GCN, self).__init__()
        self.conv1 = GCNConv(num_features, 4)  # 첫 번째 그래프 컨볼루션 레이어
        self.conv2 = GCNConv(4, 2)              # 두 번째 그래프 컨볼루션 레이어

    def forward(self, data):
        x, edge_index = data.x, data.edge_index
        x = self.conv1(x, edge_index)
        x = F.relu(x)
        x = self.conv2(x, edge_index)
        return x

# 모델 초기화 및 데이터 통과
model = GCN()
output = model(data)

print("Output features:", output)
```

- Temporal Gated-Conv: Time 정보를 shrink 하는 Layer
	- 1D Conv 개념
		- 3가지 값을 측정하는 3차원 dim, 하루에 24번 측정해서 (3, 24) 형태의 matrix
		  k=3, channel=32인 1D Conv 적용을 적용하고 싶다고 하자.
		  Time Shrink를 해야하므로 값에 대한 차원은 축소되지 않게 한다.
		  1D Conv를 시간축으로 sliding 시킨다.
		  [[인스톨 파이토치#1D Conv]] 참고
	- 출력 Tensor
	  이 Layer를 통과하면 $R^{M(time) \times n(sensor) \times feature}$ 인 Tensor가 나옴.![[Pasted image 20250509134235.png]]
	  각 센서 별로 Time shrink된 feature vector를 갖게 된다.
	  1D Conv를 위 그림예시대로 적용해보면 `in_channels` = 4, `out_channels` = 3 으로 적용한것.
	  
	  **N 센서 수는 그대로인 점을 주목**
	  
	  ![[Pasted image 20250509134812.png]]
	  이제 위 그림처럼 센서축을 Time 축으로 변경하면, 센서 별 feature vector를 볼 수 있다.
	  **이게 GCN의 Node Feature가 됀다!**
	  

자 이제 ST-Conv Block의 전체 과정을 보자.
1. Temporal Gated Conv: Time shrink 된 feature vector를 얻는다.
![[Pasted image 20250509134235.png]]
![[Pasted image 20250509134812.png]]
2. 각 센서의 feature vector를 node feature로 설정하고 GCN을 태운다.
   각 time 시점에서의 GCN은 모두 동일한 layer를 사용했다고 함.
   이미 time shrink는 1. 과정에서 진행해서 그런 것 같음.
   ![[Pasted image 20250509135755.png]]