# lg-aimers-7-


📑 LG Aimers 7th: Resort F&B Demand Forecasting AI

[주제] 리조트 내 식음업장 메뉴별 수요 예측 AI 모델 개발

      * 외부데이터 사용이 엄격히 금지된 대회였습니다.(오로지 EDA로 알아낸 정보만 피쳐로 활용가능)

[Metric] SMAPE (Symmetric Mean Absolute Percentage Error)

[팀원]
염재림, 김민석, 박채림, 정예경, 김도균 

[결과] Public Top 18% ➡️ Private Top 15% (124위 / 800+팀) 🏆

1) public
<img width="1353" height="69" alt="image" src="https://github.com/user-attachments/assets/46dbc0c6-56f2-40f0-ac52-298dd130c6ee" />

2) private
<img width="1342" height="72" alt="image" src="https://github.com/user-attachments/assets/313296eb-1dce-4966-af93-4adf4cb1f442" />



# 1. Project Overview
리조트 내 식음업장의 메뉴별 수요를 예측하여 식자재 로스율을 최소화하고, 운영 효율을 극대화하는 AI 모델을 개발했습니다. 불규칙한 수요 패턴 속에서 요일, 시즌, 메뉴 카테고리 간의 상관관계를 찾아내어 높은 예측 정확도를 달성했습니다.

# 2. Key Contributions 
본 프로젝트에서 데이터 분석(EDA)부터 최종 앙상블 모델링까지 전 과정에 참여하며 성능 향상을 이끌었습니다.

🔍 탐색적 데이터 분석 (EDA) & 전처리
```text
1) 시계열 패턴 추출: 연/월/일/요일/공휴일 등 시간 기반 피처를 생성하여 매장별 매출수량 시계열 패턴 추출

2) EDA:-특정 요일에 특정 매장의 매출 수량이 반복적으로 0인것을 통해 해당 요일이 매장의 정기 휴무일임을 추측.
       -공휴일 뿐만 아니라 공휴일 전날, 공휴일 다음날, 공휴일과 공휴일 사이의 평일(일명 샌드위치 평일), 일반 평일로 일자 구분 세분화하여 매출수량 분석
       -특정 시기에만 매출수량이 0인 시즌 메뉴 판별
                  
3) 이상치 및 결측치 처리: -행사 등으로 인해 발생한 튀는 데이터를 식별하고, 비즈니스 로직에 기반한 데이터 정제 수행.
                          - 매출 수량 중 음수로 나타난 값은 외상 또는 노쇼로 추측, 이상치로 판단하여 0으로 처리
```
🤖 모델링 및 최적화

CatBoost 기반 설계: 범주형 피처가 많은 데이터 특성에 맞춰 CatBoost를 메인 모델로 채택.

하이퍼파라미터 튜닝: Optuna를 활용하여 SMAPE 지표를 최소화하는 최적의 파라미터 조합 도출.

Robust 앙상블: 단일 모델의 한계를 극복하기 위해 CatBoost, XGBoost, LightGBM을 결합한 Weighted Ensemble 전략 적용.

# 3. Modeling Strategy & Results

| Step | Model & Strategy | Validation (SMAPE) |
| :--- | :--- | :---: |
| Base | CatBoost , LSTM Ensemble | 0.54885 |
| Final | Weighted Ensemble (CatBoost, XGB, LGBM) | 0.52770 |

# 4. Repository Structure

```text
├── EDA.ipynb               # 데이터 탐색, 시각화 및 전처리 전략 수립 (Individual)
├── lg_aimers,0.54885.ipynb # CatBoost , LSTM Ensemble (단순 가중치로 앙상블) (Individual)
├── final_code,0.5277.ipynb # 최종 앙상블 및 SMAPE 최적화 추론 코드 (Team/Main)
└── README.md
```
# 5. Tech Stack

Language: Python 3.8+

Frameworks: CatBoost, XGBoost, LightGBM, LSTM, Scikit-learn

Optimization: Optuna

Data Analysis: Pandas, Numpy, Matplotlib, Seaborn
