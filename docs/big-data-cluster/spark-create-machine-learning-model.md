---
title: 만들기 및 Spark 기계 학습 MLeap 사용 하 여 모델 내보내기
titleSuffix: SQL Server big data clusters
description: PySpark를 사용 하 여 학습 하 고 SQL Server 빅 데이터 클러스터 (미리 보기)에서 Spark를 사용 하 여 기계 학습 모델을 만듭니다. MLeap를 사용 하 여 내보내고 SQL Server에서 Java 사용 하 여 모델을 점수 매기기입니다.
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727379"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>만들기, 내보내기 및 SQL Server 빅 데이터 클러스터에 Spark를 기계 학습 모델 점수 매기기

다음 샘플을 사용 하 여 모델을 빌드하는 방법을 보여 줍니다 [Spark ML](https://spark.apache.org/docs/latest/ml-guide.html), 모델을 내보낼 [MLeap](http://mleap-docs.combust.ml/)를 사용 하 여 SQL Server에서 모델을 점수 매기기 및 해당 [Java 언어 확장](../language-extensions/language-extensions-overview.md)합니다. SQL Server 2019 빅 데이터 클러스터의 컨텍스트에서 수행 됩니다.

다음 다이어그램에서는이 샘플에서 수행 하는 작업을 보여 줍니다.

![Spark 사용 하 여 학습 점수 내보내기](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>사전 요구 사항

이 샘플에 대 한 모든 파일은 [ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)합니다.

샘플을 실행 하려면 다음 필수 조건이 있어야 합니다.

- [빅 데이터 클러스터 SQL Server](deploy-get-started.md)

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Spark ML을 사용 하 여 모델 학습

이 샘플에서는 인구 조사 데이터 (**AdultCensusIncome.csv**) Spark ML 파이프라인 모델을 빌드하는 데 사용 합니다.

1. 사용 된 [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) 파일이 인터넷에서 데이터 집합을 다운로드 하 고 SQL Server 빅 데이터 클러스터의 HDFS에 넣습니다. 따라서 Spark에서 액세스할 수 있습니다.

1. 다음 샘플 노트북을 다운로드 [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)합니다. PowerShell 또는 bash 명령줄에서 노트북을 다운로드 하려면 다음 명령을 실행 합니다.

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   이 노트북 샘플의이 섹션에 대 한 필요한 명령 사용 하 여 셀을 포함합니다.

1. Azure 데이터 스튜디오에서 노트북을 열고 각 코드 블록을 실행 합니다. Notebook 사용 하 여 작업에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.

데이터는 먼저 Spark를 읽고 학습 및 테스트 데이터 집합으로 분할 합니다. 다음 코드는 학습 데이터를 사용 하 여 파이프라인 모델을 학습합니다. 마지막으로 모델을 MLeap 번들에 내보냅니다.

> [!TIP]
> 또한 검토 하거나 외부의 노트북에서 다음이 단계를 사용 하 여 연결 된 Python 코드를 실행 합니다 [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) 파일입니다.

## <a name="model-scoring-with-sql-server"></a>SQL Server를 사용 하 여 점수 매기기 모델

Spark ML 파이프라인 모델은 일반적인 serialization 했으므로 [MLeap 번들](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) 형식으로 Java에서 모델을 Spark 없이 채 점할 수 있습니다. 

이 샘플에서는 합니다 [Java 언어 확장](../language-extensions/language-extensions-overview.md) SQL Server에서. SQL Server에서 모델 점수 매기기를 위해 먼저 Java 모델을 로드 하 고 점수를 매긴 수 있는 Java 응용 프로그램을 작성 해야 합니다. 이 Java 응용 프로그램에 대 한 샘플 코드를 찾을 수 있습니다 합니다 [mssql-mleap 앱 폴더](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app)합니다.

샘플을 빌드한 후를 Java 응용 프로그램을 호출 하 여 데이터베이스 테이블을 사용 하 여 모델 점수 매기기 Transact SQL을 사용할 수 있습니다. 이 다음에서 볼 수 있습니다 [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) 소스 파일입니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [Kubernetes 클러스터로 빅 데이터를 SQL Server를 배포 하는 방법](deployment-guidance.md)
