# 2020-seoultech-datamining-assignment
- 본 과제에서 활용된 데이터의 출처는 kaggle 에서 가져온 데이터. 각 실험별로 데이터는 다음과 같음.
> -  Regression : Compressive strength concrete
> -  Classification : Tic_Tac_Toe_endgame
---
## regression analysis
- 2020년 1학기 데이터 마이닝 수업 중 과제수행 작업물을 깃 허브에 업로드함.
- linear regression 단일 모델 task와 lightgbm ensemble model task로 나눠서 분석 시행
- 모든 분석은 동일하게 train/test 를 7:3 비율로 split 했으며, 스케일링을 거치지 않은 raw data와 로그 스케일링을 진행한 log-scaling data로 나눠서 분석 시행.
- ensemble model의 경우 단일 모델과 실험 환경을 동일하게 하기 위해 grid search cv를 진행하지 않음.
- lightgbm 패키지 설치 요망
- Correlation coefficient heatmap 출력을 위한 Seaborn 패키지 설치 요망
```
$ pip install lightgbm Seaborn
```
---
## Classification analysis
- classification의 경우 황근성 선배님의 코드를 통해 분석을 실시했으며, 기존 코드와 다른점은 추가적인 EDA를 진행.
- graphviz 패키지 설치 요망. 기존 환경에서는 graphviz가 정상적으로 설치되지 않으므로 가상환경에서 생성하는 방법 추천. (OS 별로 문제도 있으며 가상환경으로 설치하는 방법이 제일 간단함)
```
$ conda create -n <virtual environment name>
```

### Mac/linux
```
$ source activate <virtual environment name>
```

### Windows
```
$ activate <virtual environment name>
```

### graphviz install
```
$ <virtual environment name> pip install graphviz
```

---
실습 코드는 python notebook으로 진행되어 있으며 각 데이터 별로 별도로 path를 설정해야 함.

## 실험 결과 요약
- Regression task
* 단일 모델로 좋은 성능을 내려면 데이터를 충분히 가공해야 함. 하지만 동일 조건에서 앙상블 모델을 사용할 경우 훨씬 좋은 성능을 낼 수 있음.
* 앙상블 모델의 경우 grid search, random search 등, 최적의 하이퍼 파라미터를 찾는 다양한 패키지가 존재.
* 블랙박스 모델이기 때문에 설명력은 다소 떨어지나, 예측값만큼은 동일 조건에서 우수한 성능을 보유.

- Classification task
* 동일한 regression tree 모델에서 index (Gini, Entropy, Entropy_Gain_Ratio)로 나눠서 분석 시행.
* 전체적인 퍼포먼스는 Gain_Ratio index가 우수하지만, 예측값의 안정성을 보장하고 싶다면 Gini index를 적용하는게 바람직함.
