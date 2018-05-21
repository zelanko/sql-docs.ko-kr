---
title: 인덱스 다시 구성 및 다시 빌드 | Microsoft 문서
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
caps.latest.revision: 70
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d23489e55a793e63b6b3bfcb8c2a71708a2bb567
ms.sourcegitcommit: bac61a04d11fdf61deeb03060e66621c0606c074
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
---
# <a name="reorganize-and-rebuild-indexes"></a>인덱스 다시 구성 및 다시 작성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> [!NOTE]
> 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 관련된 콘텐츠는 [인덱스 다시 구성 및 다시 작성](https://msdn.microsoft.com/en-US/library/ms189858(SQL.120).aspx)을 참조하세요.

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 조각난 인덱스를 다시 구성하거나 다시 작성하는 방법에 대해 설명합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 기본 데이터에 삽입, 업데이트 또는 삭제 작업을 수행할 때마다 인덱스를 자동으로 수정합니다. 이러한 수정이 거듭되면 시간이 흐름에 따라 인덱스의 정보가 조각화되어 데이터베이스 내에 흩어지게 될 수 있습니다. 조각화는 키 값을 기준으로 하는 인덱스의 논리적 페이지 순서가 데이터 파일 내의 물리적 순서와 일치하지 않을 때 나타납니다. 심하게 조각화된 인덱스는 쿼리 성능을 저하시키고 응용 프로그램이 응답을 늦출 수 있습니다(특히 검사 작업).  
  
인덱스를 다시 구성하거나 다시 작성하여 인덱스 조각화 문제를 해결할 수 있습니다. 파티션 구성표에 작성한 분할된 인덱스의 경우 전체 인덱스나 인덱스의 단일 파티션에 이러한 방법 중 하나를 사용할 수 있습니다.    
인덱스를 다시 작성하면 이 인덱스가 삭제된 다음 다시 생성됩니다. 이렇게 하면 조각화를 제거하고, 지정된 채우기 비율 또는 기존 채우기 비율 설정을 기준으로 페이지를 압축하여 디스크 공간을 회수하고, 인덱스 행을 연속된 페이지로 다시 정렬할 수 있습니다. `ALL`을 지정하면 테이블의 모든 인덱스가 단일 트랜잭션으로 삭제되고 다시 작성됩니다.   
인덱스를 다시 구성할 때는 최소한의 시스템 리소스가 사용됩니다. 이때는 왼쪽에서 오른쪽으로 표시되는 리프 노드의 논리적 순서에 맞도록 리프 수준 페이지를 물리적으로 다시 정렬하여 테이블 및 뷰의 클러스터형 및 비클러스터형 인덱스의 리프 수준에 대한 조각 모음을 수행합니다. 다시 구성 작업을 수행하면 인덱스 페이지도 압축됩니다. 이때 압축은 기존 채우기 비율 값을 기준으로 수행됩니다.  
   
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Fragmentation"></a> 조각화 검색  
사용할 조각 모음 방법을 결정하기 위한 첫 번째 단계는 인덱스를 분석하여 조각화 수준을 확인하는 것입니다. [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)시스템 함수를 사용하여 특정 인덱스, 테이블이나 인덱싱된 뷰의 모든 인덱스, 데이터베이스의 모든 인덱스 또는 모든 데이터베이스 내 모든 인덱스에서 조각화를 검색할 수 있습니다. 분할된 인덱스의 경우 **sys.dm_db_index_physical_stats** 에서도 각 파티션의 조각화 정보를 제공합니다.  
  
**sys.dm_db_index_physical_stats** 함수에서 반환한 결과 집합은 다음 열을 포함합니다.  
  
|Column|설명|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|논리적 조각화(인덱스에서 순서가 잘못된 페이지) 비율|  
|**fragment_count**|인덱스의 조각(물리적으로 연속되는 리프 페이지) 수|  
|**avg_fragment_size_in_pages**|인덱스 한 조각의 평균 페이지 수|  
  
조각화 수준을 파악하고 나면 다음 테이블을 사용하여 가장 적합한 조각화 수정 방법을 결정합니다.  
  
|**avg_fragmentation_in_percent** 값|수정문|  
|-----------------------------------------------|--------------------------|  
|> 5% 및 < = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|  
  
<sup>1</sup> 온라인 또는 오프라인으로 인덱스를 다시 작성할 수 있습니다. 인덱스를 다시 구성하는 과정은 항상 온라인으로 실행됩니다. 다시 구성할 때와 비슷한 가용성을 얻으려면 온라인으로 인덱스를 다시 작성해야 합니다.  
  
이러한 값은 `ALTER INDEX REORGANIZE` 및 `ALTER INDEX REBUILD`를 전환해야 하는 시점을 확인하기 위한 대략적인 지침을 제공합니다. 그러나 실제 값은 경우에 따라 달라질 수 있습니다. 실험을 통해 환경에 맞는 임계값을 확인하는 것이 중요합니다.    
대체로 작은 양의 조각화를 제거할 경우 얻게 되는 이점보다 인덱스를 다시 구성하거나 다시 작성하는 비용이 훨씬 크기 때문에 일반적으로 두 명령 중 하나를 사용하여 매우 낮은 수준의 조각화(5% 미만)를 처리하는 것은 바람직하지 않습니다. `ALTER INDEX REORGANIZE` 및 `ALTER INDEX REBUILD`에 대한 자세한 내용은 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.   
  
> [!NOTE]
> 작은 인덱스는 다시 작성하거나 다시 구성해도 조각화가 줄어들지 않는 경우가 많습니다. 작은 인덱스의 페이지는 종종 혼합 익스텐트에 저장됩니다. 혼합 익스텐트는 최대 8개의 개체가 공유할 수 있으므로 인덱스를 다시 작성하거나 다시 구성한 후에도 작은 인덱스의 조각화가 줄어들지 않을 수 있습니다.  
  
### <a name="Restrictions"></a> 제한 사항  
  
128 익스텐트 이상의 인덱스는 논리적 단계와 물리적 단계로 나누어 다시 작성합니다. 논리적 단계에서는 인덱스에 의해 사용되는 기존 할당 단위가 할당 취소 상태로 표시되며 데이터 행이 복사되어 정렬된 후 다시 작성된 인덱스를 저장하기 위해 생성된 새 할당 단위로 옮겨집니다. 물리적 단계에서는 이전에 할당 취소 상태로 표시된 할당 단위가 백그라운드로 실행되는 짧은 트랜잭션을 통해 물리적으로 삭제됩니다. 이 단계는 잠금을 많이 필요로 하지 않습니다. 익스텐트에 대한 자세한 내용은 [페이지 및 익스텐트 아키텍처 가이드](../../relational-databases/pages-and-extents-architecture-guide.md)를 참조하세요. 
  
`ALTER INDEX REORGANIZE` 문을 사용하면 작업에서 파일 그룹 내의 다른 파일이 아닌 동일한 파일에만 임시 작업 페이지를 할당할 수 있으므로 인덱스가 포함된 데이터 파일에 사용 가능한 공간이 있어야 합니다. 따라서 파일 그룹에 사용 가능한 페이지가 있을 수 있지만 사용자는 여전히 오류 1105: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`이 발생할 수 있습니다.
  
파티션 수가 1,000개를 초과하는 테이블에서 정렬되지 않은 인덱스를 만들거나 다시 작성할 수 있지만 해당 인덱스는 권장되지 않습니다. 그러면 작업 중에 성능이 저하되거나 메모리가 과도하게 소비될 수 있습니다.

인덱스가 위치한 파일 그룹이 오프라인이거나 읽기 전용으로 설정되어 있으면 인덱스를 다시 구성할 수 없습니다. `ALL` 키워드를 지정하면 하나 이상의 인덱스가 오프라인 또는 읽기 전용 파일 그룹에 있을 경우 해당 문이 실패합니다.
  
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 만들거나 업데이트합니다.
> 
> 하지만 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 분할된 인덱스를 만들거나 다시 작성할 때 테이블의 모든 행을 검사하여 통계를 만들거나 업데이트하지 않습니다. 대신 쿼리 최적화 프로그램에서 기본 샘플링 알고리즘을 사용하여 이러한 통계를 생성합니다. 테이블의 모든 행을 검사하여 분할된 인덱스에 대한 통계를 얻으려면 `FULLSCAN` 절에서 `CREATE STATISTICS` 또는 `UPDATE STATISTICS`를 사용합니다.  
  
### <a name="Security"></a> 보안  
  
#### <a name="Permissions"></a> Permissions  
테이블이나 뷰에 대한 ALTER 권한이 필요합니다. 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 **db_ddladmin** 및 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="SSMSProcedureFrag"></a> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 인덱스 조각화 확인  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>인덱스의 조각화를 확인하려면  
  
1.  개체 탐색기에서 인덱스의 조각화를 확인할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  인덱스의 조각화를 확인할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  조각화를 확인할 인덱스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **페이지 선택**아래에서 **조각화**를 선택합니다.  
  
     **조각화** 페이지에서 다음 정보를 사용할 수 있습니다.  
  
     **페이지 사용률**  
     인덱스 페이지의 평균 사용률(%)을 나타냅니다. 즉, 인덱스 페이지가 모두 사용되고 있는 경우 100%로 표시되며, 50%인 경우 평균적으로 각 인덱스 페이지가 절반 정도 사용되고 있는 것입니다.  
  
     **총 조각화**  
     논리적 조각화 비율입니다. 이 값은 인덱스에서 순서대로 저장되어 있지 않은 페이지의 수를 나타냅니다.  
  
     **평균 행 크기**  
     리프 수준 행의 평균 크기입니다.  
  
     **깊이**  
     리프 수준을 포함한 인덱스의 수준 수입니다.  
  
     **전달된 레코드**  
     다른 데이터 위치로의 전달 포인터가 있는 힙의 레코드 수입니다. 이 상태는 업데이트하는 동안 원본 위치에 새 행을 저장할 공간이 충분하지 않은 경우에 발생합니다.  
  
     **삭제할 행**  
     삭제하도록 표시되어 있지만 아직 제거되지 않은 행의 수입니다. 이러한 행은 서버 사용량이 적을 때 정리 스레드에 의해 제거됩니다. 처리 중인 스냅숏 격리 트랜잭션으로 인해 보유된 행은 이 값에 포함되지 않습니다.  
  
     **인덱스 유형**  
     인덱스의 유형입니다. 가능한 값은 **클러스터형 인덱스**, **비클러스터형 인덱스**및 **기본 XML**입니다. 테이블을 인덱스가 없는 힙으로 저장할 수도 있지만, 그러한 경우 이 인덱스 속성 페이지를 열 수 없습니다.  
  
     **리프 수준 행**  
     리프 수준 행의 수입니다.  
  
     **최대 행 크기**  
     리프 수준 행의 최대 크기입니다.  
  
     **최소 행 크기**  
     리프 수준 행의 최소 크기입니다.  
  
     **페이지**  
     총 데이터 페이지 수입니다.  
  
     **Partition ID**  
     인덱스를 포함하는 B-트리의 파티션 ID입니다.  
  
     **버전 삭제할 행**  
     처리 중인 스냅숏 격리 트랜잭션으로 인해 보유하고 있는 삭제할 레코드 수입니다.  
  
##  <a name="TsqlProcedureFrag"></a> [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용하여 인덱스 조각화 확인  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>인덱스의 조각화를 확인하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), 
          OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b 
          ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     위의 문은 다음과 비슷한 결과 집합을 반환할 수 있습니다.  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
자세한 내용은 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 참조하세요.  
  
##  <a name="SSMSProcedureReorg"></a> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 조각화 제거  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>인덱스를 다시 구성하거나 다시 작성하려면  
  
1.  개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  인덱스를 다시 구성할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  다시 구성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 구성**을 선택합니다.  
  
6.  **인덱스 다시 구성** 대화 상자에서 **다시 구성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인**을 클릭합니다.  
  
7.  **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.  
  
8.  **확인.**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>테이블의 모든 인덱스를 다시 구성하려면  
  
1.  개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  인덱스를 다시 구성할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 마우스 오른쪽 단추로 클릭하고 **모두 다시 구성**을 선택합니다.  
  
5.  **인덱스 다시 구성** 대화 상자에서 **다시 구성할 인덱스**에 올바른 인덱스가 있는지 확인합니다. **다시 구성할 인덱스** 표에서 인덱스를 제거하려면 인덱스를 선택한 다음 Delete 키를 누릅니다.  
  
6.  **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.  
  
7.  **확인.**  
  
#### <a name="to-rebuild-an-index"></a>인덱스를 다시 작성하려면  
  
1.  개체 탐색기에서 인덱스를 다시 구성할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블** 폴더를 확장합니다.  
  
3.  인덱스를 다시 구성할 테이블을 확장합니다.  
  
4.  **인덱스** 폴더를 확장합니다.  
  
5.  다시 구성할 인덱스를 마우스 오른쪽 단추로 클릭하고 **다시 작성**을 선택합니다.  
  
6.  **인덱스 다시 작성** 대화 상자에서 **다시 작성할 인덱스** 표에 올바른 인덱스가 있는지 확인한 다음 **확인**을 클릭합니다.  
  
7.  **큰 개체 열 데이터 압축** 확인란을 선택하여 LOB(Large Object) 데이터가 포함된 모든 페이지도 압축되도록 지정합니다.  
  
8.  **확인.**  
  
## <a name="TsqlProcedureReorg"></a> [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용하여 조각화 제거 
  
#### <a name="to-reorganize-a-fragmented-index"></a>조각난 인덱스를 다시 구성하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode 
    -- index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode 
      ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>테이블의 모든 인덱스를 다시 구성하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-fragmented-index"></a>조각난 인덱스를 다시 작성하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `Employee` 테이블의 단일 인덱스를 다시 작성합니다.  
  
     [!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>테이블에서 모든 인덱스를 다시 작성하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣습니다. 이 예에서는 키워드 `ALL`을 지정합니다. 이 키워드는 테이블에 연결된 인덱스를 모두 다시 작성합니다. 3개의 옵션이 지정됩니다.  
  
     [!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]  
  
자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
 
### <a name="automatic-index-and-statistics-management"></a>자동 인덱스 및 통계 관리

[Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)와 같은 솔루션을 사용하여 하나 이상의 데이터베이스에 대한 인덱스 조각 모음 및 통계 업데이트를 자동으로 관리합니다. 이 절차는 다른 매개 변수 사이에서 조각화 수준에 따라 인덱스를 다시 작성하거나 다시 구성할지 여부를 자동으로 선택하고 통계를 선형 임계값으로 업데이트합니다.
  
## <a name="see-also"></a>참고 항목  
  [SQL Server 인덱스 디자인 가이드](../../relational-databases/sql-server-index-design-guide.md)   
  [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
  [Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)   
  [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
  [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
  
