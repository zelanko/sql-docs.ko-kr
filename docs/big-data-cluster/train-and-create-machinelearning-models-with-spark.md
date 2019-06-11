---
title: Spark 사용 하 여 학습/만들기 ML 모델
titleSuffix: SQL Server big data clusters
description: PySpark를 사용 하 여 학습 하 고 SQL Server 빅 데이터 클러스터 (미리 보기)에서 Spark를 사용 하 여 기계 학습 모델을 만듭니다.
author: lgongmsft
ms.author: lgong
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 348749b038b97138c4a6c85fd2f56b45b85c5d60
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822927"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>학습 및 Spark를 사용 하 여 기계 학습 모델 만들기

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 빅 데이터 클러스터에서 Spark를 통해 AI 및 기계 학습 수 있습니다. 이 예제에서는 어떻게 기계 학습 모델을 학습에 데이터를 사용 하 여 Spark (PySpark)에서 Python을 사용 하 여 HDFS에 저장 하는 방법을 보여 줍니다. 

예제에는 한 번에 각 셀 실행된 한 단계는 Azure 데이터 Studio Notebook에서 사용할 수 있는 코드 조각 사용 하 여 단계별 가이드입니다. Notebook에서 Spark를 사용 하 여 연결 하는 방법에 대 한 자세한 내용은 참조 [여기](notebooks-guidance.md)

예제:

1. 시작 **데이터 및 원하는 예측 이해**
2. **HDFS에 데이터를 업로드 하 고 데이터 준비** 모델을 만들기 위한
3. **사용 하 여 기능 선택**
4. **학습 및 테스트 집합으로 데이터 분합니다**
5. 결합 된 **ml 파이프라인 및 모델 빌드**
6. 만든된 모델을 사용 하 여 **예측**
7. 마지막 단계로 **나중에 사용 하도록 작성된 된 모델을 유지**합니다.

E2E machine learning에는 몇 가지 추가 단계, 예, 데이터 탐색, 기능 선택 및 사용자 구성 요소 분석, 모델 선택 해야합니다. 이러한 단계의 대부분 여기에 간단히 나타내기 위해 무시 됩니다.

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>1 단계-데이터 및 원하는 예측 이해

이 예제에서는 성인 인구 조사 소득 데이터로 [여기]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv )합니다. `AdultCensusIncome.csv`, 각 행이 나타내는 수입 범위 및 기타 특성 등 기간, 주당 시간, 교육, 직업 등 특정된 성인에 대 한 합니다. 하는 경우 예측할 수 있는 모델 작성 수입 범위입니다. 모델 사용 기간 및 기능으로 주당 시간 되며 수입 하는 경우 예측할 > 50k 또는 < 50 11. 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>2 단계-데이터의 기본 탐색 하 고 HDFS에 데이터 업로드
Azure Data Studio에서 HDFS/Spark 게이트웨이로 연결 하 고 라는 디렉터리를 만듭니다 `spark_ml` HDFS에서. 다운로드 [AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ) 로컬 시스템 및 HDFS에 업로드 합니다. 업로드 `AdultCensusIncome.csv` 사용자가 만든 폴더에 있습니다.


이제 일부 코드를 작성 합니다. 아래 코드를 복사 하에서 Azure Data Studio notebook의 개별 셀에 붙여 넣습니다. 

아래 코드는 Spark 데이터 프레임으로 CSV 파일을 읽습니다. 세세 하는 행 및 열 수를 계산 하 고 로드 된 데이터를 표시 합니다.

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>3 단계-사용 하 여 기능 선택

이 단계에서는 다음 두 용어 사용
1. `Label`    -예측할 값을 가리킵니다. 이 데이터의 열으로 표시 됩니다.  
2. `Features` -예측 하는 데이터의 특징을 가리킵니다. 또는 일부 시간 라고도 함 `predictors` 

이 예제의 `Label`은 합니다 **income** 열입니다. 간단히 하기 위해 선택 **age** 하 고 **hours_per_week** 으로 `Features`입니다. 실제로 어떤 가장 특징을 결정 예측 레이블 이해 하려면 몇 가지 상관 관계 기법을 적용 하 여 기능 선택 됩니다.

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>4 단계-학습 및 테스트 집합으로 분할

행의 75%를 사용 하 여 나머지 25% 모델을 평가 하 고 모델을 학습 합니다. 또한 학습을 유지 하 고 HDFS 저장소에 데이터 집합을 테스트 합니다. 단계는 필요 하 긴 하지만 보여 주기 위해 표시 된 저장 및 ORC 형식으로 로드 합니다. 예를 들어, 다른 형식으로 `Parquet` 사용할 수도 있습니다.

이 단계를 참조 해야 AdultCensusIncomeTrain 이름과 AdultCensusIncomeTest를 사용 하 여 만든 두 개의 디렉터리 게시

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>5 단계-파이프라인에 결합 하 고, 모델 작성
[Spark ML 파이프라인](https://spark.apache.org/docs/2.3.1/ml-pipeline.html) 워크플로로 모든 단계를 시퀀스 하 고 쉽게 다양 한 알고리즘 및 매개 변수를 사용 하 여 실험을 허용 합니다. 다음 코드는 먼저 단계를 생성 하 고이 단계를 함께 Ml 파이프라인에 놓입니다.  LogisticRegression 모델을 만드는 사용 됩니다.

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

이제 마련 파이프라인. 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

파이프라인 만들어지면 했으므로 모델의 학습에 사용 합니다.

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>6 단계-모델을 사용 하 여 예측 및 모델 정확도 평가 합니다.
아래 코드는 위의 단계에서 만든 모델을 사용 하 여 결과 예측 하려면 테스트 데이터 집합을 사용 합니다. 사용 하 여 모델의 정확도 측정 `areaUnderROC` 고 `areaUnderPR` 메트릭.

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>7 단계-hdfs 모델 유지
마지막으로 HDFS에서 나중에 사용할 모델을 유지 합니다. /Spark_ml/AdultCensus.mml으로 작성된 된 모델 저장이 단계를 게시 합니다.

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>다음 단계

PySpark notebook을 사용 하 여 시작 하는 방법에 대 한 자세한 내용은 참조 하세요. [notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.