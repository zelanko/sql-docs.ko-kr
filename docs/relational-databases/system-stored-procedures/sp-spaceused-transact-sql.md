---
title: sp_spaceused (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 61cd3c5c4ba15d42c1b1fe261703cfbb67b3e24f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538555"
---
# <a name="spspaceused-transact-sql"></a>sp_spaceused(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  행의 수, 예약된 디스크 공간 및 현재 데이터베이스의 테이블, 인덱싱된 뷰 또는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 사용하는 디스크 공간을 표시하거나, 전체 데이터베이스가 예약하여 사용하는 디스크 공간을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>인수  

에 대 한 [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] 하 고 [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)]를 `sp_spaceused` 명명 된 매개 변수를 지정 해야 합니다 (예를 들어 `sp_spaceused (@objname= N'Table1');` 매개 변수의 서 수 위치에 의존 합니다. 

`[ @objname = ] 'objname'`
   
 공간 사용 정보가 요청된 테이블, 인덱싱된 뷰 또는 큐의 정규화되거나 정규화되지 않은 이름입니다. 정규화된 개체 이름이 지정된 경우에만 따옴표가 필요합니다. 데이터베이스 이름을 포함하는 정규화된 개체 이름인 경우 데이터베이스 이름이 반드시 현재 데이터베이스의 이름이어야 합니다.  
하는 경우 *objname* 지정 하지 않으면 전체 데이터베이스에 대 한 결과 반환 합니다.  
*objname* 됩니다 **nvarchar(776)**, 기본값은 NULL입니다.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] 및 [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] 만 데이터베이스 및 테이블 개체를 지원 합니다.
  
`[ @updateusage = ] 'updateusage'` 공간 사용 정보를 업데이트 하려면 DBCC UPDATEUSAGE를 실행 해야 나타냅니다. 때 *objname* 는 지정 하지 않으면 문이 전체 데이터베이스에서 실행 될; 명령문을 실행 하는 고, 그렇지 *objname*합니다. 값은 **true** 하거나 **false**합니다. *updateusage* 됩니다 **varchar(5)**, 기본값은 **false**합니다.  
  
`[ @mode = ] 'mode'` 결과의 범위를 나타냅니다. 스트레치 된 테이블 또는 데이터베이스를 *모드* 매개 변수를 사용 하면 포함 하거나 원격 개체 부분을 제외 합니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
 합니다 *모드* 인수는 다음 값을 가질 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|ALL|개체 또는 로컬 부분과 원격 부분 모두를 포함 하 여 데이터베이스의 저장소 통계를 반환 합니다.|  
|LOCAL_ONLY|개체 또는 데이터베이스의 로컬 부분만의 저장소 통계를 반환합니다. 개체 또는 데이터베이스를 없는 경우 스트레치가 활성화 된 경우와 동일한 통계를 반환 합니다. @mode = ALL입니다.|  
|REMOTE_ONLY|개체 또는 데이터베이스의 원격 부분에 저장소 통계를 반환합니다. 이 옵션은 다음 조건 중 하나가 true 인 경우 오류를 발생 시킵니다.<br /><br /> 테이블은 스트레치에 대해 사용 되지 않습니다.<br /><br /> 테이블에는 Stretch를 활성화 하지만 하지 하도록 설정한 경우 데이터 마이그레이션. 이 경우 원격 테이블이 아직 없는 스키마.<br /><br /> 사용자가 원격 테이블을 삭제 수동으로.<br /><br /> 원격 데이터 보관의 프로 비전 성공, 상태를 반환 했지만 사실 실패 했습니다.|  
  
 *모드* 됩니다 **varchar(11)**, 기본값은 **N'ALL'** 합니다.  
  
`[ @oneresultset = ] oneresultset` 단일 결과 집합을 반환할지 여부를 나타냅니다. 합니다 *oneresultset* 인수는 다음 값을 가질 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|때 *@objname* null 이거나 지정 하지 않으면 두 개의 결과 집합이 반환 됩니다. 두 개의 결과 집합에는 기본 동작입니다.|  
|1|때 *@objname* = null 이거나 지정 되지 않은 단일 결과 집합 반환 됩니다.|  
  
 *oneresultset* 됩니다 **비트**, 기본값은 **0**합니다.  

`[ @include_total_xtp_storage] 'include_total_xtp_storage'`
**적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)]합니다.  
  
 때 @oneresultset= 1, 매개 변수 @include_total_xtp_storage 단일 결과 집합에 MEMORY_OPTIMIZED_DATA 저장소에 대 한 열이 포함 되어 있는지 여부를 결정 합니다. 기본값은 0, 즉, 기본적으로 (매개 변수를 생략) XTP 열 결과 집합에 포함 되지 않습니다.  

## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 하는 경우 *objname* 생략 된 값과 *oneresultset* 0 인 현재 데이터베이스 크기 정보를 제공 하는 다음 결과 집합 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다.|  
|**할당 되지 않은 공간**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 경우 *objname* 생략 된 값과 *oneresultset* 가 1 이면 현재 데이터베이스 크기 정보를 제공 하는 다음 단일 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다.|  
|**할당 되지 않은 공간**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 하는 경우 *objname* 지정 된 경우 지정 된 개체는 다음 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|공간 사용 정보가 필요한 개체의 이름입니다.<br /><br /> 개체의 스키마 이름은 반환되지 않습니다. 스키마 이름이 필요한 경우 사용 합니다 [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 하거나 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 해당 크기 정보를 가져오려면 동적 관리 뷰.|  
|**rows**|**char(20)**|테이블에 있는 행 수입니다. 지정된 개체가 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐일 경우 이 열은 큐에 있는 메시지 수를 나타냅니다.|  
|**reserved**|**varchar(18)**|에 대 한 예약 된 공간의 전체 양을 *objname*합니다.|  
|**data**|**varchar(18)**|데이터에 사용 되는 공간의 총량 *objname*합니다.|  
|**index_size**|**varchar(18)**|인덱스에서 사용 되는 공간의 총량 *objname*합니다.|  
|**unused**|**varchar(18)**|에 대 한 예약 된 공간의 전체 양을 *objname* 되었지만 아직 사용 합니다.|  
 
매개 변수 없이 지정 된 경우 이것이 기본 모드입니다. 다음 결과 집합에는 세부 디스크에 데이터베이스 크기 정보를 반환 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 경우 파일 그룹의 모든 검사점 파일의 총 디스크 크기 포함 됩니다.|  
|**할당 되지 않은 공간**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 경우 PRECREATED 상태의 검사점 파일의 총 디스크 크기 파일 그룹에 포함 됩니다.|  

데이터베이스의 테이블에 사용 된 공간: (이 결과 집합 반영 하지 않습니다 메모리 최적화 테이블에는 디스크 사용량의 테이블당 계정 없음) 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|

다음 결과 집합이 반환 됩니다 **경우에만** 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 하나 이상의 컨테이너를 사용 하 여: 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|PRECREATED, 기술 자료의 상태를 사용 하 여 검사점 파일의 총 크기입니다. 전체 데이터베이스에 할당 되지 않은 공간으로 개수 됩니다. [예를 들어 600, 000 KB 다시 만들어진된 검사점 파일의 경우이 열 포함 ' 600000 KB']|  
|**xtp_used**|**varchar(18)**|상태 UNDER CONSTRUCTION, ACTIVE, 및 MERGE TARGET (kb)를 사용 하 여 검사점 파일의 총 크기입니다. 메모리 최적화 테이블의 데이터에 대 한 현재 사용 중인 디스크 공간입니다.|  
|**xtp_pending_truncation**|**varchar(18)**|Kb에서 WAITING_FOR_LOG_TRUNCATION 상태를 사용 하 여 검사점 파일의 총 크기입니다. 로그 잘림이 발생 한 후 정리를 대기 중인 검사점 파일에 사용 되는 디스크 공간입니다.|

하는 경우 *objname* 는 생략 oneresultset의 값은 1 및 *include_total_xtp_storage* 이 1 이면 현재 데이터베이스 크기 정보를 제공 하는 다음 단일 결과 집합이 반환 됩니다. 경우 `include_total_xtp_storage` 은 0 (기본값), 마지막 세 열은 생략 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 경우 파일 그룹의 모든 검사점 파일의 총 디스크 크기 포함 됩니다.|
|**할당 되지 않은 공간**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 경우 PRECREATED 상태의 검사점 파일의 총 디스크 크기 파일 그룹에 포함 됩니다.|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|
|**xtp_precreated**|**varchar(18)**|PRECREATED, 기술 자료의 상태를 사용 하 여 검사점 파일의 총 크기입니다. 이 데이터베이스에 할당 되지 않은 공간으로 전체적으로 계산 됩니다. 데이터베이스에 하나 이상의 컨테이너를 사용 하 여 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. *이 열은만 포함 된 경우 @include_total_xtp_storage= 1*합니다.| 
|**xtp_used**|**varchar(18)**|상태 UNDER CONSTRUCTION, ACTIVE, 및 MERGE TARGET (kb)를 사용 하 여 검사점 파일의 총 크기입니다. 메모리 최적화 테이블의 데이터에 대 한 현재 사용 중인 디스크 공간입니다. 데이터베이스에 하나 이상의 컨테이너를 사용 하 여 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. *이 열은만 포함 된 경우 @include_total_xtp_storage= 1*합니다.| 
|**xtp_pending_truncation**|**varchar(18)**|Kb에서 WAITING_FOR_LOG_TRUNCATION 상태를 사용 하 여 검사점 파일의 총 크기입니다. 로그 잘림이 발생 한 후 정리를 대기 중인 검사점 파일에 사용 되는 디스크 공간입니다. 데이터베이스에 하나 이상의 컨테이너를 사용 하 여 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. 이 열은만 포함 된 경우 `@include_total_xtp_storage=1`합니다.|

## <a name="remarks"></a>Remarks  
 **database_size** 의 합계 보다 항상 큽니다 **예약** + **할당 되지 않은 공간이** 로그 파일의 크기를 포함 하기 때문에 있지만 **예약**하 고 **unallocated_space** 데이터 페이지만 고려 합니다.  
  
 XML 인덱스 및 전체 텍스트 인덱스에서 사용 되는 페이지에 포함 된 **index_size** 모두 결과 집합에 대 한 합니다. 때 *objname* 지정 된 경우 XML 인덱스 및 개체에 대 한 전체 텍스트 인덱스에 대 한 페이지 합계에도 계산 됩니다 **예약** 하 고 **index_size** 결과입니다.  
  
 데이터베이스 또는 같은 공간 크기 열에 공간 인덱스를 가진 개체에 대 한 공간 사용량을 계산 하는 경우 **database_size**를 **예약**, 및 **index_size**, 포함 공간 인덱스의 크기입니다.  
  
 때 *updateusage* 를 지정 합니다 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 검색 데이터를 데이터베이스에서 페이지 및 하나를 사용 하면 필요한 수정을 **sys.allocation_units** 및 **sys.partitions** 카탈로그 뷰의 각 테이블에서 사용한 저장소 공간에 대 한 합니다. 인덱스가 삭제된 후처럼 테이블에 대한 공간 정보가 최신 상태가 아닌 경우도 있습니다. *updateusage* 큰 테이블 또는 데이터베이스에서 실행 하는 데 시간이 걸릴 수 있습니다. 사용 하 여 *updateusage* 만 잘못 된 값을 반환 되는 의심 했으며 경우 프로세스는 다른 사용자 또는 프로세스에 부정적인 영향을 데이터베이스에 있습니다. 원하는 경우에는 DBCC UPDATEUSAGE를 별도로 실행할 수 있습니다.  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 반환 하는 값 **sp_spaceused** 직후 삭제 하거나 자른 큰 개체를 사용 가능한 실제 디스크 공간은 나타내지 않을 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sp_spaceused** 를 실행할 수 있는 사용 권한은 **public** 역할에 부여됩니다. **db_owner** 고정 데이터베이스 역할의 멤버만 **@updateusage** 매개 변수를 지정할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>1. 테이블에 관한 디스크 공간 정보 표시  
 다음 예에서는 `Vendor` 테이블 및 해당 인덱스의 디스크 공간 정보를 알려 줍니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>2. 데이터베이스에 관한 업데이트된 공간 정보 표시  
 다음 예에서는 현재 데이터베이스에서 사용하는 공간을 요약하고 선택적 매개 변수 `@updateusage`를 사용하여 현재 값이 반환되도록 합니다.  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>3. 스트레치 사용 테이블을 사용 하 여 연결 된 원격 테이블에 대 한 공간 사용량 정보를 표시 합니다.  
 다음 예제를 사용 하 여 스트레치 사용 테이블을 사용 하 여 연결 된 원격 테이블에서 사용 된 공간을 요약 합니다 **@mode** 원격 대상 지정 하는 인수입니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>4. 집합에서 단일 결과 데이터베이스에 대 한 공간 사용 정보를 표시  
 다음 예에서는 현재 데이터베이스를 단일 결과 집합의 공간 사용량을 요약합니다.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>5. 단일 결과 집합에서 하나 이상의 메모리 액세스에 최적화 파일 그룹을 사용 하 여 데이터베이스에 대 한 공간 사용 정보를 표시합니다. 
 다음 예제에서는 단일 결과 집합에서 하나 이상의 메모리 액세스에 최적화 파일 그룹을 사용 하 여 현재 데이터베이스에 대 한 공간 사용량을 요약합니다.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>6. 데이터베이스에 MEMORY_OPTIMIZED 테이블 개체에 대 한 공간 사용량 정보를 표시 합니다.
 다음 예제에서는 하나 이상의 메모리 액세스에 최적화 파일 그룹을 사용 하 여 현재 데이터베이스의 MEMORY_OPTIMIZED 테이블 개체에 대 한 공간 사용량을 요약합니다.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused
@objname = N'VehicleTemparatures',
@updateusage = 'FALSE',
@mode = 'ALL',
@oneresultset = '0',
@include_total_xtp_storage = '1';
GO
```  

## <a name="see-also"></a>관련 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;TRANSACT-SQL&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
