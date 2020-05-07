# K-Means Clustering

- k-means 알고리즘은 클러스터링 중에서 가장 유명한 알고리즘.

## 1. 알고리즘 과정
1. 데이터셋에서 k개의 centroids를 임의로 지정
2. 각 데이터들을 가장 가까운 centroids가 속한 그룹에 할당
3. 2번 과정에서 할당된 결과를 바탕으로 centroids를 새롭게 지정
4. 2~3번 과정을 centroids가 더 이상 변하지 않을 때까지 반복
![kmeans](https://i.imgur.com/WL1tIZ4.gif)

## 2. API
```python
class sklearn.cluster.KMeans(
	n_clusters=8, 
	init='k-means++', 
	n_init=10, 
	max_iter=300, 
	tol=0.0001, 
	precompute_distances='auto',
	verbose=0,
	random_state=None,
	copy_x=True,
	n_jobs=None,
	algorithm='auto')
```
*위 값은 defualt*

- **n_cluster : `int`**
	- 군집의 수
- **init : `k-mean++` , `random`**
	- 초기화 방법
	- `k-mean++` : 초기 군집의 k평균 방법으로 지정
	- `random`: 무작위로 지정
- **n_init : `int`**
	- 초기 중심위치 시도 횟수
	- 디폴트는 10이고 10개의 무작위 중심위치 목록 중 가장 좋은 값을 선택
- **max_iter: `int`**
	- 반복 횟수
- **tol : `float`**
	- 군집 수렴 과정에서 관성과 관련하여 상대적 허용 오차 값

## 3. Example
iris 예제 데이터로 진행
```python
from sklearn.datasets import load_iris
from sklearn.cluster import KMeans
import pandas as pd

iris_df = load_iris()
iris_df = pd.DataFrame(data = iris.data,
                       columns = ['sepal_length','sepal_width','petal_length','petal_width'])
```
클러스터링
```python
kmeans = KMeans(n_clusters = 3, 
		init = 'k-means++', 
		max_iter = 300, 
		random_state = 0).fit(iris_df)
```
결과값 저장
```python
iris_df['cluster'] = kmeans.labels_
