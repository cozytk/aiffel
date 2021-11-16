### 인코더와 디코더

- 인코더에 입력 문장이 들어가고, 디코더는 이에 상응하는 출력 문장을 생성함

<img width="680" alt="스크린샷 2021-11-16 오후 12 01 27" src="https://user-images.githubusercontent.com/59143479/141962779-8916c5b3-9d4c-4596-8d22-2aa9f3837255.png">

### 임베딩 벡터

- 임베딩 벡터와 포지셔널 인코딩의 덧셈
    
    →  임베딩 벡터가 모여 만들어진 문장 벡터 행렬과 포지셔널 인코딩 행렬의 덧셈 연산을 통해 이루어짐
    

$PE_{pos,2i} = sin(pos/10000^{2i/d_{model}})$

$PE_{(pos_,2i+1)} = cos(pos/10000^{2i/d_{model}})$

<img width="570" alt="스크린샷 2021-11-16 오후 12 02 09" src="https://user-images.githubusercontent.com/59143479/141963273-20434aab-4ff2-4515-b954-ef960d61cae8.png">


<img width="363" alt="스크린샷 2021-11-16 오후 12 02 21" src="https://user-images.githubusercontent.com/59143479/141963279-c3a262da-e218-4d1d-b704-43da5d143710.png">


$d_{model}$: 임베딩 벡터의 차원

$pos$: 입력 문장에서의 임베딩 벡터의 위치

$i$: 임베딩 벡터 내의 차원의 인덱스

<img width="436" alt="스크린샷 2021-11-16 오후 12 02 43" src="https://user-images.githubusercontent.com/59143479/141963315-146dc1fa-4422-4561-843e-6d5c6a8ebdd0.png">

### 어텐션 메커니즘

유사도를 구함

- 주어진 Query에 대해 모든 Key와의 유사도를 각각 구함
- 구해낸 이 유사들 Key와 맵핑되어있는 각각의 Value에 반영
- 유사도가 반영된 Value를 모두 더해서 뭉쳐줌

→ Attention Value

### Query, Key, Value

- 단어 (정보를 함축한) 벡터
    - 여기서 단어벡터란 초기 입력으로 사용되었던 임베딩 벡터가 아니고, 트랜스포머의 여러 연산을 거친 후 단어 벡터

![스크린샷 2021-11-16 오후 12.03.50.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b37f4699-03ef-40f6-a523-2cb241942a0e/스크린샷_2021-11-16_오후_12.03.50.png)

### 트랜스포머의 어텐션

- 인코더 셀프 어텐션: 인코더의 입력으로 들어간 문장 내 단어들이 서로 유사도를 구함
- 디코더 셀프 어텐션: 단어를 1개씩 생성하는 디코더가 이미 생성된 앞 단어들과의 유사도를 구함
- 인코더-디코더 셀프 어텐션: 디코더가 잘! 예측하기 위해서 인코더에 입력된 단어들과 유사도를 구함


<img width="390" alt="스크린샷 2021-11-16 오후 12 03 50" src="https://user-images.githubusercontent.com/59143479/141963311-54d00e9e-d114-456d-9397-2be3646d24f6.png">


### 셀프 어텐션

*유사도를 구하는 대상이 다른 문장의 단어가 아니라 현재 문장 내의 단어들이 서로 유사도를 구하는 경우*


<img width="586" alt="스크린샷 2021-11-16 오후 12 04 15" src="https://user-images.githubusercontent.com/59143479/141963307-5f7e37de-bf70-487c-ad15-ae906a25329c.png">

<img width="278" alt="스크린샷 2021-11-16 오후 12 04 45" src="https://user-images.githubusercontent.com/59143479/141963305-f65ed720-2e2e-4bb6-ba9b-71a463dceb84.png">

### Scaled Dot Product Attetion

$Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V$

- Q, K, V는 단어 벡터를 행으로 하는 문장 행렬
- 백터의 내적은 백터의 유사도를 의미
- $d_k$는 스케일링

### 병렬 어텐션 수행

$d_{model} = d_v + num\_heads$

- d_model은 임베딩 차원이자 열의 크기
- 입력된 문장 행렬을 num_heads의 수만큼 쪼개서 어텐션을 수행하고, num_heads의 개수만큼 다시 하나로 concatenate

### 병렬 어텐션 수행의 효과

<img width="421" alt="스크린샷 2021-11-16 오후 12 25 37" src="https://user-images.githubusercontent.com/59143479/141963304-a2506a09-353e-414c-8b8d-13c8292fe4b2.png">


- 각각 다른 관점에서 셀프 어텐션을 수행
- 한 번의 어텐션만 수행했다면 놓칠 수도 있던 정보를 캐치

### 마스킹

*특정 값들을 가려서 실제 연산에 방해가 되지 않도록 하는 기법*

### Padding Masking

- Padding token 이용
    
    ※ Padding : 짧은 문장에 0 넣어주는 것
    
- 패딩 마스킹은 숫자가 0인 위치를 체크
- 어텐션 연산 시 패딩 마스킹을 참고하면 불필요하게 숫자 0을 참고하지 않을 수 있음

### Look-ahead masking

- 자신보다 다음에 나올 단어를 참고하지 않도록 가리는 기법


<img width="716" alt="스크린샷 2021-11-16 오후 1 46 08" src="https://user-images.githubusercontent.com/59143479/141963302-366af8f3-f515-49a0-81e6-5236d064a24d.png">


- Query 단어가 '찾고'라면, 빨간색 영역으로 칠해지기 전인 '찾고'까지만 참고

### 인코더

- Self-Attention & Feed Forward Neural Network
- Self-Attention은 Multi-Head Attention으로 병렬적으로 이루어짐


<img width="668" alt="스크린샷 2021-11-16 오후 2 06 46" src="https://user-images.githubusercontent.com/59143479/141963298-0950438f-e7d7-4cd9-9d49-8cf6e3317d00.png">


- 이렇게 구현한 인코더 층을 Embedding layer와 Positional Encoding을 연결하고, 사용자가 원하는 만큼 인코더 층을 쌓음으로써 트랜스포머의 인코더가 완성
- Layer Normalization(그림 속 Normalize) 에서 각 서브 층 이후의 훈련을 도움

### 디코더


<img width="703" alt="스크린샷 2021-11-16 오후 2 10 22" src="https://user-images.githubusercontent.com/59143479/141963295-c7e5f77a-0749-4e55-9c45-da2658c29d88.png">

- 셀프 어텐션, 인코더-디코더 어텐션, 피드 포워드 신경망
- 인코더-디코더 어텐션은 셀프 어텐션과는 달리, Query가 디커도의 벡터인 반면에 Key와 Value가 인코더의 벡터라는 특징이 있음
- 인코더의 셀프 어텐션과 마찬가지로 디코더의 셀프 어텐션, 인코더-디코더 어텐션 두 개의 어텐션 모두 스케일드 닷 프로덕션 어텐션을 멀티 헤드 어텐션으로 병렬적으로 수행
- 구현한 디코더 층은 임베딩 층과 포지셔널 인코딩을 연결하고, 사용자가 원하는 만큼 디코더 층을 쌓음

### Advice by 이창호 퍼실님

*임베딩을 하는 다양한 방법과 각각의 특징, 의미에 대해 윤곽이 잡히신 상태에서 트랜스포머 모델을 보라*

→ word2vec, GloVe, Elmo 같은 다양한 임베딩에 대한 이해가 선행되어야 수월하게 접근할 수 있음
