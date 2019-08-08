---
title: 스토리지 풀에서 HDFS 데이터 쿼리
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 SQL Server 2019 빅 데이터 클러스터(미리 보기)에서 HDFS 데이터를 쿼리하는 방법을 보여 줍니다. 스토리지 풀의 데이터에 대해 외부 테이블을 만든 다음, 쿼리를 실행합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 77e9e7ddcbca9b397ab4f1ca85ff0d6bada93171
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957702"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에서 HDFS 쿼리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에서는 SQL Server 2019 빅 데이터 클러스터(미리 보기)에서 HDFS 데이터를 쿼리하는 방법을 보여 줍니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 빅 데이터 클러스터의 HDFS 데이터를 가리키는 외부 테이블을 만듭니다.
> * 이 데이터를 마스터 인스턴스의 중요 데이터와 조인합니다.

> [!TIP]
> 원하는 경우 이 자습서의 명령에 대한 스크립트를 다운로드하여 실행할 수 있습니다. 자세한 내용은 GitHub의 [데이터 가상화 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)을 참조하세요.

## <a id="prereqs"></a> 사전 요구 사항

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>HDFS에 대한 외부 테이블 만들기

스토리지 풀은 HDFS에 저장된 CSV 파일의 웹 클릭스트림 데이터를 포함합니다. 다음 단계를 사용하여 해당 파일의 데이터에 액세스할 수 있는 외부 테이블을 정의합니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)을 참조하세요.

1. **서버** 창에서 연결을 두 번 클릭하여 SQL Server 마스터 인스턴스의 서버 대시보드를 표시합니다. **새 쿼리**를 선택합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

1. 다음 Transact-SQL 명령을 실행하여 마스터 인스턴스의 **Sales** 데이터베이스로 컨텍스트를 변경합니다.

   ```sql
   USE Sales
   GO
   ```

1. HDFS에서 읽을 CSV 파일의 형식을 정의합니다. F5 키를 눌러 문을 실행합니다.

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

1. 스토리지 풀에 외부 데이터 원본이 아직 없는 경우 새로 만듭니다.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   BEGIN
     CREATE EXTERNAL DATA SOURCE SqlStoragePool
     WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   END
   ```

1. 스토리지 풀에서 `/clickstream_data`를 읽을 수 있는 외부 테이블을 만듭니다. **SqlStoragePool**은 빅 데이터 클러스터의 마스터 인스턴스에서 액세스할 수 있습니다.

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>데이터 쿼리

다음 쿼리를 실행하여 `web_clickstream_hdfs` 외부 테이블의 HDFS 데이터를 로컬 `Sales` 데이터베이스의 관계형 데이터와 조인합니다.

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>정리

다음 명령을 사용하여 이 자습서에서 사용되는 외부 테이블을 제거합니다.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에서 Oracle을 쿼리하는 방법을 알아보려면 다음 문서로 이동합니다.
> [!div class="nextstepaction"]
> [Oracle에서 외부 데이터 쿼리](tutorial-query-oracle.md)
