### 목표

- Extractive/Abstractive summarization 이해
- Text normalization 적용
- seq2seq 성능을 Up시키는 Attention Mechanism 적용

## Text Summarization(텍스트 요약)

- 요약 전후에 정보 손실 발생이 최소화되어야 함
    - 정보를 압축하는 과정과 같음

**요약 문장을 만들어내는 방법**

- Extractive Summarization (추출적 요약)
- Abstractive Summarization (추상적 요약)

### Extractive Summarization

- 단어 그대로 원문에서 **문장들을 추출**해서 요약
- 딥러닝보다는 주로 전통적인 머신러닝 방식에 속하는 TextRank와 같은 알고리즘을 사용해서 이 방법을 사용

**단점**

결과로 나온 문장들 간의 호응이 자연스럽지 않을 수 있음 

어색하거나 문법적으로 이상한 결과물 (구글 텍스트 요약)

**예시**

네이버 뉴스 서비스 요약봇

### Abstractive Summarization

원몬으로부터 내용이 요약된 **새로운 문장을 생성**

- NLP
- Text Classfication 문제로 볼 수 있음

**RNN의 문제**

- 언급을안해..

## seq2seq

- 두 개의 RNN 아키텍쳐를 사용
- 주로 뉴럴 기계번역에 사용되며 지금은 텍스트 요약으로 사용 (원문을 요약문으로 번역한다)

**과정**

원문 → *인코더* → context vector → *디코더* → 요약 문장

![스크린샷 2021-10-28 오전 10.14.41.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63912299-0738-4eb3-9700-3de7ae2b5653/스크린샷_2021-10-28_오전_10.14.41.png)

- time step 셀에 hidden state 뿐만 아니라 cell state도 전달
    - 인코더가 디코더에 전달하는 컨텍스트 벡터 또한 hidden state `h` 와 cell state `c` 두 개의 값 모두 존재

### 시작 토큰과 종료 토큰

![스크린샷 2021-10-28 오전 10.17.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e7c68a2-779c-4062-8531-3824a00f5408/스크린샷_2021-10-28_오전_10.17.21.png)

- 시작 토큰 <SOS> 가 입력되면, 종료 토큰 <EOS> 예측하는 순간까지 멈추지 않음
- 시작 토큰과 종료 토큰을 넣어주는 전처리를 통해 어디서 멈춰야 하는지 알려줄 필요가 있음

![스크린샷 2021-10-28 오전 10.35.36.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6c8e3373-b58c-4c63-b4fb-6b6c7e6e02ec/스크린샷_2021-10-28_오전_10.35.36.png)

- 기존 seq2seq은 인코더 마지막 time step의 hidden state를 context vector로 사용

**RNN 계열 한계 (RNN, LSTM, GRU)**

context 정보에 이미 입력 시퀀스의 많은 정보가 손실

### 어탠션 메커니즘

- 인코더의 모든 step의 hidden state 정보가 context vector에 전부 반영
- 인코더의 모든 hidden state가 동일한 비중으로 반영되는 것이 아니라, 디코더의 현재 time step의 예측에 인코더의 각 step이 얼마나 영향을 미치는지에 따른 가중합으로 계산

**Conflict**

- 어텐션 모델에서는 디코더의 time step에 따라 컨텍스트 벡터를 구성하기 위한 hidden state의 가중치가 달라짐
    - 디코더의 현재 문장 생성 부위가 주어부인지 술어부인지 목적어인지에 따라 컨텍스트 벡터가 달라짐
- 이와 달리 전통적인 seq2seq 모델에서 컨텍스트 벡터는 디코더의 time step의 무관하게 한번 계산되면 고정값

디코더의 현재 스텝에 따라 **동적으로 달라지는** 인코더의 컨텍스트 벡터를 사용해서 현재의 예측에 활용 → 디코더가 좀 더 정확한 예측

### NLTK

- Natural Language Toolkit. 영어 기호, 통계, 자연어 처리를 위한 라이브러리
- 의미를 분석하고 요약하는 데는 거의 의미가 없는 100여개의 불용어 미리 정리

### Text normalization(텍스트 정규화)

같은 문장 다른 단어로 처리하지 않게하기

- ex) `mustn't`, `must not`

[Expanding English language contractions in Python](https://stackoverflow.com/questions/19790188/expanding-english-language-contractions-in-python)

- 정규화 사전

```python
from tensorflow.keras.layers import Input, LSTM, Embedding, Dense, Concatenate
from tensorflow.keras.models import Model
from tensorflow.keras.callbacks import EarlyStopping, ModelCheckpoint

# 인코더 설계 시작
embedding_dim = 128
hidden_size = 256

# 인코더
encoder_inputs = Input(shape=(text_max_len,))

# 인코더의 임베딩 층
enc_emb = Embedding(src_vocab, embedding_dim)(encoder_inputs)

# 인코더의 LSTM 1
encoder_lstm1 = LSTM(hidden_size, return_sequences=True, return_state=True ,dropout = 0.4, recurrent_dropout = 0.4)
encoder_output1, state_h1, state_c1 = encoder_lstm1(enc_emb)

# 인코더의 LSTM 2
encoder_lstm2 = LSTM(hidden_size, return_sequences=True, return_state=True, dropout=0.4, recurrent_dropout=0.4)
encoder_output2, state_h2, state_c2 = encoder_lstm2(encoder_output1)

# 인코더의 LSTM 3
encoder_lstm3 = LSTM(hidden_size, return_state=True, return_sequences=True, dropout=0.4, recurrent_dropout=0.4)
encoder_outputs, state_h, state_c= encoder_lstm3(encoder_output2)
```

### Hidden state

LSTM에서 얼만큼의 수용력(capacity)를 가질지를 정하는 파라미터

- LSTM의 용량의 크기나,  LSTM에서의 뉴런의 개수

### 3개의 층

hidden state의 크기를 늘리는 것이 LSTM 층 1개의 용량을 늘린다면, 3개의 층을 사용하는 것은 모델의 용량을 늘림.

층을 지나서 인코더로부터 나온 출력 벡터는 디코더로 보내줌

```python
# 디코더 설계
decoder_inputs = Input(shape=(None,))

# 디코더의 임베딩 층
dec_emb_layer = Embedding(tar_vocab, embedding_dim)
dec_emb = dec_emb_layer(decoder_inputs)

# 디코더의 LSTM
decoder_lstm = LSTM(hidden_size, return_sequences=True, return_state=True, dropout=0.4, recurrent_dropout=0.2)
decoder_outputs, _, _ = decoder_lstm(dec_emb, initial_state=[state_h, state_c])
```

### initial_state

인자로 인코더의 hidden state와 cell state값을 넣어주어야함.

### 어텐션 메커니즘

어텐션 메커니즘을 수행하는 어텐션 함수를 설계하는 것은 또 다른 신경망을 설계해야한다는 뜻임

```python
# 어텐션 층(어텐션 함수)
attn_layer = AttentionLayer(name='attention_layer')
# 인코더와 디코더의 모든 time step의 hidden state를 어텐션 층에 전달하고 결과를 리턴
attn_out, attn_states = attn_layer([encoder_outputs, decoder_outputs])

# 어텐션의 결과와 디코더의 hidden state들을 연결
decoder_concat_input = Concatenate(axis=-1, name='concat_layer')([decoder_outputs, attn_out])

# 디코더의 출력층
decoder_softmax_layer = Dense(tar_vocab, activation='softmax')
decoder_softmax_outputs = decoder_softmax_layer(decoder_concat_input)

# 모델 정의
model = Model([encoder_inputs, decoder_inputs], decoder_softmax_outputs)
model.summary()
```

- 인코더의 hidden state들과 디코더의 hidden state들을 어텐션 함수의 입력으로 사용, 어텐션 함수가 리턴한 값을 예측 시에 디코더의 hidden state와 함께 활용

### 프로젝트 할 때 유의할 점

- NLP는 높은 컴퓨팅 자원 필요함. 결과를 개선하기 위한 접근 방안 중 너무 단순한 데이터 정제향 전처리는 지양하자

### Early stopping

[tf.keras.callbacks.EarlyStopping | TensorFlow Core v2.6.0](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/EarlyStopping)

인자로준것 (ex, val_loss)가 정해준 횟수만큼 줄어들지 않으면 epoch이 몇이든 멈춤

### seq2seq

- 훈련할 때와 실제 동작할 때 (인퍼런스 단계)의 방식이 다름
- 훈련 단계에서는 디코더의 입력부에 정답이 되는 문장 전체를 한번에 넣고 디코더의 출력과 한 번에 비교할 수 있으므로, 인코더와 디코더를 엮은 통짜 모델 하나만 준비했음
- 그러나 정답 문장이 없는 인퍼런스 단계에서는 만들어야 할 문장의 길이만큼 디코더가 반복 구조로 동작해야 하기 때문에 부득이하게 인퍼런스를 위한 모델 설계를 별도로 해주어야 함. 이때는 인코더 모델과 디코더 모델을 분리해서 설계

→ 훈련때는 디코더의 출력 길이가 정해져있음 (정답문장) 허나 인퍼런스단계에서는 만들어야 할 문장의 길이를 모르기때문에 별도 설계

## 궁금한 점

❓ 시작 토큰과 종료 토큰을 넣어주는 전처리를 통해 어디서 멈춰야 하는지 알려줄 필요가 있음

❓ seq2seq 모델의 개념 - RNN LSTM 어텐션 메커니즘 등과 상응하는 모델인건지, 그럼 어텐션 메커니즘 seq2seq을 결합한 모델이 되는건지

### initial_state

인자로 인코더의 hidden state와 cell state값을 넣어주어야함

❓ 인코더 마지막 layer hidden state와 cell state를 주어야 하는 건가

### 더 보기

- seq2seq + attention with lstm layers 이해하기