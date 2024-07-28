## 분류? 얜 비지도학습 아닌가요?

1. 개념

   분류 모델은 학습 데이터의 레이블 중 하나가 결과값이 된다. 즉, 레이블이 지정된 데이터로 학습한 후에 새로 입력된 데이터가 학습했던 그룹 중 어디에 속하는지를 찾아내는 방법이다. 따라서 레이블이 이산적인 경우 주로 사용한다.

   비슷하게 생긴 비지도학습의 고놈은 clustering(군집화) 이다...

2. 종류

   1. K-NN

      K-NN은 K-Nearest Neighbor의 약자로 다양한 레이블의 데이터 중에서 입력값에 대해 가장 가까운 데이터를 찾아 입력값의 레이블을 결정하는 방식이다. 이때, 단순히 ‘가장 가까이 있는게 무엇인가?’ 보다 ‘가장 가깝고 많이 있는 것이 무엇인가?’ 에 더 가까운 방식을 사용한다. 하지만 데이터의 분포는 크게 신경쓰지 않는다.

      ![knn](https://github.com/user-attachments/assets/42ceb22f-60a5-45da-8a2b-f0055d82f078)

   2. 의사결정트리

      의사결정트리(decision trees)는 데이터를 분석하여 이들 사이에 존재하는 패턴을 시각적이고도 명시적인 방법으로 보여주는 학습 알고리즘이다.

      의사결정트리는 node로 구성되며 각 node는 입력값과 연관성을 가진다. 또한 edge(간선)라고 하는 연결선이 각 node 사이를 연결한다. 또한 의사결정트리는 가장 단순한 분류 모델 중 하나이다. 때문에 누구나 쉽게 이해할 수 있다는 장점이 있다.

      ![의사트리](https://github.com/user-attachments/assets/784ebbc6-5f65-4a82-a1ae-35387fdd4e82)

   3. SVM

      SVM은 Support Vector Machine의 약자로, 주로 다루려는 데이터가 2개의 그룹으로 분류될 때 사용한다. SVM은 데이터가 벡터 공간에 위치하고 있다고 가정하고 데이터의 feature 수를 조절함을써 2개의 그룹을 분리하는 decision boundary(경계선)를 지정하고, 이를 기반으로 패턴을 찾아내는 방법이다. 이때 경계선은 모든 그룹과의 margin(거리)이 최대한 멀게끔 하며, 이는 입력값을 분류할 때 정확도를 높이기 위해서이다.

      아래 그림에서는 초록색과 노란색의 점들이 각각의 벡터로 존재하며, 그들이 모여 있는 것을 특징량이라고 한다.

      ![svm](https://github.com/user-attachments/assets/5cb9c9dd-2fe1-4119-b942-be6425afe8b5)

---