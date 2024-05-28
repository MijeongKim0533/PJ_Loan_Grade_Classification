# 고객 대출등급 분류

## 1. 프로젝트 주제
고객 금융정보를 기반으로 대출등급 분류 및 등급에 영향을 미치는 변수 파악

## 2. 프로젝트 목적
- 신용등급 상향평준화로 신용점수 변별력 감소 -> 은행은 자체 신용평가 모델을 개발하여 활용 중
- 신용등급에 따라 대출의 한도를 정하는 대출등급은 어떻게 분류되고 있는지 확인
  
## 3. 분석과정
- 데이터 : 
<p align='center'><img width="300" alt="image" src="https://github.com/MijeongKim0533/PJ_Loan_Grade_Classification/assets/152786534/db8d3df2-8241-47f6-ab26-a0888decc872"><br>

- 대출금액의 단위가 크고 분포가 편향된 변수가 있어 로그 스케일링 진행
- 범주형 컬럼 라벨인코딩 적용<br> 
    -> 숫자의 크기에 영향을 받지 않는 트리계열 모델 선택<br>
    (GradientBoosting, XGBoost, RandomForest)
- 기존 변수로는 정확도가 오르지 않아 파생변수 2개 생성<br>
  1. 총상환원금 / 총상환이자
  2. 총상환원금 / 대출금액
- 변수선택 : RFECV, Feature importance 사용
- Grid Search 사용하여 파라미터 튜닝, Kfold 사용하여 교차검증
- SHAP라이브러리 사용하여 등급에 영향을 미치는 변수 파악
- 최종 선택모델 : XGBClassifier<br>
  정확도 0.77 -> 0.94, F1 score 0.75 -> 0.94  
## 4. 결론
<p align='center'><img width="400" alt="image" src="https://github.com/MijeongKim0533/PJ_Loan_Grade_Classification/assets/152786534/14294e90-f812-4894-8737-b7a4c4f423b6"></p>
1. 대출등급을 결정하는 중요한 변수는 상환과 관련된 변수이다.<br>
2. 상환액보다는 상환 자체가 대출등급과 관련이 있다.<br>
3. 연체관련 변수나 주택소유는 대출등급과 큰 관련이 없다.<br>
4. 참고논문('P2P 대출상환 성공요인에 관한 연구')에서 생계필수비용 목적의 경우 상환율이 높다는 연구가 있음.<br>
5. 금융데이터 이외의 정보를 추가하여 상환가능성을 측정하면 운영에 도움이 될 것이라 예상
