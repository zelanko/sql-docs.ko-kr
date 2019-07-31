---
title: MLeap를 사용 하 여 Spark machine learning 모델 만들기 및 내보내기
titleSuffix: SQL Server big data clusters
description: PySpark를 사용 하 여 SQL Server 빅 데이터 클러스터 (미리 보기)에서 Spark를 사용 하 여 기계 학습 모델을 학습 하 고 만들 수 있습니다. MLeap를 사용 하 여 내보낸 다음 SQL Server의 Java를 사용 하 여 모델의 점수를 계산 합니다.
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "67727379"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터에서 Spark 기계 학습 모델 만들기, 내보내기 및 점수 매기기

다음 샘플에서는 [SPARK ML](https://spark.apache.org/docs/latest/ml-guide.html)을 사용 하 여 모델을 작성 하 고, 모델을 [mleap](http://mleap-docs.combust.ml/)로 내보내고, SQL Server에서 모델의 점수를 [Java 언어 확장과](../language-extensions/language-extensions-overview.md)함께 보여 줍니다. SQL Server 2019 빅 데이터 클러스터의 컨텍스트에서 수행 됩니다.

다음 다이어그램은이 샘플에서 수행 되는 작업을 보여 줍니다.

![Spark로 점수 내보내기 학습](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>사전 요구 사항

이 샘플의 모든 파일은에 [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)있습니다.

샘플을 실행 하려면 다음과 같은 필수 구성 요소도 필요 합니다.

- [SQL Server 빅 데이터 클러스터](deploy-get-started.md)

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Spark ML을 사용 하 여 모델 학습

이 샘플에서는 인구 조사 data (**AdultCensusIncome**)를 사용 하 여 Spark ML 파이프라인 모델을 만듭니다.

1. [Mleap_sql_test/setup.exe](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) 파일을 사용 하 여 인터넷에서 데이터 집합을 다운로드 하 고 SQL Server 빅 데이터 클러스터의 HDFS에 배치 합니다. 이렇게 하면 Spark에서 액세스할 수 있습니다.

1. 그런 다음 샘플 노트북 train_score_export_ml_models_with_spark를 다운로드 합니다 [.](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb) PowerShell 또는 bash 명령줄에서 다음 명령을 실행 하 여 노트북을 다운로드 합니다.

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   이 노트북에는 샘플의이 섹션에 필요한 명령이 포함 된 셀이 포함 되어 있습니다.

1. Azure Data Studio에서 노트북을 열고 각 코드 블록을 실행 합니다. 노트북 작업에 대 한 자세한 내용은 [SQL Server 2019 미리 보기에서 노트북을 사용 하는 방법](notebooks-guidance.md)을 참조 하세요.

먼저 데이터를 Spark로 읽어서 학습 및 테스트 데이터 집합으로 분할 합니다. 그런 다음 코드는 학습 데이터를 사용 하 여 파이프라인 모델을 학습 합니다. 마지막으로, 모델을 MLeap 번들로 내보냅니다.

> [!TIP]
> [Mleap_sql_test/mleap_pyspark py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) 파일의 노트북 외부에서 이러한 단계와 연결 된 Python 코드를 검토 하거나 실행할 수도 있습니다.

## <a name="model-scoring-with-sql-server"></a>SQL Server를 사용 하 여 모델 점수 매기기

이제 Spark ML 파이프라인 모델이 일반적인 직렬화 [Mleap 번들](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) 형식 이므로 spark가 없어도 Java에서 모델의 점수를 매길 수 있습니다. 

이 샘플에서는 SQL Server의 [Java 언어 확장](../language-extensions/language-extensions-overview.md) 을 사용 합니다. SQL Server에서 모델의 점수를 매기는 먼저 모델을 Java로 로드 하 고 점수를 매길 수 있는 Java 응용 프로그램을 만들어야 합니다. 이 Java 응용 프로그램에 대 한 샘플 코드는 [mssql-mleap-앱 폴더](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app)에서 찾을 수 있습니다.

예제를 빌드한 후에는 Transact-sql을 사용 하 여 Java 응용 프로그램을 호출 하 고 데이터베이스 테이블을 사용 하 여 모델의 점수를 매길 수 있습니다. 이는 [mleap_sql_test/mleap_sql_tests py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) 원본 파일에서 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md) 을 참조 하세요.
