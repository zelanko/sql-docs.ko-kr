---
title: 실시간 운영 분석을 위한 Columnstore 시작 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: quickstart
ms.assetid: e1328615-6b59-4473-8a8d-4f360f73187d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 907cd0278119351c9bfabf2c2c64e514a7840c7a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531540"
---
# <a name="get-started-with-columnstore-for-real-time-operational-analytics"></a>실시간 운영 분석을 위한 Columnstore 시작
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  SQL Server 2016에는 분석 워크로드와 OLTP 워크로드를 같은 데이터베이스 테이블에서 동시에 실행하는 기능인 실시간 운영 분석이 도입되었습니다. 분석을 실시간으로 실행하는 것 외에 ETL 및 데이터 웨어하우스에 대한 필요성도 제거할 수 있습니다.  
  
## <a name="real-time-operational-analytics-explained"></a>실시간 운영 분석 설명  
 기존에는 운영 워크로드(즉, OLTP)와 분석 워크로드에 사용되는 별도의 시스템이 있었습니다. 이러한 시스템에서는 ETL(추출, 변환 및 로드) 작업이 운영 저장소에서 분석 저장소로 데이터를 정기적으로 이동합니다. 분석 데이터는 일반적으로 데이터 웨어하우스나 분석 쿼리 실행 전용 데이터 마트에 저장됩니다. 이 솔루션은 표준이었지만 다음 세 가지 주요 문제가 있었습니다.  
  
-   **복잡성.** ETL을 구현하려면 특히 수정된 행만 로드하는 데 상당한 코딩이 필요할 수 있습니다. 따라서 수정된 행을 식별하기가 복잡할 수 있습니다.  
  
-   **비용이 듭니다.** ETL을 구현하려면 추가 하드웨어 및 소프트웨어 라이선스 구매 비용이 듭니다.  
  
-   **데이터 대기 시간.** ETL을 구현하면 분석을 실행하는 데 지연 시간이 추가됩니다. 예를 들어 ETL 작업이 각 업무일 종료 시간에 실행되는 경우 분석 쿼리는 최소한 하루 이전의 데이터에서 실행됩니다. 많은 기업에서 이러한 지연은 허용되지 않습니다. 실시간 데이터 분석에 의존하기 때문입니다. 예를 들어 사기 감지에는 운영 데이터에 대한 실시간 분석이 필요합니다.  
  
 ![실시간 운영 분석 개요](../../relational-databases/indexes/media/real-time-operational-analytics-overview.png "real-time operational analytics overview")  
  
 실시간 운영 분석은 이러한 과제에 대한 솔루션을 제공합니다.   
        분석 워크로드와 OLTP 워크로드가 동일한 기본 테이블에서 실행되는 경우에는 시간 지연이 없습니다.   실시간 분석을 사용할 수 있는 시나리오에서는 ETL이 필요 없고 별도의 데이터 웨어하우스를 구매하고 유지 관리할 필요가 없으므로 비용 및 복잡성이 크게 줄어듭니다.  
  
> [!NOTE]  
>  실시간 운영 분석은 운영 워크로드와 분석 워크로드를 둘 다 실행할 수 있는 ERP(전사적 자원 관리) 응용 프로그램과 같은 단일 데이터 원본 시나리오를 대상으로 합니다. 이는 분석 워크로드를 실행하기 전에 여러 원본의 데이터를 통합해야 하거나 큐브와 같은 사전 집계된 데이터의 사용으로 극단적인 분석 성능이 필요한 경우에는 별도 데이터 웨어하우스에 대한 필요성을 대체하지 못합니다.  
  
 실시간 분석에서는 rowstore 테이블에서 업데이트 가능한 columnstore 인덱스를 사용합니다.  Columnstore 인덱스는 데이터의 복사본을 유지하므로 OLTP 워크로드와 분석 워크로드가 데이터의 개별 복사본에 대해 실행됩니다. 이는 동시에 실행되는 두 워크로드의 성능 영향을 최소화합니다.  SQL Server는 인덱스 변경 내용을 자동으로 유지 관리하므로 OLTP 변경 내용이 분석을 위해 항상 최신 상태로 유지됩니다. 이 디자인에서는 최신 데이터에서 실시간으로 분석을 실행하는 것이 가능하고 유용합니다. 이는 디스크 기반 테이블과 메모리 최적화 테이블 모두에 적용됩니다.  
  
## <a name="get-started-example"></a>시작 예제  
 실시간 분석을 시작하려면  
  
1.  운영 스키마에서 분석에 필요한 데이터가 포함된 테이블을 식별합니다.  
  
2.  각 테이블에 대해 주로 OLTP 워크로드에 대한 기존 분석을 가속화하도록 디자인된 모든 btree 인덱스를 삭제합니다. 이를 단일 columnstore 인덱스로 바꿉니다.  그러면 유지 관리할 인덱스가 적으므로 OLTP 워크로드의 전반적인 성능이 향상됩니다.  
  
    ```  
    --This example creates a nonclustered columnstore index on an existing OLTP table.  
    --Create the table  
    CREATE TABLE t_account (  
        accountkey int PRIMARY KEY,  
        accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int  
    );  
  
    --Create the columnstore index with a filtered condition  
    CREATE NONCLUSTERED COLUMNSTORE INDEX account_NCCI   
    ON t_account (accountkey, accountdescription, unitsold)   
    ;  
  
    ```  
  
     메모리 내 테이블의 columnstore 인덱스는 메모리 내 OLTP 및 메모리 내 columnstore 기술을 통합하여 OLTP 및 분석 워크로드에 대한 뛰어난 성능을 제공함으로써 운영 분석을 지원합니다. 메모리 내 테이블의 columnstore 인덱스는 모든 열을 포함해야 합니다.  
  
    ```  
    -- This example creates a memory-optimized table with a columnstore index.  
    CREATE TABLE t_account (  
        accountkey int NOT NULL PRIMARY KEY NONCLUSTERED,  
        Accountdescription nvarchar (50),  
        accounttype nvarchar(50),  
        unitsold int,  
        INDEX t_account_cci CLUSTERED COLUMNSTORE  
        )  
        WITH (MEMORY_OPTIMIZED = ON );  
    GO  
  
    ```  
  
3.  이 작업만 수행하면 됩니다!  
  
 이제 응용 프로그램을 변경하지 않고도 실시간 운영 분석을 실행할 준비가 완료되었습니다.  분석 쿼리는 columnstore 인덱스에 대해 실행되고 OLTP 작업은 OLTP btree 인덱스에 대해 계속 실행됩니다. OLTP 워크로드는 계속 수행되지만 columnstore 인덱스를 유지하기 위해 약간의 추가 오버헤드가 발생합니다. 다음 섹션에서 성능 최적화를 참조하세요.  
  
## <a name="blog-posts"></a>블로그 게시물  
 실시간 운영 분석에 대해 자세히 알아보려면 Sunil Agarwal의 블로그 게시물을 읽어 보세요.  이 블로그 게시물을 먼저 살펴보면 성능 팁 섹션을 보다 쉽게 이해할 수 있습니다.  
  
-   [실시간 운영 분석에 대한 비즈니스 사례](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)  
  
-   [실시간 운영 분석에 비클러스터형 columnstore 인덱스 사용](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)  
  
-   [비클러스터형 columnstore 인덱스를 사용하는 간단한 예제](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)  
  
-   [SQL Server가 트랜잭션 워크로드에서 비클러스터형 columnstore 인덱스를 유지 관리하는 방법](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)  
  
-   [필터링된 인덱스를 사용하여 비클러스터형 columnstore 인덱스 유지 관리의 영향 최소화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)  
  
-   [압축 지연을 사용하여 비클러스터형 columnstore 인덱스 유지 관리의 영향 최소화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)  
  
-   [압축 지연 - 성능 수치를 사용하여 비클러스터형 columnstore 인덱스 유지 관리의 영향 최소화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)  
  
-   [메모리 최적화 테이블을 사용한 실시간 운영 분석](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)  
  
-   [Columnstore 인덱스에서 인덱스 조각화 최소화](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
  
-   [Columnstore 인덱스와 행 그룹에 대한 병합 정책](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
## <a name="performance-tip-1-use-filtered-indexes-to-improve-query-performance"></a>성능 팁 1: 필터링된 인덱스를 사용하여 쿼리 성능 향상  
 실시간 운영 분석을 실행하면 OLTP 워크로드의 성능이 영향을 받을 수 있습니다.  이 영향을 최소화해야 합니다. 아래 예제에서는 실시간 분석을 제공하면서 필터링된 인덱스를 사용하여 비클러스터형 columnstore 인덱스가 트랜잭션 워크로드에 미치는 영향을 최소화하는 방법을 보여 줍니다.  
  
 운영 워크로드에서 비클러스터형 columnstore 인덱스 유지 관리 오버헤드를 최소화하려면 필터링된 조건을 사용하여 *웜* 또는 느린 변경 데이터에만 비클러스터형 columnstore 인덱스를 만들면 됩니다. 예를 들어 주문 관리 응용 프로그램에서 이미 배송된 주문에 대한 비클러스터형 columnstore 인덱스를 만들 수 있습니다. 주문이 배송된 후에는 변경 내용이 거의 없으므로 웜 데이터로 간주할 수 있습니다. 필터링된 인덱스를 사용하는 경우 비클러스터형 columnstore 인덱스의 데이터에 필요한 업데이트가 적으므로 트랜잭션 워크로드에 대한 영향을 감소합니다.  
  
 분석 쿼리는 실시간 분석을 제공하는 데 필요한 경우 웜 데이터와 핫 데이터 모두에 투명하게 액세스합니다. 운영 워크로드의 중요한 부분이 '핫' 데이터에 연결되어 있는 경우 이러한 작업에는 columnstore 인덱스의 추가 유지 관리가 필요하지 않습니다. 필터링된 인덱스 정의에 사용된 열에서 rowstore 클러스터형 인덱스를 유지하는 것이 가장 좋습니다.   SQL Server는 클러스터형 인덱스를 사용하여 필터링된 조건을 충족하지 않는 행을 신속하게 검색합니다. 이 클러스터형 인덱스가 없으면 분석 쿼리의 성능을 크게 저하시킬 수 있는 이러한 행을 찾기 위해 rowstore 테이블의 전체 검색을 수행해야 합니다. 클러스터형 인덱스가 없는 경우 필터링된 비클러스터형 btree 보조 인덱스를 만들어 이러한 행을 식별할 수 있지만 비클러스터형 btree 인덱스를 통해 큰 범위의 행에 액세스하는 것은 비용이 많이 들기 때문에 이는 권장되지 않습니다.  
  
> [!NOTE]  
>  필터링된 비클러스터형 columnstore 인덱스는 디스크 기반 테이블에서만 지원됩니다. 메모리 최적화 테이블에서는 지원되지 않습니다.  
  
### <a name="example-a-access-hot-data-from-btree-index-warm-data-from-columnstore-index"></a>예제 A: btree 인덱스에서 핫 데이터에 액세스하고, columnstore 인덱스에서 웜 데이터에 액세스  
 이 예제에서는 필터링된 조건(accountkey > 0)을 사용하여 columnstore 인덱스에 포함할 행을 설정합니다. 자주 변경되는 “핫” 데이터는 btree 인덱스에서 액세스하고 보다 안정적인 “웜” 데이터는 columnstore 인덱스에서 액세스하도록 필터링된 조건 및 후속 쿼리를 디자인하는 것이 목적입니다.  
  
 ![웜 및 핫 데이터에 대한 결합된 인덱스](../../relational-databases/indexes/media/de-columnstore-warmhotdata.png "Combined indexes for warm and hot data")  
  
> [!NOTE]  
>  쿼리 최적화 프로그램에서는 경우에 따라 쿼리 계획에 대해 columnstore 인덱스를 선택할 수 있습니다. 필터링된 columnstore 인덱스를 선택한 경우 쿼리 최적화 프로그램은 실시간 분석을 허용하기 위해 columnstore 인덱스의 행과 필터링된 조건을 충족하지 않는 행을 모두 투명하게 통합합니다. 이는 인덱스에 있는 행으로 제한되는 쿼리에서만 사용할 수 있는 일반 비클러스터형 필터링된 인덱스와 다릅니다.  
  
```  
--Use a filtered condition to separate hot data in a rowstore table  
-- from "warm" data in a columnstore index.  
  
-- create the table  
CREATE TABLE  orders (  
         AccountKey         int not null,  
         Customername       nvarchar (50),  
        OrderNumber         bigint,  
        PurchasePrice       decimal (9,2),  
        OrderStatus         smallint not null,  
        OrderStatusDesc     nvarchar (50))  
  
-- OrderStatusDesc  
-- 0 => 'Order Started'  
-- 1 => 'Order Closed'  
-- 2 => 'Order Paid'  
-- 3 => 'Order Fullfillment Wait'  
-- 4 => 'Order Shipped'  
-- 5 => 'Order Received'  
  
CREATE CLUSTERED INDEX  orders_ci ON orders(OrderStatus)  
  
--Create the columnstore index with a filtered condition  
CREATE NONCLUSTERED COLUMNSTORE INDEX orders_ncci ON orders  (accountkey, customername, purchaseprice, orderstatus)  
where orderstatus = 5  
;  
  
-- The following query returns the total purchase done by customers for items > $100 .00  
-- This query will pick  rows both from NCCI and from 'hot' rows that are not part of NCCI  
SELECT top 5 customername, sum (PurchasePrice)  
FROM orders  
WHERE purchaseprice > 100.0   
Group By customername  
```  
  
 분석 쿼리는 다음 쿼리 계획으로 실행됩니다. 필터링된 조건을 충족하지 않는 행에는 클러스터형 btree 인덱스를 통해 액세스하는 것을 볼 수 있습니다.  
  
 ![쿼리 계획](../../relational-databases/indexes/media/query-plan-columnstore.png "Query plan")  
  
 [필터링된 비클러스터형 columnstore 인덱스](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)에 대한 자세한 내용은 블로그를 참조하세요.  
  
## <a name="performance-tip-2-offload-analytics-to-always-on-readable-secondary"></a>성능 팁 2: 분석을 Always On 읽기 가능한 보조로 오프로드  
 필터링된 columnstore 인덱스를 사용하여 columnstore 인덱스 유지 관리를 최소화할 수 있지만 분석 쿼리에는 여전히 운영 워크로드 성능에 영향을 주는 많은 컴퓨팅 리소스(CPU, IO, 메모리)가 필요할 수 있습니다. 업무에 중요한 워크로드에는 대부분 Always On 구성을 사용하는 것이 좋습니다. 이 구성에서는 분석 실행을 읽기 가능한 보조로 오프로드하여 그 영향을 제거할 수 있습니다.  
  
## <a name="performance-tip-3-reducing-index-fragmentation-by-keeping-hot-data-in-delta-rowgroups"></a>성능 팁 3: 델타 행 그룹에서 핫 데이터를 유지하여 인덱스 조각화 줄이기  
 워크로드에서 압축된 행을 업데이트/삭제하는 경우 columnstore 인덱스가 있는 테이블이 크게 조각화(즉, 삭제된 행)될 수 있습니다. 조각화된 columnstore 인덱스는 메모리/저장소의 비효율적인 사용률을 초래합니다. 리소스의 비효율적인 사용 외에 분석 쿼리 성능도 저하됩니다. 이는 결과 집합에서 삭제된 행을 필터링해야 하고 추가 IO가 필요하기 때문입니다.  
  
 삭제된 행은 REORGANIZE 명령을 사용하여 인덱스 조각 모음을 실행하거나 전체 테이블 또는 영향을 받는 패턴에서 columnstore 인덱스를 다시 작성할 때까지 물리적으로 제거되지 않습니다. REORGANIZE와 인덱스 REBUILD 둘 다 워크로드에 사용될 수 있는 리소스를 차지하는 부담이 큰 작업입니다. 또한 행이 너무 일찍 압축된 경우 업데이트로 인해 여러 번 다시 압축해야 할 수 있으므로 압축 오버헤드가 낭비됩니다.  
COMPRESSION_DELAY 옵션을 사용하여 인덱스 조각화를 최소화할 수 있습니다.  
  
```  
  
-- Create a sample table  
create table t_colstor (  
               accountkey                      int not null,  
               accountdescription              nvarchar (50) not null,  
               accounttype                     nvarchar(50),  
               accountCodeAlternatekey         int)  
  
-- Creating nonclustered columnstore index with COMPRESSION_DELAY. The columnstore index will keep the rows in closed delta rowgroup for 100 minutes   
-- after it has been marked closed  
CREATE NONCLUSTERED COLUMNSTORE index t_colstor_cci on t_colstor (accountkey, accountdescription, accounttype)   
                       WITH (DATA_COMPRESSION= COLUMNSTORE, COMPRESSION_DELAY = 100);  
  
;  
```  
  
 [압축 지연](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)에 대한 자세한 내용은 블로그를 참조하세요.  
  
 권장 모범 사례는 다음과 같습니다.  
  
-   **삽입/쿼리 워크로드:** 워크로드가 주로 데이터를 삽입하고 쿼리하는 경우 기본 COMPRESSION_DELAY(0)가 권장되는 옵션입니다. 100만 개의 행이 단일 델타 행 그룹에 삽입되면 새로 삽입된 행이 압축됩니다.  
    이러한 워크로드의 예로는 (a) 기존 DW 워크로드 (b) 웹 응용 프로그램에서 클릭 패턴을 분석해야 하는 경우의 클릭 스트림 분석 등이 있습니다.  
  
-   **OLTP 워크로드:** 워크로드가 DMV에 집중된 경우(즉, 주로 업데이트, 삭제 및 삽입 수행) DMV sys를 검사하면 columnstore 인덱스 조각화를 볼 수 있습니다. dm_db_column_store_row_group_physical_stats. 최근에 압축된 행 그룹에서 삭제된 것으로 표시된 행 수가 10%를 초과하는 경우 COMPRESSION_DELAY 옵션을 사용하여 행이 압축에 적합하게 될 때 시간 지연을 추가할 수 있습니다. 예를 들어 워크로드에 대해 새로 삽입된 행이 60분 동안 '핫' 상태로 유지되는 경우(즉, 여러 번 업데이트되는 경우) COMPRESSION_DELAY가 60이 되도록 선택해야 합니다.  
  
 대부분의 고객은 아무 작업도 수행하지 않아도 됩니다. COMPRESSION_DELAY 옵션의 기본값이 적용됩니다.  
고급 사용자의 경우 아래 쿼리를 실행하여 지난 7일 동안 삭제된 행의 비율(%)을 수집하는 것이 좋습니다.  
  
```  
SELECT row_group_id,cast(deleted_rows as float)/cast(total_rows as float)*100 as [% fragmented], created_time  
FROM sys. dm_db_column_store_row_group_physical_stats  
WHERE object_id = object_id('FactOnlineSales2')   
             AND  state_desc='COMPRESSED'   
             AND deleted_rows>0   
             AND created_time > GETDATE() - 7  
ORDER BY created_time DESC  
```  
  
 압축된 행 그룹에서 삭제된 행 수가 20%를 초과하여 이전 행 그룹이 5% 미만의 변형으로 안정된 경우(콜드 행 그룹이라고 함) COMPRESSION_DELAY = (youngest_rowgroup_created_time –  current_time)을 설정합니다. 이 접근 방식은 안정적이고 상대적으로 유형이 같은 워크로드에 가장 적합합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)   
 [Columnstore 인덱스 데이터 로드](../../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [Columnstore 인덱스 쿼리 성능](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [데이터 웨어하우스용 Columnstore 인덱스](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [Columnstore 인덱스 조각 모음](../../relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  
