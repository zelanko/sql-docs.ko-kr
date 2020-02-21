---
title: 'Spark ML 모델 만들기, 내보내기: MLeap'
titleSuffix: SQL Server Big Data Clusters
description: PySpark를 사용하여 SQL Server 빅 데이터 클러스터에서 Spark로 Machine Learning 모델을 학습하고 만듭니다. MLeap을 사용하여 내보낸 후 SQL Server에서 Java를 사용하여 모델을 채점합니다.
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 717093278790c90486b424678d332f73e056e86e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255907"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에서 Spark Machine Learning 모델을 만들고, 내보내고, 채점합니다.

다음 샘플은 [Spark ML](https://spark.apache.org/docs/latest/ml-guide.html)을 사용하여 모델을 빌드하고, 모델을 [MLeap](http://mleap-docs.combust.ml/)으로 내보내고, SQL Server에서 해당 [Java 언어 확장 프로그램](../language-extensions/language-extensions-overview.md)을 사용하여 모델을 채점하는 방법을 보여줍니다. 이 작업은 SQL Server 2019 빅 데이터 클러스터의 컨텍스트에서 수행됩니다.

다음 다이어그램은 이 샘플에서 수행되는 작업을 보여줍니다.

![Spark로 학습 점수 내보내기](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>사전 요구 사항

이 샘플의 모든 파일은 [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)에 있습니다.

또한 샘플을 실행하기 위한 사전 요구 사항은 다음과 같습니다.

- [SQL Server 빅 데이터 클러스터](deploy-get-started.md)

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Spark ML을 사용하여 모델 학습

이 샘플에서는 Spark ML 파이프라인 모델을 빌드하기 위해 인구 조사 데이터(**AdultCensusIncome.csv**)가 사용됩니다.

1. [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/setup.sh) 파일을 사용하여 인터넷에서 데이터 세트를 다운로드하고 이를 SQL Server 빅 데이터 클러스터의 HDFS에 둡니다. 이렇게 하면 Spark에서 액세스할 수 있습니다.

1. 그런 후 샘플 노트북 [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)를 다운로드합니다. PowerShell 또는 bash 명령줄에서 다음 명령을 실행하여 노트북을 다운로드합니다.

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   이 노트북에는 샘플의 이 섹션에 필요한 명령이 포함된 셀이 있습니다.

1. Azure Data Studio에서 노트북을 열고 각 코드 블록을 실행합니다. 노트북 작업에 대한 자세한 내용은 [SQL Server에서 노트북 사용 방법](notebooks-guidance.md)을 참조하세요.

데이터가 먼저 Spark로 읽혀진 후 학습 및 테스트 데이터 세트로 분할됩니다. 그런 다음, 코드가 학습 데이터를 사용하여 파이프라인 모델을 학습시킵니다. 마지막으로 모델을 MLeap 번들로 내보냅니다.

> [!TIP]
> 또한 [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_pyspark.py) 파일의 노트북 외부에서 이 단계들과 연관된 Python 코드를 검토하거나 실행할 수 있습니다.

## <a name="model-scoring-with-sql-server"></a>SQL Server로 모델 채점

이제 Spark ML 파이프라인 모델이 일반 직렬화 [MLeap 번들](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) 형식이므로, Spark가 없어도 Java로 모델을 채점할 수 있습니다. 

이 샘플은 SQL Server에서 [Java 언어 확장 프로그램](../language-extensions/language-extensions-overview.md)을 사용합니다. SQL Server에서 모델을 채점하려면 먼저 모델을 Java로 로드하고 채점할 수 있는 Java 애플리케이션을 빌드해야 합니다. 이 Java 애플리케이션의 샘플 코드는 [mssql-mleap-app 폴더](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mssql-mleap-app)에서 찾을 수 있습니다.

샘플을 빌드한 후 Transact-SQL을 사용하여 Java 애플리케이션을 호출하고 데이터베이스 테이블로 모델을 채점할 수 있습니다. 이것은 [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_sql_tests.py) 소스 파일에서 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.
