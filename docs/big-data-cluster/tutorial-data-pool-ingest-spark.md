---
title: Spark 작업을 사용 하 여 SQL Server 데이터 풀에 데이터를 수집 하는 방법 | Microsoft Docs
description: 이 자습서에는 Spark 작업을 사용 하 여 Azure Data Studio에서 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 데이터 풀에 데이터를 수집 하는 방법을 보여 줍니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: 186de5e63663b9c5485cd0385ded816cafbc7c3d
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221479"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>자습서: Spark 작업을 사용 하 여 SQL Server 데이터 풀에 데이터 수집

이 자습서에는 Spark 작업을 사용 하 여 데이터를 로드 하는 방법을 보여 줍니다.는 [데이터 풀](concept-data-pool.md) SQL Server 2019 빅 데이터 클러스터 (미리 보기). 

이 자습서에 알아봅니다 방법:

> [!div class="checklist"]
> * 데이터 풀에서 외부 테이블을 만듭니다.
> * HDFS에서 데이터를 로드 하는 Spark 작업을 만듭니다.
> * 외부 테이블에 결과 쿼리 합니다.

> [!TIP]
> 원한다 면 다운로드 하 고이 자습서의 명령에 대 한 스크립트를 실행할 수 있습니다. 지침은 합니다 [데이터 샘플 풀](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) github입니다.

## <a id="prereqs"></a> 사전 요구 사항

* [Kubernetes에서 빅 데이터 클러스터를 배포](deployment-guidance.md)합니다.
* [Azure Data Studio 및 SQL Server 2019 확장 설치](deploy-big-data-tools.md)합니다.
* [클러스터에 샘플 데이터 로드](#sampledata)합니다.

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-in-the-data-pool"></a>데이터 풀에서 외부 테이블 만들기

다음 단계에서는 명명 된 데이터 풀의 외부 테이블을 만듭니다 **web_clickstreams_spark_results**합니다. 이 표에서 사용할 수 있습니다 다음 위치로 데이터를 수집 하는 방법에 대 한 빅 데이터 클러스터에.

1. Azure Data Studio, 빅 데이터 클러스터의 마스터 SQL Server 인스턴스에 연결 합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결할](deploy-big-data-tools.md#master)합니다.

1. 연결을 두 번 클릭 합니다 **서버** 창 마스터 SQL Server 인스턴스에 대 한 서버 대시보드를 표시 합니다. 선택 **새 쿼리**합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 명명 된 외부 테이블을 만듭니다 **web_clickstreams_spark_results** 데이터 풀에 있습니다. `SqlDataPool` 데이터 원본은 모든 빅 데이터 클러스터의 마스터 인스턴스를 사용할 수 있는 특수 데이터 원본 형식입니다.

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
  
1. CTP 2.1에서 데이터 풀을 만드는 비동기 되었지만 아직 완료 될 때 확인 방법이 있습니다. 계속 하기 전에 데이터 풀 생성 되도록 하려면 2 분을 기다립니다.

## <a name="start-a-spark-streaming-job"></a>Spark 스트리밍 작업 시작

다음 단계는 Spark 스트리밍 (HDFS) 저장소 풀에서 웹 클릭 동향 데이터를 로드 하는 작업을 만들려면 데이터 풀에서 만든 외부 테이블에입니다.

1. Azure Data Studio, 빅 데이터 클러스터의 HDFS/Spark 게이트웨이에 연결 합니다. 자세한 내용은 [HDFS/Spark 게이트웨이에 연결할](deploy-big-data-tools.md#hdfs)합니다.

1. HDFS/Spark 게이트웨이 연결을 두 번 클릭 합니다 **서버** 창입니다. 선택한 **새 Spark 작업**합니다.

   ![새 Spark 작업](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. 에 **새 작업** 창에 이름을 입력 합니다 **작업 이름** 필드입니다.

1. 에 **Jar/py 파일** 드롭다운 목록에서 선택 **HDFS**합니다. 다음 jar 파일 경로 입력 합니다.

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. 에 **인수** 필드에서 마스터 SQL Server 인스턴스를 암호를 지정 하는 다음 텍스트를 입력 합니다는 `<your_password>` 자리 표시자입니다. 

   ```text
   mssql-master-pool-0.service-master-pool 1433 sa <your_password> sales web_clickstreams_spark_results hdfs:///clickstream_data csv false
   ```

   다음 표에서 각 인수를 설명합니다.

   | 인수 | Description |
   |---|---|
   | 서버 이름(server name) | 테이블 스키마를 읽는 SQL Server 사용 |
   | 포트 번호 | SQL Server 포트 (기본값 1433)에서 수신 대기 |
   | username | SQL Server 로그인 사용자 이름 |
   | password | SQL Server 로그인 암호 |
   | 데이터베이스 이름 | 대상 데이터베이스 |
   | 외부 테이블 이름 | 결과에 사용할 테이블 |
   | 스트리밍에 대 한 원본 디렉터리 | 와 같은 전체 URI 여야 합니다 "hdfs: / / / clickstream_data" |
   | 입력된 형식 | "Csv", "parquet" 또는 "json" 수 있습니다. |
   | 검사점을 사용 하도록 설정 | true 또는 false |

1. 키를 눌러 **제출** 작업을 제출 합니다.

   ![Spark 작업 제출](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>데이터를 쿼리 합니다.

다음 단계는 Spark 스트리밍 작업 데이터를 HDFS에서 풀으로 로드 데이터를 표시 합니다.

1. 수집 된 데이터를 쿼리 하기 전에 출력을 살펴 작업 기록에서 볼 수 있듯이 작업을 완료 했습니다.

   ![Spark 작업 기록](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 이 자습서의 시작 부분에 열리는 SQL Server 마스터 인스턴스 쿼리 창으로 돌아갑니다...

1. 수집 된 데이터를 검사 하려면 다음 쿼리를 실행 합니다.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>정리

이 자습서에서 만든 데이터베이스 개체를 제거 하려면 다음 명령을 사용 합니다.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>다음 단계

Azure Data Studio에서 샘플 notebook을 실행 하는 방법에 알아봅니다.
> [!div class="nextstepaction"]
> [샘플 노트북을 실행 합니다.](tutorial-notebook-spark.md)
