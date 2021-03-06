### 의료 영상 분석 특징

- 의료 영상 이미지는 개인 정보 보호 등의 이슈로 인해 데이터를 구하는 것이 쉽지 않음
- 라벨링 작업 자체가 전문 지식을 요하므로 데이터셋 구축 비용 비쌈
- 희귀질병을 다루는 경우 데이터를 입수하는 것 자체가 드뭄
- 음성/양성 데이터 간 imbalance가 심함. 학습에 주의가 필요
- 이미지만으로 진단이 쉽지 않아 다른 데이터와 결합해서 해석해야 할 필요

→ 딥러닝 영상처리 기술뿐 아니라, 의료 도메인 지식 및 의료 영상에 대한 명확한 이해가 아울러 필요

### 폐 문제 진단 방법

- X-RAY(엑스레이) 영상
- CT 영상

### X-RAY

- 전자를 물체에 충돌시킬 때 발생하는 투과력이 강한 복사선(전자기파)
- 방사선의 일종으로 지방, 근육, 천, 종이같이 밀도가 낮은 것은 수월하게 통과하지만, 밀도가 높은 뼈, 금속 같은 물질은 잘 통과하지 못함

### CT

- Computed Tomography
- 환자를 중심으로 X-RAY를 빠르게 회전하여 3D 이미지를 만들어냄
- 환자의 3차원 이미지를 형성하여 기본 구조는 물론 가능한 종양 또는 이상을 쉽게 식별하고 위치를 파악할 수 있음
- Slice : 신체의 단면 이미지. 단층 촬영 이미지라고도 하며 기존의 X-RAY 보다 더 자세한 정보를 포함

### MRI

- Magnetic Resonance Imageing (자기 공명 영상)
- 신체의 해부학적 과정과 생리적 과정을 보기 위해 사용하는 의료 영상 기술
- MRI 스캐너는 강한 자기장을 사용하여 신체 기관의 이미지를 생성
- MRI는 CT, X-RAY와 다르게 방사선을 사용하지 않아서 방사선의 위험성에서는 보다 안전