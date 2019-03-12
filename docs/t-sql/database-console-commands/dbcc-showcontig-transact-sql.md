---
title: DBCC SHOWCONTIG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_SHOWCONTIG_TSQL
- DBCC SHOWCONTIG
- SHOWCONTIG
- SHOWCONTIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying defragmentation information
- DBCC SHOWCONTIG statement
- defragmenting indexes
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 1df2123a-1197-4fff-91a3-25e3d8848aaa
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 0cc3055f6d6d6f293500cdd6aabca5c0e51df11a
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685790"
---
# <a name="dbcc-showcontig-transact-sql"></a>DBCC SHOWCONTIG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

지정한 테이블이나 뷰의 데이터와 인덱스에 대한 조각화 정보를 표시합니다.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)를 대신 사용합니다.  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC SHOWCONTIG   
[ (   
    { table_name | table_id | view_name | view_id }   
    [ , index_name | index_id ]   
) ]   
    [ WITH   
        {   
         [ , [ ALL_INDEXES ] ]   
         [ , [ TABLERESULTS ] ]   
         [ , [ FAST ] ]  
         [ , [ ALL_LEVELS ] ]   
         [ NO_INFOMSGS ]  
         }  
    ]  
```  
  
## <a name="arguments"></a>인수  
 *table_name* | *table_id* | *view_name* | *view_id*  
 조각화 정보를 검사할 테이블이나 뷰입니다. 이 인수를 지정하지 않으면 현재 데이터베이스의 모든 테이블과 인덱싱된 뷰를 검사합니다. 테이블이나 뷰 ID를 구하려면 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 함수를 사용합니다.  
  
 *index_name* | *index_id*  
 조각화 정보를 검사할 인덱스입니다. 이 인수를 지정하지 않으면 지정한 테이블이나 뷰의 기본 인덱스를 처리합니다. 인덱스 ID를 가져오려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
 의 모든 멘션을  
 DBCC 문에서 반환되는 정보 유형에 대한 옵션을 지정합니다.  
  
 FAST  
 인덱스의 고속 검색과 최소 정보 출력 수행 여부를 지정합니다. 고속 검색은 인덱스의 리프 또는 데이터 수준 페이지를 읽지 않습니다.  
  
 ALL_INDEXES  
 특정 인덱스가 지정된 경우라도 지정한 테이블과 뷰의 모든 인덱스에 대한 결과를 표시합니다.  
  
 TABLERESULTS  
 결과를 추가 정보와 함께 행 집합으로 표시합니다.  
  
 ALL_LEVELS  
 이전 버전과의 호환성을 위해서만 유지됩니다. ALL_LEVELS가 지정되더라도 인덱스 리프 수준 또는 테이블 데이터 수준만 처리됩니다.  
  
 NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
다음 표에서는 결과 집합에 표시되는 정보를 설명합니다.
  
|통계|설명|  
|---|---|
|**검색한 페이지**|테이블이나 인덱스의 페이지 수입니다.|  
|**검색한 익스텐트**|테이블이나 인덱스의 익스텐트 수입니다.|  
|**익스텐트 스위치**|DBCC 문이 테이블이나 인덱스의 페이지를 이동한 동안 익스텐트 간에 이동한 횟수입니다.|  
|**Avg. Pages per Extent**|페이지 체인에서 익스텐트당 페이지 수입니다.|  
|**검색 밀도[최적: 실제]**|백분율입니다. **Best Count** 대 **Actual Count**의 비율입니다. 모든 데이터가 인접한 경우 이 값은 100이고 이 값이 100보다 작으면 일부 데이터가 조각화된 것입니다.<br /><br /> **최적**은 모든 데이터가 인접해서 연결되어 있는 경우 이상적인 익스텐트 변경 횟수이고 **실제**는 실제 익스텐트 변경 횟수입니다.|  
|**논리 검색 조각화 상태**|인덱스의 리프 페이지 검색에서 반환된 순서가 잘못된 페이지의 비율입니다. 이 값은 힙과는 관계가 없습니다. 순서가 잘못된 페이지란 인덱스에 할당된 다음 물리적 페이지가 현재 리프 페이지의 다음 페이지 포인터가 가리키는 페이지와 다른 경우를 나타냅니다.|  
|**익스텐트 검색 조각화 상태**|인덱스의 리프 페이지 검색에서 순서가 잘못된 익스텐트의 비율입니다. 이 값은 힙과는 관계가 없습니다. 순서가 잘못된 익스텐트란 인덱스의 현재 페이지가 들어 있는 익스텐트가 실제로 인덱스의 이전 페이지가 들어 있는 익스텐트의 다음 익스텐트가 아닌 경우입니다.<br /><br /> 참고: 인덱스가 여러 파일에 걸쳐 있을 경우 이 값은 의미가 없습니다.|  
|**Avg. Bytes Free per Page**|검색된 페이지에서 사용 가능한 평균 바이트 수입니다. 이 값이 클수록 페이지의 사용률이 낮습니다. 인덱스의 임의 삽입 횟수가 적은 경우 이 값이 작은 것이 좋습니다. 이 값은 행 크기에 따라 달라지며 행 크기가 크면 값이 커집니다.|  
|**Avg. Page density (full)**|평균 페이지 밀도입니다(백분율). 이 값은 행 크기의 영향을 받습니다. 따라서 이 값은 페이지의 꽉 찬 정도를 보다 정확하게 반영합니다. 이 백분율 값이 클수록 좋습니다.|  
  
*table_id*와 FAST를 지정하면 DBCC SHOWCONTIG가 다음 열만 가진 결과 집합을 반환합니다.
-   **검색한 페이지**  
-   **익스텐트 스위치**  
-   **검색 밀도[최적:실제]**  
-   **익스텐트 검색 조각화 상태**  
-   **논리 검색 조각화 상태**  
  
TABLERESULTS를 지정하면 DBCC SHOWCONTIG가 다음 열을 반환하고 이전 테이블에 설명된 9개의 열도 반환합니다.
  
|통계|설명|  
|---|---|
|**개체 이름**|처리되는 테이블 또는 뷰의 이름입니다.|  
|**ObjectId**|개체 이름의 ID입니다.|  
|**IndexName**|처리되는 인덱스 이름입니다. 힙의 경우 NULL입니다.|  
|**IndexId**|인덱스의 ID입니다. 힙의 경우 0입니다.|  
|**Level**|인덱스 수준입니다. 수준 0은 인덱스의 리프 또는 데이터 수준입니다.<br /><br /> 힙의 경우 수준은 0입니다.|  
|**페이지**|인덱스 또는 전체 힙의 해당 수준을 구성하는 페이지의 수입니다.|  
|**행**|인덱스의 해당 수준에 있는 데이터 또는 인덱스 레코드의 수입니다. 힙의 경우 이 값은 전체 힙에 있는 데이터 레코드 수입니다.<br /><br /> 힙의 경우 이 함수에서 반환된 레코드 수는 힙에 대해 SELECT COUNT(*)를 실행하여 반환된 행 수와 다릅니다. 이것은 한 행에 여러 레코드가 있기 때문입니다. 예를 들어 특정 업데이트 상황에서 업데이트 작업으로 인해 단일 힙 행에 한 개의 전달되고 있는 레코드와 한 개의 전달된 레코드가 있을 수 있습니다. 또한 가장 큰 LOB 행이 LOB_DATA 저장소에서 여러 레코드로 분할됩니다.|  
|**MinimumRecordSize**|인덱스 또는 전체 힙의 해당 수준에 있는 최소 레코드 크기입니다.|  
|**MaximumRecordSize**|인덱스 또는 전체 힙의 해당 수준에 있는 최대 레코드 크기입니다.|  
|**AverageRecordSize**|인덱스 또는 전체 힙의 해당 수준에 있는 평균 레코드 크기입니다.|  
|**ForwardedRecords**|인덱스 또는 전체 힙의 해당 수준에 있는 전달된 레코드 수입니다.|  
|**Extents**|인덱스 또는 전체 힙의 해당 수준에 있는 익스텐트 수입니다.|  
|**ExtentSwitches**|DBCC 문이 테이블이나 인덱스의 페이지를 이동한 동안 익스텐트 간에 이동한 횟수입니다.|  
|**AverageFreeBytes**|검색된 페이지에서 사용 가능한 평균 바이트 수입니다. 이 값이 클수록 페이지의 사용률이 낮습니다. 인덱스의 임의 삽입 횟수가 적은 경우 이 값이 작은 것이 좋습니다. 이 값은 행 크기에 따라 달라지며 행 크기가 크면 값이 커집니다.|  
|**AveragePageDensity**|평균 페이지 밀도입니다(백분율). 이 값은 행 크기의 영향을 받습니다. 따라서 이 값은 페이지의 꽉 찬 정도를 보다 정확하게 반영합니다. 이 백분율 값이 클수록 좋습니다.|  
|**ScanDensity**|백분율입니다. **BestCount** 대 **ActualCount** 비율입니다. 모든 데이터가 인접한 경우 이 값은 100이고 이 값이 100보다 작으면 일부 데이터가 조각화된 것입니다.|  
|**BestCount**|모든 데이터가 인접해서 연결되어 있는 경우 이상적인 익스텐트 변경 횟수가 됩니다.|  
|**ActualCount**|실제 익스텐트 변경 횟수입니다.|  
|**LogicalFragmentation**|인덱스의 리프 페이지 검색에서 반환된 순서가 잘못된 페이지의 비율입니다. 이 값은 힙과는 관계가 없습니다. 순서가 잘못된 페이지란 인덱스에 할당된 다음 물리적 페이지가 현재 리프 페이지의 다음 페이지 포인터가 가리키는 페이지와 다른 경우를 나타냅니다.|  
|**ExtentFragmentation**|인덱스의 리프 페이지 검색에서 순서가 잘못된 익스텐트의 비율입니다. 이 값은 힙과는 관계가 없습니다. 순서가 잘못된 익스텐트란 인덱스의 현재 페이지가 들어 있는 익스텐트가 실제로 인덱스의 이전 페이지가 들어 있는 익스텐트의 다음 익스텐트가 아닌 경우입니다.<br /><br /> 참고: 인덱스가 여러 파일에 걸쳐 있을 경우 이 값은 의미가 없습니다.|  
  
WITH TABLERESULTS와 FAST를 지정할 때의 결과 집합은 다음 열이 Null 값을 가진다는 점을 제외하면 WITH TABLERESULTS를 지정할 때와 동일합니다.

| 행| Extents |
|---|---|
|**MinimumRecordSize**|**AverageFreeBytes**|  
|**MaximumRecordSize**|**AveragePageDensity**|  
|**AverageRecordSize**|**ExtentFragmentation**|  
|**ForwardedRecords**||  
  
## <a name="remarks"></a>Remarks  
DBCC SHOWCONTIG 문은 *index_id*를 지정했을 때 지정된 인덱스의 리프 수준에서 페이지 체인을 검색하고, *table_id*만 지정하거나 *index_id*가 0인 경우에는 지정한 테이블의 데이터 페이지를 검색합니다. 이 작업에는 내재된 공유(IS) 테이블 잠금만 필요합니다. 이런 방법으로 배타적(X) 테이블 잠금이 필요한 경우를 제외하고 모든 업데이트와 삽입을 수행할 수 있으므로 실행 속도 및 동시성의 유지 그리고 반환되는 통계 데이터 수 사이에서 절충점을 찾을 수 있습니다. 그러나 조각화를 평가하는 데만 이 명령을 사용하는 경우에는 최상의 성능을 얻으려면 WITH FAST 옵션을 사용하는 것이 좋습니다. 고속 검색은 인덱스의 리프 또는 데이터 수준 페이지를 읽지 않습니다. WITH FAST 옵션은 힙에 적용되지 않습니다.
  
## <a name="restrictions"></a>Restrictions  
DBCC SHOWCONTIG는 **ntext**, **text** 및 **image** 데이터 형식에 데이터를 표시하지 않습니다. 이것은 텍스트와 이미지 데이터를 저장하는 텍스트 인덱스가 더 이상 존재하지 않기 때문입니다.
  
또한 DBCC SHOWCONTIG는 일부 새로운 기능을 지원하지 않습니다. 예를 들어 다음과 같이 사용할 수 있습니다.
-   지정된 테이블이나 인덱스가 분할되는 경우 DBCC SHOWCONTIG는 지정된 테이블이나 인덱스의 첫 번째 파티션만 표시합니다.  
-   DBCC SHOWCONTIG는 행 오버플로 스토리지 정보와 **nvarchar(max)**, **varchar(max)**, **varbinary(max)** 및 **xml**과 같은 새로운 행 외부 데이터 형식을 표시하지 않습니다.  
-   공간 인덱스는 DBCC SHOWCONTIG에서 지원되지 않습니다.  
  
모든 새로운 기능은 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 동적 관리 뷰에서 완전히 지원됩니다.
  
## <a name="table-fragmentation"></a>테이블 조각화  
DBCC SHOWCONTIG는 테이블의 조각화 여부를 확인합니다. 테이블 조각화는 테이블에서 INSERT, UPDATE, DELETE 문 등의 데이터 수정 문을 처리할 때 발생합니다. 이러한 수정 사항은 테이블의 행에서 균등하게 분산되지 않으므로 각 페이지의 사용률 수준이 시간에 따라 달라지게 됩니다. 테이블의 일부 또는 전부를 검색하는 쿼리의 경우 이런 테이블 조각화로 인해 읽어야 하는 페이지의 수가 늘어날 수 있으며 이는 데이터의 병렬 검색에 방해가 됩니다.
  
인덱스가 심하게 조각화된 경우에는 다음의 방법으로 조각화를 줄일 수 있습니다.
-   클러스터형 인덱스를 삭제한 다음 다시 만듭니다.  
     클러스터형 인덱스를 다시 만들면 데이터가 재구성되어 완전한 데이터 페이지가 만들어집니다. 사용률 수준은 CREATE INDEX의 FILLFACTOR 옵션으로 구성할 수 있습니다. 이 방법의 단점은 삭제하거나 다시 만드는 동안 인덱스가 오프라인 상태라는 것과 작업의 원자성에 있습니다. 인덱스 생성이 중단되면 그 인덱스는 다시 생성되지 않습니다.  
-   인덱스의 리프 수준 페이지를 논리적인 순서로 다시 정렬합니다.  
     ALTER INDEX...REORGANIZE를 사용하여 인덱스의 리프 수준 페이지를 논리적 순서로 다시 정렬합니다. 이 작업은 온라인 작업이므로 문이 실행 중일 때 인덱스를 사용할 수 있습니다. 또한 이 작업은 완료된 작업의 손실 없이 중단할 수 있습니다. 이 방법의 단점은 클러스터형 인덱스를 삭제하거나 다시 만드는 방법만큼은 데이터를 잘 구성하지 못한다는 점입니다.  
-   인덱스를 다시 작성합니다.  
     ALTER INDEX에 REBUILD를 사용하여 인덱스를 다시 작성합니다. 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
임의 삽입이 많지 않은 인덱스의 경우 **Avg. Bytes free per page** 및 **Avg. Page density (full)** 통계는 인덱스 페이지의 사용률을 나타냅니다. 임의 삽입이 많지 않은 인덱스의 경우 **Avg. Bytes free per page** 수는 낮고 **Avg. Page density (full)** 수는 임의 삽입이 많지 않은 인덱스에 대해 높아야 합니다. 인덱스를 삭제하고 FILLFACTOR 옵션을 지정하여 다시 만들면 통계 결과를 개선할 수 있습니다. 또한 FILLFACTOR를 고려하여 ALTER INDEX에 REORGANIZE를 사용하면 인덱스가 압축되어 통계 결과가 개선됩니다.
  
> [!NOTE]  
>  임의 삽입이 많고 페이지 사용률이 매우 높은 인덱스에서는 페이지 분할의 횟수가 증가하므로 더 많은 조각이 생깁니다.  
  
인덱스의 조각화 수준은 다음 방법으로 확인할 수 있습니다.
-   **익스텐트 스위치**와 **검색한 익스텐트**의 값을 비교합니다.  
     **익스텐트 스위치**의 값은 **검색한 익스텐트**의 값에 가능한 근접해야 합니다. 이 비율은 **검색 밀도** 값으로 계산됩니다. 이 값은 높을수록 좋으며 인덱스 조각화를 줄여 개선할 수 있습니다.  
  
    > [!NOTE]  
    >  인덱스가 여러 파일에 걸쳐 있으면 이 방법을 사용할 수 없습니다.  
  
-   **논리 검색 조각화 상태**와 **익스텐트 검색 조각화 상태** 값을 파악하는 방법입니다.  
     **논리 검색 조각화 상태**와 그 정도는 덜하지만 **익스텐트 검색 조각화 상태** 값은 테이블의 조각화를 가장 잘 나타내는 지표입니다. 이 두 값은 모두 0%부터 10%까지의 값이 될 수 있지만 가능한 0에 가까워야 합니다.  
  
    > [!NOTE]  
    >  인덱스가 여러 파일에 걸쳐 있으면 **익스텐트 검색 조각화 상태** 값이 높아집니다. 이 값을 줄이려면 인덱스 조각화를 줄여야 합니다.  
  
## <a name="permissions"></a>Permissions  
사용자는 테이블을 소유하거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
### <a name="a-displaying-fragmentation-information-for-a-table"></a>1. 테이블의 조각화 정보 표시  
다음 예에서는 `Employee` 테이블의 조각화 정보를 표시합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('HumanResources.Employee');  
GO  
```  
  
### <a name="b-using-objectid-to-obtain-the-table-id-and-sysindexes-to-obtain-the-index-id"></a>2. OBJECT_ID를 사용한 테이블 ID 가져오기 및 sys.indexes를 사용한 인덱스 ID 가져오기  
다음 예에서는 `OBJECT_ID` 및 `sys.indexes` 카탈로그 뷰를 사용하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스의 `Production.Product`테이블에서 `AK_Product_Name` 인덱스의 테이블 ID 및 인덱스 ID를 가져옵니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @id int, @indid int  
SET @id = OBJECT_ID('Production.Product')  
SELECT @indid = index_id   
FROM sys.indexes  
WHERE object_id = @id   
   AND name = 'AK_Product_Name'  
DBCC SHOWCONTIG (@id, @indid);  
GO  
```  
  
### <a name="c-displaying-an-abbreviated-result-set-for-a-table"></a>C. 테이블에 대한 생략된 결과 집합 표시  
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]데이터베이스의 `Product`테이블에 대해 생략된 결과 집합을 반환합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('Production.Product', 1) WITH FAST;  
GO  
```  
  
### <a name="d-displaying-the-full-result-set-for-every-index-on-every-table-in-a-database"></a>D. 데이터베이스의 모든 테이블의 모든 인덱스에 대한 전체 결과 집합 표시  
다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에 있는 모든 테이블의 모든 인덱스에 대한 전체 테이블 결과 집합을 반환합니다.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG WITH TABLERESULTS, ALL_INDEXES;  
GO  
```  
  
### <a name="e-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>E. DBCC SHOWCONTIG 및 DBCC INDEXDEFRAG를 사용하여 데이터베이스에서 인덱스 조각 모음 수행  
다음 예에서는 데이터베이스에서 선언된 임계값 이상으로 조각화된 모든 인덱스에 조각 모음을 수행하는 간단한 방법을 보여 줍니다.
  
```sql
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DROP INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
[sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)
  
  

