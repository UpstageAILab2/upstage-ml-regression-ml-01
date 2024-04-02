# Title (Please modify the title)

## Team

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [박패캠](https://github.com/UpstageAILab)             |            [이패캠](https://github.com/UpstageAILab)             |            [최패캠](https://github.com/UpstageAILab)             |            [김패캠](https://github.com/UpstageAILab)             |            [오패캠](https://github.com/UpstageAILab)             |
|                            팀장, 담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |                            담당 역할                             |

## 1. Competiton Info

### Overview
House Price Prediction 경진대회는 주어진 데이터를 활용하여 서울의 아파트 실거래가를 효과적으로 예측하는 모델을 개발하는 대회
다양한 변수와 데이터를 고려하여 모델을 훈련하고, 아파트의 실거래가에 대한 예측 성능을 높이기 위한 최적의 방법 찾기
서울시 각 지역의 아파트 매매 실거래가를 예측하는데 중점

### Timeline
2024.03.27 ~ 2024.04.02

### Evaluation

해당 시점의 매매 실거래가를 예측하는 Regression 대회
평가지표는 RMSE(Root Mean Squared Error)를 사용

## 2. Team Component

- 윤상원(팀원) : 모델 설계 및 실험(cat, xgboost,lightGBM), optuna로 파라미터 튜닝 
- 정병원(팀원) : 지오코팅을 이용한, 좌표X와 좌표Y의 결측치 보완
- 길종현(팀원) : 전반적인 전처리 및 feature importance 찾기
- 홍재민(팀원) : 범주형 데이터 인코딩(one-hot, label) 및 k-fold수행
- 한지승(팀장) : 팀의 기본적인 목표 설정, 협업 보조 및 공부

## 3. Data descrption

### Dataset overview

- 데이터 종류
아파트 실거래가 데이터(train.csv)
지하철역과 버스정류장에 대한 데이터(bus_feature.csv, subway_feature.csv)
평가 데이터(test.csv)

### EDA
train기준 결측치 80% ~ 90% 이상인 변수 제거
검색할 수 있는 데이터는 직접 찾아서 대체 ex) x,y좌표 보완
연속형 변수에는 -100, 범주형 변수는 null대체
Outlier삭제(건축년도 1973년, 층 -2) 

### Feature engineering
1. 강남/서초/용산구
   평균 실거래가가 높은 구는 강남구, 서초구, 용산구 -> 3개의 구에 해당하면 1, 아니면 0으로 처리
2. 건설사
   345개의 unique한 건설사 이름 존재 -> 특정 회사 단어를 기준으로 묶어 범주화 함 (345->136)
3. 버스, 지하철
   geocoding으로 주소정보를 이용하여 결측치 보완
4. 전용면적
   90 이하일 경우 1, 초과일경우 0
5. 아파트명 정리
   정규표현식을 이용 cardinality를 줄임 : n동, n차, n단지 등 제거(6586 -> 4362)
6. 아파트 브랜드
   아파트 브랜드가 부동산 가격에 영향을 미침 : 브랜드 있는 아파트명 1, 아니면 0으로 처리
   
## 4. Modeling

Encoding(one-hot, label) : 각 변수마다 적절한 인코딩을 사용

### Model descrition

사용 모델(CatBoost, XGBoost, LightGBM) 

### Modeling Result
<img width="799" alt="스크린샷 2024-04-02 오후 4 17 06" src="https://github.com/UpstageAILab2/upstage-ml-regression-ml-01/assets/156395327/9f05d5c4-bbfd-4a7e-8f52-7ea3f5786c92">


## 5. Result

### Leader Board
Team name : ML_1wh
<img width="1072" alt="스크린샷 2024-04-02 오후 4 22 07" src="https://github.com/UpstageAILab2/upstage-ml-regression-ml-01/assets/156395327/09f4dde0-5359-4734-b5d1-8696dbfca0e1">

### Presentation
[ML 1조 발표.pptx.pdf](https://github.com/UpstageAILab2/upstage-ml-regression-ml-01/files/14833025/ML.1.pptx.pdf)

### Areas for improvement
서버에서 저장한 CatBoost와 LGBM이 로컬에서 돌아가지 않아 앙상블을 수행하지 못함 ---> 추후에 진행할 예정
라우터를 사용하고 하였으나 혼선이 생겨 에러를 해결하지 못함 ---> 추후 라우터 사용을 위한 코드 수정
