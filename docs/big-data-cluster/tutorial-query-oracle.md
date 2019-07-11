---
title: Oracle에서 데이터를 외부 쿼리
titleSuffix: SQL Server big data clusters
description: 이 자습서에는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 Oracle 데이터를 쿼리 하는 방법을 보여 줍니다. Oracle에서 데이터에 대 한 외부 테이블을 만들고 쿼리를 실행 합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
manager: jroth
ms.date: 12/12/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8da0248eb4e31e25503efad9797f4c58243f3b5e
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728330"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에서 Oracle 쿼리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 자습서에는 SQL Server 2019 빅 데이터 클러스터에서 Oracle 데이터를 쿼리 하는 방법을 보여 줍니다. 이 자습서를 실행 하려면 Oracle 서버에 액세스할 수 있도록 해야 합니다. 액세스 없으면 외부 데이터 원본 SQL Server 빅 데이터 클러스터에 대 한 데이터 가상화의 작동 방식을 이해가이 자습서에 제공할 수 있습니다.

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * 외부 Oracle 데이터베이스에서 데이터에 대 한 외부 테이블을 만듭니다.
> * 높은 가치의 데이터를 사용 하 여이 데이터 마스터 인스턴스를 조인 합니다.

> [!TIP]
> 원한다 면 다운로드 하 고이 자습서의 명령에 대 한 스크립트를 실행할 수 있습니다. 지침은 합니다 [데이터 가상화 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) github입니다.

## <a id="prereqs"></a> 사전 요구 사항

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Oracle 테이블 만들기

다음 단계를 라는 샘플 테이블을 만들어 `INVENTORY` Oracle에서.

1. Oracle 인스턴스 및이 자습서에 사용 하려는 데이터베이스에 연결 합니다.

1. 만들려면 다음 문을 실행 하 여 `INVENTORY` 테이블:

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. 콘텐츠를 가져와 합니다 **inventory.csv** 이 테이블에는 파일입니다. 샘플 생성 스크립트에서이 파일을 만든 합니다 [필수 구성 요소](#prereqs) 섹션입니다.

## <a name="create-an-external-data-source"></a>외부 데이터 원본 만들기

먼저는 Oracle 서버에 액세스할 수 있는 외부 데이터 원본을 만드는 것입니다.

1. Azure Data Studio, 빅 데이터 클러스터의 마스터 SQL Server 인스턴스에 연결 합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결할](connect-to-big-data-cluster.md#master)합니다.

1. 연결을 두 번 클릭 합니다 **서버** 창 마스터 SQL Server 인스턴스에 대 한 서버 대시보드를 표시 합니다. 선택 **새 쿼리**합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 컨텍스트를 변경 하려면 다음 TRANSACT-SQL 명령을 실행 합니다 **Sales** 마스터 인스턴스에 있는 데이터베이스입니다.

   ```sql
   USE Sales
   GO
   ```

1. Oracle 서버에 연결 하는 데이터베이스 범위 자격 증명을 만듭니다. 다음 문에서 Oracle 서버에 적절 한 자격 증명을 제공 합니다.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Oracle 서버를 가리키는 외부 데이터 원본을 만듭니다.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>외부 테이블 만들기

다음으로 명명 된 외부 테이블을 만듭니다 **iventory_ora** 조치는 `INVENTORY` Oracle 서버에는 테이블입니다.

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> 테이블 이름과 열 이름은 ANSI SQL Oracle에 대해 쿼리 하는 동안 따옴표 붙은 식별자를 사용 합니다. 결과적으로 이름은 대/소문자 구분 됩니다. Oracle 메타 데이터의 테이블 및 열 이름 대/소문자와 일치 하는 외부 테이블 정의의 이름을 지정 하는 것이 반드시 합니다.

## <a name="query-the-data"></a>데이터를 쿼리 합니다.

데이터를 조인 하려면 다음 쿼리를 실행 합니다 `iventory_ora` 외부 테이블과 로컬에서 테이블 `Sales` 데이터베이스입니다.

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>정리

이 자습서에서 만든 데이터베이스 개체를 제거 하려면 다음 명령을 사용 합니다.

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>다음 단계

데이터 풀에 데이터를 수집 하는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [데이터 풀에 데이터 로드](tutorial-data-pool-ingest-sql.md)
