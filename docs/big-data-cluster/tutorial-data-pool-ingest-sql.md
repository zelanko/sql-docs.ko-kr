---
title: SQL Server 데이터 풀에 데이터 수집
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 데이터 풀로 데이터를 수집하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f2ae96a04da69835b4b13886637cf87e62996b57
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653317"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>자습서: Transact-SQL을 사용하여 SQL Server 데이터 풀에 데이터 수집

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 [데이터 풀](concept-data-pool.md)로 데이터를 수집하는 방법을 보여 줍니다. [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 사용하여 다양한 원본의 데이터를 수집하고 데이터 풀 인스턴스 간에 분산할 수 있습니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 데이터 풀에 외부 테이블을 만듭니다.
> * 샘플 웹 클릭스트림 데이터를 데이터 풀 테이블에 삽입합니다.
> * 데이터 풀 테이블의 데이터를 로컬 테이블에 조인합니다.

> [!TIP]
> 원하는 경우 이 자습서의 명령에 대한 스크립트를 다운로드하여 실행할 수 있습니다. 자세한 내용은 GitHub에서 [데이터 풀 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)을 참조하세요.

## <a id="prereqs"></a> 사전 요구 사항

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>데이터 풀에 외부 테이블 만들기

다음 단계에서는 **web_clickstream_clicks_data_pool**이라는 데이터 풀에 외부 테이블을 만듭니다. 그런 다음, 이 테이블을 빅 데이터 클러스터로 데이터를 수집하는 위치로 사용할 수 있습니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)을 참조하세요.

1. **서버** 창에서 연결을 두 번 클릭하여 SQL Server 마스터 인스턴스의 서버 대시보드를 표시합니다. **새 쿼리**를 선택합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 다음 Transact-SQL 명령을 실행하여 마스터 인스턴스의 **Sales** 데이터베이스로 컨텍스트를 변경합니다.

   ```sql
   USE Sales
   GO
   ```

1. 데이터 풀에 외부 데이터 원본이 아직 없는 경우 새로 만듭니다.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 데이터 풀에 이름이 **web_clickstream_clicks_data_pool**인 외부 테이블을 만듭니다.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. CTP 3.1에서 데이터 풀 만들기는 비동기식으로 진행되지만 이미 완료되었는지 여부를 확인할 방법이 없습니다. 데이터 풀이 생성될 때까지 2분 정도 기다렸다가 계속 진행합니다.

## <a name="load-data"></a>데이터 로드

다음 단계에서는 이전 단계에서 만든 외부 테이블을 사용하여 샘플 웹 클릭스트림 데이터를 데이터 풀에 수집합니다.

1. `INSERT INTO` 문을 사용하여 쿼리의 결과를 데이터 풀(**web_clickstream_clicks_data_pool** 외부 테이블)에 삽입합니다.

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. 두 개의 SELECT 쿼리를 사용하여 삽입된 데이터를 조사합니다.

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>데이터 쿼리

데이터 풀의 쿼리에서 생성된 저장된 결과를 **Sales** 테이블의 로컬 데이터와 조인합니다.

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>정리

다음 명령을 사용하여 이 자습서에서 만든 데이터베이스 개체를 제거합니다.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>다음 단계

Spark 작업을 사용하여 데이터 풀에 데이터를 수집하는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [Spark 작업을 사용하여 데이터 수집](tutorial-data-pool-ingest-spark.md)
