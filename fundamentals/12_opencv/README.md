# 알게된 것

### 랜드마크

- 조정(alignment)이라고도 함
- 조금 더 큰 범위로는 keypoint detection이라고 부름
- 각각의 위치를 찾아냄

### dilb

- HOG feature를 사용해서 SVM의 sliding window로 얼굴을 찾음.

### 이미지 파라미드

- 이미지를 unsampling 방법을 통해 크기를 키우는 것

### face landmoark localization

- 이목구비 위치 추론

# 궁금한 것

### `cv2.imread(fileName, flag)`

- flag에 origin과 IMREAD_UNCHANGED 의 차이가 뭔지 몰겠음. alpha channel까지 포함한다는데!