---
title: Spark 작업을 사용하여 데이터 수집
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 Azure Data Studio에서 Spark 작업을 사용 하 여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 데이터 풀에 데이터를 수집 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6ebcc95d48f894ff8cef9771946130fc67216a45
ms.sourcegitcommit: c8b8101c62a6af3e4a7244683e3f34f7189c150f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2019
ms.locfileid: "73182636"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>자습서: Spark 작업을 사용 하 여 SQL Server 데이터 풀로 데이터 수집

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 Spark 작업을 사용 하 여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 [데이터 풀](concept-data-pool.md) 에 데이터를 로드 하는 방법을 보여 줍니다. 

이 자습서에서는 다음 작업 방법을 알아봅니다.

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
   USE Sales
   GO
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

다음 단계는 스토리지 풀(HDFS)에서 데이터 풀에 만든 외부 테이블로 웹 클릭 스트림 데이터를 로드하는 Spark 스트리밍 작업을 만드는 것입니다. 이 데이터는 [빅 데이터 클러스터에 샘플 데이터를 로드](tutorial-load-sample-data.md)하는/clickstream_data에 추가 되었습니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 마스터 인스턴스에 연결합니다. 자세한 내용은 [빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

2. 새 노트북을 만들고 Spark |를 선택 합니다. 커널로 Scala.

3. Spark 수집 작업 실행
   1. Spark-SQL 커넥터 매개 변수 구성
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",IntegerType,true), StructField("wcs_click_time_sk",IntegerType,true), StructField("wcs_sales_sk",IntegerType,true), StructField("wcs_item_sk",IntegerType,true), 
      StructField("wcs_web_page_sk",IntegerType,true), StructField("wcs_user_sk",IntegerType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. Spark 작업 정의 및 실행
      * 각 작업은 readStream 및 writeStream의 두 부분으로 구성 됩니다. 아래에서 위에 정의 된 스키마를 사용 하 여 데이터 프레임을 만든 다음 데이터 풀의 외부 테이블에 기록 합니다.
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.processAllAvailable()
      query.awaitTermination(40000)
      ```
## <a name="query-the-data"></a>데이터 쿼리

다음 단계에서는 Spark 스트리밍 작업이 HDFS에서 데이터 풀로 데이터를 로드하는 방법을 보여 줍니다.

1. 수집 데이터를 쿼리 하기 전에 Yarn App ID, Spark UI 및 드라이버 로그를 포함 하 여 Spark 실행 상태를 확인 합니다.

   ![Spark 실행 세부 정보](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. 이 자습서의 시작 부분에서 열었던 SQL Server 마스터 인스턴스 쿼리 창으로 돌아갑니다.

1. 다음 쿼리를 실행하여 수집된 데이터를 검사합니다.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. Spark에서 데이터를 쿼리할 수도 있습니다. 예를 들어 아래 코드는 테이블의 레코드 수를 인쇄 합니다.
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
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
