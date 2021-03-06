# 알게된 것

### 시퀀스

나열된 데이터

### RNN(순환신경망)

output을 input으로 다시 사용

### 언어모델

n-1개의 단어 시퀀스가 주어졌을 때, n번째 단어로 무엇이 올지 예측하는 확률 모델

# 궁금한 것

# 하이퍼파라미터 튜닝기

1. num_words = 20000, BATCH_SIZE = 64, embedding_size = 512, hidden_size = 1024 `
    
    ![스크린샷 2021-10-10 오후 6.01.05.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d08b629d-dfe2-4b2a-bc66-ed590870f5df/스크린샷_2021-10-10_오후_6.01.05.png)
    

1. num_words = 20000, BATCH_SIZE = 64, embedding_size = 512, hidden_size = 1024 `

```
Epoch 1/10
1950/1950 [==============================] - 779s 398ms/step - loss: 3.5208 - val_loss: 2.8165
Epoch 2/10
1950/1950 [==============================] - 778s 399ms/step - loss: 2.6247 - val_loss: 2.5413
Epoch 3/10
1950/1950 [==============================] - 779s 399ms/step - loss: 2.1381 - val_loss: 2.3609
Epoch 4/10
1950/1950 [==============================] - 778s 399ms/step - loss: 1.7189 - val_loss: 2.2674
Epoch 5/10
1950/1950 [==============================] - 778s 399ms/step - loss: 1.4010 - val_loss: 2.2427
Epoch 6/10
1950/1950 [==============================] - 778s 399ms/step - loss: 1.2054 - val_loss: 2.2708
Epoch 7/10
 503/1950 [======>.......................] - ETA: 8:55 - loss: 1.0710 
```

수치를 다들 확 줄여보자

1, num_words 20000, BATCH 64, embedding 64, hidden 512

→ 10,000,000 param

1, num_words 12000, BATCH 64, embedding 1024, hidden 2048, LSTM2 dropout

```
Epoch 1/10
1976/1976 [==============================] - 752s 379ms/step - loss: 3.3360 - val_loss: 2.7342
Epoch 2/10
1976/1976 [==============================] - 747s 378ms/step - loss: 2.5861 - val_loss: 2.4951
Epoch 3/10
1976/1976 [==============================] - 748s 379ms/step - loss: 2.2059 - val_loss: 2.3509
Epoch 4/10
1976/1976 [==============================] - 743s 376ms/step - loss: 1.8995 - val_loss: 2.2674
Epoch 5/10
1976/1976 [==============================] - 735s 372ms/step - loss: 1.6632 - val_loss: 2.2271
Epoch 6/10
1976/1976 [==============================] - 736s 372ms/step - loss: 1.4918 - val_loss: 2.2178
Epoch 7/10
1976/1976 [==============================] - 750s 379ms/step - loss: 1.3648 - val_loss: 2.2288
Epoch 8/10
1976/1976 [==============================] - 746s 378ms/step - loss: 1.2786 - val_loss: 2.2494
Epoch 9/10
1976/1976 [==============================] - 747s 378ms/step - loss: 1.2135 - val_loss: 2.2781
Epoch 10/10
1976/1976 [==============================] - 747s 378ms/step - loss: 1.1698 - val_loss: 2.3055
```

1, num_words 12000, BATCH 64, embedding 512, hidden 2048, 2 dropout

```python
	Epoch 1/10
1976/1976 [==============================] - 619s 312ms/step - loss: 3.3704 - val_loss: 2.7712
Epoch 2/10
1976/1976 [==============================] - 617s 312ms/step - loss: 2.6300 - val_loss: 2.5314
Epoch 3/10
1976/1976 [==============================] - 616s 312ms/step - loss: 2.2502 - val_loss: 2.3787
Epoch 4/10
1976/1976 [==============================] - 616s 312ms/step - loss: 1.9316 - val_loss: 2.2884
Epoch 5/10
1976/1976 [==============================] - 617s 312ms/step - loss: 1.6847 - val_loss: 2.2451
Epoch 6/10
1976/1976 [==============================] - 615s 311ms/step - loss: 1.5025 - val_loss: 2.2328
Epoch 7/10
1976/1976 [==============================] - 616s 312ms/step - loss: 1.3727 - val_loss: 2.2418
Epoch 8/10
1976/1976 [==============================] - 616s 312ms/step - loss: 1.2794 - val_loss: 2.2618
Epoch 9/10
1976/1976 [==============================] - 616s 311ms/step - loss: 1.2071 - val_loss: 2.2875
Epoch 10/10
 979/1976 [=============>................] - ETA: 4:45 - loss: 1.1440 
```

1, num_words 12000, BATCH 64, embedding 1024, hiddel 2048, dropout 2