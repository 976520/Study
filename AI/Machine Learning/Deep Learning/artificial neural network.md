## 잉공싱경망

> ANN(Artificial Neural Network)은 행렬 수학을 모델로 삼아 소프트웨어적으로 인간의 뉴런 구조를 본떠 만든 기계학습 모델로 인공지능을 구현하기 위한 기술 중 한 형태이다.

이름에서 알 수 있듯 생물의 신경망 매커니즘을 본떠 만든 알고리즘이다.

![인공신경망](https://github.com/user-attachments/assets/a7d88944-e430-4459-9d28-8638bfaf6091)

노란색 동그라미로 표현된 것은 neural network의 processing element 역할을 하며 node라고 부른다. 이는 자신에게 input되는 값들과 weight들을 받아서 자신의 activation(활성화) 상태에 따라 하나의 처리 결과를 만들어 전달하는 역할을 한다. 대부분의 경우 각 node는 0부터 1까지의 값을 취하며 이는 그 뉴런의 활성화 정도를 나타낸다. 인간의 신경세포는 input되어 처리된 정보의 강도가 임계값 미만이 되면 비활성화하고, 이상이 되면 활성화하여 그 결과를 ou

node를 용도별로 분리한 단위를 layer(층)이라고 하며, 이러한 layer가 1개 존재하는 신경망을 single layer perceptron(단층 퍼셉트론), 2개 이상 존재하는 신경망을 multi layer perceptron(다층 퍼셉트론)이라고 한다.

최초로 신호를 받는 쪽에 있는 layer는 input layer(입력층)이라고 하고, 최후에 정보를 내보내는 쪽의 layer를 output layer(출력층)이라고 하며, 그 중간에서 성능을 높이기 위해 존재하는 node들로 구성된 layer를 hidden layer(은닉층)이라고 한다. 이는 각각 생물의 신경망에서 수상돌기, 핵, 축삭돌기와 유사하다. 각 node가 신호를 주고 받는 그 연결을 망이라고 한다.

ANN에 어떠한 신호가 주어질 때, 각 node 별로 그 신호에 반응하고, 다음 node에 신호를 전달한다. 이때 신호를 받는 각각의 node들은 자신이 가진 bias에 따라 신호를 거르고 다시 산출하는데, 산출된 신호들의 총합이 인공지능이 전달하는 출력이다.

---
