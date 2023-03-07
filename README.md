# 조기폐암 진단을 위한 폐암 예측 모델링

## 1. 프로젝트 설명

### (1) 주제 및 배경 설명
- 주제 : 폐암의 조기 진단을 위해 데이터를 통해 폐암을 조기 진단하는 XGB 모델을 개발하자
- 프로젝트 배경 : 폐암은 X-ray 검사만으로는 발견하지 못함, 흉부 CT검사 필요 -> 조기 폐암진단을 통해 사회적 비용을 줄일 수 있음

### (2) 데이터 
- 출처 : 캐글(https://www.kaggle.com/datasets/mysarahmadbhat/lung-cancer)

<img width = "200" src="https://user-images.githubusercontent.com/102526342/222624862-751350a9-82d0-4db0-a8e4-29f97c889c67.png">


- LUNG_CANCER, GENDER : 명목형 칼럼
- AGE : 연속형 칼럼
- 이외 칼럼 : 이진형(binary)

### (3) 전처리
- NA 0개
- 증복 관측치 33개 제거
- LUNG_CANCER, GENDER : LabelEncoder()사용

### (4) 모델링
- XGBClassifier, Randomized Search
- 최적의 파라미터
    - max_depth : 6
    - min_child_weight : 4
    - learning_rate : 0.05
- baseline model : weighted avg f1-score =0.83

<img width = "400" src="https://user-images.githubusercontent.com/102526342/222626251-adc461b3-7dfe-4c00-a406-38a3b8b075d0.png">

- 타겟 불균형을 SMOTE(oversampling)을 활용하여 0/1 class 개수를 맞춰줌
<img width = "400" src="https://user-images.githubusercontent.com/102526342/222626528-d31e571c-477f-4c3a-995e-2b7d57d77b37.png">

<img width = "400" src="https://user-images.githubusercontent.com/102526342/222626552-117633cc-e695-4ff7-b425-89a443ef43f4.png">

- eli5.sklearn의 PermutaionImportance를 통해 상위 특성 5개만 사용 -> test weighted avg f1-score =0.87로 오히려 성능이 떨어짐

<img width = "700" src="https://user-images.githubusercontent.com/102526342/222628592-db667c60-3cd5-4e15-a318-e73171ec63fd.png">

### (5) 결과
- 최종 train weighted avg f1-score = 0.92<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; teset weighted avg f1-score = 0.93 (basemodel의 weighted avg f1-score =0.83 보다 0.1 높음)

<img width = "400" src="https://user-images.githubusercontent.com/102526342/222626588-cb256710-5812-4be5-bdb3-0c10fbc57bdb.png">

