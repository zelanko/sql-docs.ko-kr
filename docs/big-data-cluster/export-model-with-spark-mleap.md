---
title: MLeap 사용 하 여 Spark ML 모델 내보내기
titleSuffix: SQL Server 2019 big data clusters
description: Spark 기계 학습 MLeap 사용 하 여 모델을 내보내는 방법에 알아봅니다.
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ee858f66c99ff7b85e2e6c456ad509ec7deb0a6e
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242134"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>Spark 기계 학습 MLeap 사용 하 여 모델 내보내기

일반적인 기계 학습 시나리오에는 Spark에서 모델 학습 및 Spark 외부에서 점수 매기기 포함 됩니다. Spark 외부는 사용할 수 있는 이식 가능한 형식으로 모델을 내보냅니다. [MLeap](https://github.com/combust/mleap) 은 이러한 하나의 모델 교환 형식입니다. Spark 기계 학습 파이프라인 및 모델을 사용 하 여 모든 JVM 기반 시스템에서 사용 하 고 이식 가능한 형식으로 내보낼 수는 `Mleap` 런타임입니다.

이 가이드에서는 Mleap를 사용 하 여 spark 모델 내보내는 방법을 보여 줍니다. 단계는 아래에 요약 하 고 다음 섹션의 코드를 사용 하 여 자세히 설명 됩니다.

1. Spark 모델을 만들어 시작 합니다. 이 용도로 **Spark를 사용 하 여 모델 학습 및 machine learning 만들기 [여기 있습니다.](train-and-create-machinelearning-models-with-spark.md)**
2. 우리가 다음 단계로 **training\test 데이터 및 모델 가져오기**
3. **모델 내보내기 `Mleap` 번들**합니다. 이 내보낸된 번들 spark 외부 점수를 이제 사용할 수 있습니다.
4. 유효성을 검사할 가져옵니다는 `Mleap` 백을 다시 번들를 사용 하는 Spark에서 점수를 매깁니다.

## <a name="step-1---start-by-creating-a-spark-model"></a>1 단계-Spark 모델을 만들어 시작
실행할 [Spark를 사용 하 여 모델 학습 및 machine learning 만들기](train-and-create-machinelearning-models-with-spark.md) 학습/테스트 집합 및 모델을 만들고 HDFS 저장소에 유지 합니다. 으로 모델을 내보내야 `AdultCensus.mml` 아래는 `spark_ml` 디렉터리입니다.

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>2 단계-training\test 데이터 및 모델을 가져옵니다

생성에 1 단계는 `AdultCensus.mml`은 spark 모델입니다. 

이 단계에서는 spark 모델을 가져옵니다.

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>3 단계-모델 내보내기 `Mleap` 번들

이식 가능한으로 Spark 모델 내보내기 `Mleap` 모델링 하 고 로컬 저장소에 유지 합니다. 이 단계를 게시, 모델은 노트북에서 사용 가능한 `Mleap` 서식을 지정 하 고 Spark 외부에서 사용할 수 있습니다.

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

유지 된 `Mleap` 로컬에서 hdfs에 번들

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>3 단계-가져오기 하 여 유효성 검사는 `Mleap` 번들 및 Spark에서 점수 매기기
2 단계에서에서는 이미 내보낸 상태 모델에는 이식 가능 `Mleap` Spark 외부에서 사용할 수 있는 형식입니다. 이 단계에서는 가져오는 `Mleap` Spark에서 serialize 되 고 테스트 집합에 점수에는 Spark에서 사용 합니다.
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>참조

* [PySpark notebook을 사용 하 여 시작](notebooks-guidance.md)
* [학습 및 Spark를 사용 하 여 기계 학습 모델 만들기](train-and-create-machinelearning-models-with-spark.md)
