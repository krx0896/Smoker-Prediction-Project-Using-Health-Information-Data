# Project
### 건강정보 데이터를 활용한 흡연자 예측 모델링 프로젝트

# Intro 
### 🗓️ Date 
- Field Camp at KAIST
Project term : 2022.08.03 ~ 2022.08.10 </br>
Presentation Date : 2022.08.11 </br>

- 산업인공지능 개인 프로젝트
Project term : 2023.04.15 ~ 2023.05.02 </br>
Presentation Date : 2023.05.03 </br>
  
# Data Set 
### ✅ Source 
https://www.kaggle.com/datasets/hongseoi/health-checkup-result?select=2020.csv <br/> 
csv file : 2020.csv : ( train + test )

### ✅ Characteristics of the dataset 
  * 타입 : Multivariate
  * 데이터 수 : 100,000개
  * 피쳐 : 31개 (Target var : "흡연자, 비흡연자, 금연", predictors : 30개)
  * 타겟 변수의 클래스 불균형 : 흡연 유무에 대한 타겟 데이터의 비율 -> 59:31:20
  * 전체 데이터의 갯수 중 60% 이상의 결측치를 가지는 변수가 6개 존재함

# Contents
- Preliminaries
- Load the dataset
- Data Preprocessing
  - 결측치 처리
    - 결측치가 많은 변수들이 중요한 변수들이라고 판단하고 결측치를 전처리하는 방법을 3가지로 나눔
      - 방법1: 65%이상의 결측치를 가지는 변수들을 모두 삭제하기 -> 10만개 데이터를 다 사용하며 변수들만 삭제함
      - 방법2: 결측치를 가지는 데이터 삭제하기 -> 중요한 변수들을 살리면서 데이터의 갯수가 결측치를 삭제해도 4만개로 충분하다고 판단
      - 방법3: 결측치를 가지는 데이터값 예측 함수(IterativeImputer)로 채워넣기 -> 10만개 데이터를 다 사용하며 변수들도 다 사용하는 방법
  - 이상치 처리
    - 사람의 체내 데이터로 이상치도 의미가 있다고 판단하여 시력이 9.9(실명)과 같은 극단적인 값들만 삭제
  - Feature Extraction
    - 성별과 키, 몸무게, 허리둘레와 같은 변수들이 많으면 다중공선성을 띄므로 BMI와 같은 새로운 파생변수를 생성
  - Scaling
    - 데이터셋에 많은 이상치가 존재하므로 이상치에 덜 민감한 Robust Scaler을 사용함
  - Encoding
    - one hot encoding으로 범주형 변수를 숫자형태로 바꾸기
  - SMOTE
    - 종속 변수의 클래스의 비율이 데이터 불균형 문제가 존재하는 것을 확인하여 합성 샘플링을 사용함
  - Data Split
    - 7:3의 비율로 train set과 test set을 나눠줌
- Build the model
  - MLP
  - Random Forest
    - OpenCV로 하이퍼파라미터 튜닝
  - SVM
  - Logestic regression
- Training
  - MLP 모델을 학습시키며 train, validation set의 Accuracy, Loss를 그래프로 시각화한 결과 결측치 전처리 방법3이 매우 불안정하게 학습되는 것을 보고 방법3은 좋은 방법이 아니라고 판단
- Evaluation
  - Confusion matrix로 모델 성능 평가
    - Recall 또는 Precision에 속하는 사람들은 모델이 잘 못 판단했을 수도 있지만 흡연을 하지만 건강 상태가 좋거나 흡연을 하지 않지만 건강하지 않은 것으로 
  - Random Forest의 Feature Importances로 결측치에서 제거하지 않은 변수가 실제로 중요한 변수인지 본 결과 중요했음

<img src="./image/[참고자료]산업인공지능 개인프로젝트 프레임워크.jpg">

### ✅ Best Model & Score
방법2로 전처리한 Random Forest </br>
  * Accuracy : 0.8019
  * F1socre : 0.8023
  * AUCscore : 0.7218

# 참고 논문
-	김진옥, “현재 흡연자와 비흡연자의 혈중지질 수준 비교”, 연세대 보건대학원, 2002.12, p18~
-	정인경, “제5기 국민건강영양조사 자료 중 남성에서 흡연 상태와 고밀도지단백-콜레스테롤 농도의 관련성”, 호남대
-	이혜숙, “정상 성인에서 흡연, 일반적 특성과 혈청지질과의 상관관계”, 한국 간호 교육 학회지, 2004
-	성동경, “청소년 흡연이 구강질환에 미치는 영향”, 연세대 보건대학원, 2000.06, p32~
-	박정진, “비만과 치아우식증의 상관성에 관한 연구”, 연세대 보건대학원, 2002.12, p13~
-	윤지선, “흡연자 판별을 위한 모형별 성능 검증”, 고려대 컴퓨터정보통신대학원, 2019
-	심경란, “성인 흡연자, 간접흡연자, 비흡연자의 DPOAE 비교”, 대구가톨릭대학교 의료보건과대학원, 2017
-	한주희, “성인 남자의 흡연과 BMI와의 관계”, 연세대 보건대학원, 1998
# 참고 자료
-	김미리, “금연하면 콜레스테롤 낮춰진다”, Medical Observer, 2010.12, http://www.monews.co.kr/news/articleView.html?idxno=38328 
-	이문예 기자, “좋은 콜레스테롤(HDL 콜레스테롤) 수치 낮다면 금연부터 시작하세요”, 푸드앤메드, http://www.foodnmed.com/news/articleView.html?idxno=12511 
-	진주창, “중성지방, 트리글리세라이드 수치 낮추는 법”, 건강상식 블로그, https://blog.naver.com/cvdasa4cfx/222561061563 
-	국가지표체계, 현재흡연율, https://www.index.go.kr/unify/idx-info.do?idxCd=4237 
-	통계청, 연령별 성별 흡연 관련 문항, KOSIS, https://kosis.kr/statHtml/statHtml.do?orgId=350&tblId=DT_35007_N045 
-	한상헌, “흡연하면 청력도 나빠진다… 비흡연자에 비해 1.7배 저하”, 서울경제, https://www.sedaily.com/NewsView/1RY41VC6QR 
