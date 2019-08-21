---
title: Spark 작업을 사용하여 데이터 수집
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 Azure Data Studio에서 Spark 작업을 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 사용 하 여의 데이터 풀에 데이터를 수집 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5325b44512d2dc1522d4bc49478e65ae4c0999e0
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653291"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>자습서: Spark 작업을 사용하여 SQL Server 데이터 풀로 데이터 수집

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 Spark 작업을 사용 하 여의 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] [데이터 풀](concept-data-pool.md) 에 데이터를 로드 하는 방법을 보여 줍니다. 

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 데이터 풀에 외부 테이블을 만듭니다.
> * HDFS에서 데이터를 로드하는 Spark 작업을 만듭니다.
> * 외부 테이블에서 결과를 쿼리합니다.

> [!TIP]
> 원하는 경우 이 자습서의 명령을 위해 스크립트를 다운로드하여 실행할 수 있습니다. 자세한 내용은 GitHub에서 [데이터 풀 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)을 참조하세요.

## <a id="prereqs"></a> 사전 요구 사항

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>데이터 풀에 외부 테이블 만들기

다음 단계에서는 데이터 풀에 **web_clickstreams_spark_results**라는 외부 테이블을 만듭니다. 그런 다음, 이 테이블을 빅 데이터 클러스터로 데이터를 수집하는 위치로 사용할 수 있습니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)을 참조하세요.

1. **서버** 창에서 연결을 두 번 클릭하여 SQL Server 마스터 인스턴스의 서버 대시보드를 표시합니다. **새 쿼리**를 선택합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 데이터 풀에 외부 데이터 원본이 아직 없는 경우 새로 만듭니다.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 데이터 풀에 **web_clickstreams_spark_results**라는 외부 테이블을 만듭니다.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. CTP 3.1에서는 데이터 풀을 만드는 작업이 비동기적으로 수행되지만, 이미 완료되었는지 확인할 수 있는 방법이 없습니다. 데이터 풀이 생성될 때까지 2분 정도 기다렸다가 계속 진행합니다.

## <a name="start-a-spark-streaming-job"></a>Spark 스트리밍 작업 시작

다음 단계는 스토리지 풀(HDFS)에서 데이터 풀에 만든 외부 테이블로 웹 클릭 스트림 데이터를 로드하는 Spark 스트리밍 작업을 만드는 것입니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 마스터 인스턴스에 연결합니다. 자세한 내용은 [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

1. **서버** 창에서 HDFS/Spark 게이트웨이 연결을 두 번 클릭합니다. 그런 다음, **새 Spark 작업**을 선택합니다.

   ![새 Spark 작업](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. **새 작업** 창의 **작업 이름** 필드에 이름을 입력합니다.

1. **Jar/py 파일** 드롭다운에서 **HDFS**를 선택합니다. 다음과 같은 jar 파일 경로를 입력합니다.

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. **주 클래스** 필드에 `FileStreaming`를 입력합니다.

1. **인수** 필드에 다음 텍스트를 입력하고 `<your_password>` 자리 표시자에 SQL Server 마스터 인스턴스의 암호를 지정합니다. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   다음 표에서는 각 인수를 설명합니다.

   | 인수 | 설명 |
   |---|---|
   | 서버 이름(server name) | 테이블 스키마를 읽는 데 사용할 SQL Server |
   | port number | SQL Server가 수신 대기 중인 포트(기본값 1433) |
   | username | SQL Server 로그인 사용자 이름 |
   | password | SQL Server 로그인 암호 |
   | 데이터베이스 이름 | 대상 데이터베이스 |
   | external table name | 결과에 사용할 테이블 |
   | Source directory for streaming | “hdfs:///clickstream_data”와 같은 전체 URI여야 합니다. |
   | input format | “csv”, “parquet” 또는 “json”일 수 있습니다. |
   | enable checkpoint | true 또는 false |
   | timeout | 종료하기까지 작업을 실행할 시간(밀리초) |

1. **제출**을 눌러 작업을 제출합니다.

   ![Spark 작업 제출](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>데이터 쿼리

다음 단계에서는 Spark 스트리밍 작업이 HDFS에서 데이터 풀로 데이터를 로드하는 방법을 보여 줍니다.

1. 수집된 데이터를 쿼리하기 전에 작업 기록 출력을 살펴보고 작업이 완료되었는지 확인합니다.

   ![Spark 작업 기록](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 이 자습서의 시작 부분에서 열었던 SQL Server 마스터 인스턴스 쿼리 창으로 돌아갑니다.

1. 다음 쿼리를 실행하여 수집된 데이터를 검사합니다.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>정리

다음 명령을 사용하여 이 자습서에서 만든 데이터베이스 개체를 제거합니다.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>다음 단계

Azure Data Studio에서 샘플 Notebook을 실행하는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [샘플 Notebook 실행](tutorial-notebook-spark.md)
