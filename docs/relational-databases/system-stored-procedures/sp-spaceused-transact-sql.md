---
title: sp_spaceused (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ef8781d5c6ab68b90aefcc9c7d01e0cb9f070a02
ms.sourcegitcommit: 270de8a0260fa3c0ecc37f91eec4a5aee9b9834a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2018
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

에 대 한 [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] 및 [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)], `sp_spaceused` 명명 된 매개 변수를 지정 해야 합니다 (예를 들어 `sp_spaceused (@objname= N'Table1');` 매개 변수의 서 수 위치에 사용 하는 대신 합니다. 

 [ **@objname=**] **'***objname***'** 
   
 공간 사용 정보가 요청된 테이블, 인덱싱된 뷰 또는 큐의 정규화되거나 정규화되지 않은 이름입니다. 정규화된 개체 이름이 지정된 경우에만 따옴표가 필요합니다. 데이터베이스 이름을 포함하는 정규화된 개체 이름인 경우 데이터베이스 이름이 반드시 현재 데이터베이스의 이름이어야 합니다.  
경우 *objname* 를 지정 하지 않으면 전체 데이터베이스에 대 한 결과가 반환 됩니다.  
*objname* 은 **nvarchar(776)**, 기본값은 NULL입니다.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] 및 [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] 만 데이터베이스 및 테이블 개체를 지원 합니다.
  
 [ **@updateusage=**] **'***updateusage***'**  
 공간 사용 정보를 업데이트하려면 DBCC UPDATEUSAGE를 실행해야 함을 나타냅니다. 때 *objname* 는 명령문을 실행 하는 전체 데이터베이스에 지정 되지 않으면 명령문을 실행 하는 그렇지 않은 경우 *objname*합니다. 값은 가능 **true** 또는 **false**합니다. *updateusage* 은 **varchar(5)**, 기본값은 **false**합니다.  
  
 [ **@mode=**] **'***mode***'**  
 결과의 범위를 나타냅니다. 스트레치 사용 테이블 또는 데이터베이스에 대 한는 *모드* 매개 변수를 포함 하거나 제외 된 개체의 원격 부분 수 있습니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
 *모드* 인수는 다음 값을 가질 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|ALL|개체 또는 로컬 부분과 원격 부분이 모두 포함 하 여 데이터베이스의 저장소 통계를 반환 합니다.|  
|LOCAL_ONLY|개체 또는 데이터베이스의 로컬 부분에 저장소 통계를 반환합니다. 개체 또는 데이터베이스 스트레치 사용 데이터베이스를 없으면 때와 동일한 통계를 반환 합니다. @mode = ALL입니다.|  
|REMOTE_ONLY|개체 또는 데이터베이스의 원격 부분에 저장소 통계를 반환합니다. 이 옵션 다음 조건 중 하나에 오류가 발생 합니다.<br /><br /> 테이블을 스트레치에 사용 되지 않습니다.<br /><br /> 테이블이 stretch를 사용 하지만 데이터 마이그레이션을 사용 하도록 설정 하지 했습니다. 이 경우 원격 테이블이 아직 없는 스키마.<br /><br /> 사용자가 원격 테이블을 삭제 수동으로.<br /><br /> 성공, 상태를 반환 하는 원격 데이터 보관의 프로 비전 하지만 실제로 실패 했습니다.|  
  
 *모드* 은 **varchar(11)**, 기본값은 **N'ALL'**합니다.  
  
 [ **@oneresultset=**] *oneresultset*  
 단일 결과 집합을 반환할 것인지를 나타냅니다. *oneresultset* 인수는 다음 값을 가질 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|0|때 *@objname* null 이거나 지정 하지 않으면 두 개의 결과 집합이 반환 됩니다. 두 개의 결과 집합은 기본 동작입니다.|  
|1.|때 *@objname* 아니거나 = null을 지정 하지는 단일 결과 집합이 반환 됩니다.|  
  
 *oneresultset* 은 **비트**, 기본값은 **0**합니다.  

[ **@include_total_xtp_storage**] **'***include_total_xtp_storage***'**  
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)]합니다.  
  
 때 @oneresultset= 1, 매개 변수 @include_total_xtp_storage MEMORY_OPTIMIZED_DATA 저장소에 대 한 열이 단일 결과 집합에 포함 되어 있는지 여부를 결정 합니다. 기본값은 0, 즉, 기본적으로 (매개 변수는 생략 됨) 하는 경우 XTP 열 결과 집합에 포함 되지 않습니다.  

## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 경우 *objname* 생략 된 값과 *oneresultset* 은 0으로, 현재 데이터베이스 크기 정보를 제공 하는 다음 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다.|  
|**unallocated space**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 경우 *objname* 생략 된 값과 *oneresultset* 는 1, 현재 데이터베이스 크기 정보를 제공 하는 다음과 같은 단일 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다.|  
|**unallocated space**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 경우 *objname* 지정, 지정 된 개체는 다음 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|공간 사용 정보가 필요한 개체의 이름입니다.<br /><br /> 개체의 스키마 이름은 반환되지 않습니다. 스키마 이름이 필요한 경우 사용 하 여는 [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 또는 [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 동적 관리 뷰인 해당 크기 정보를 가져옵니다.|  
|**rows**|**char(20)**|테이블에 있는 행 수입니다. 지정된 개체가 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐일 경우 이 열은 큐에 있는 메시지 수를 나타냅니다.|  
|**reserved**|**varchar(18)**|에 대 한 예약 된 공간의 전체 크기 *objname*합니다.|  
|**data**|**varchar(18)**|데이터에 의해 사용 되는 공간의 전체 크기 *objname*합니다.|  
|**index_size**|**varchar(18)**|인덱스에 사용 된 공간의 전체 크기 *objname*합니다.|  
|**unused**|**varchar(18)**|에 대 한 예약 된 공간의 전체 크기 *objname* 되었지만 아직 사용 합니다.|  
 
지정 된 매개 변수가 없는 경우 기본 모드입니다. 다음 결과 집합에는 세부 디스크에 데이터베이스 크기 정보를 반환 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹, 경우에 파일 그룹에 모든 검사점 파일의 총 디스크 크기 포함 됩니다.|  
|**unallocated space**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹, 경우에 파일 그룹에 PRECREATED 상태와 검사점 파일의 총 디스크 크기 포함 됩니다.|  

데이터베이스의 테이블에서 사용 중인 공간: (이 결과 집합 반영 되지 않는 메모리 액세스에 최적화 된 테이블을 그대로 디스크 사용량의 테이블당 계정 없음) 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|

다음 결과 집합이 반환 됩니다 **경우에만** 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 하나 이상의 컨테이너를 사용 합니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|PRECREATED kb에서 상태와 검사점 파일의 총 크기입니다. 전체 데이터베이스에 할당 되지 않은 공간으로 계산 합니다. [예를 들어 600, 000 KB 다시 만들어진된 검사점 파일의 경우이 열 포함 ' 600000 KB']|  
|**xtp_used**|**varchar(18)**|UNDER CONSTRUCTION, 활성, 및 kb에서 MERGE TARGET 상태가 있는 검사점 파일의 총 크기입니다. 메모리 액세스에 최적화 된 테이블의 데이터에 적극적으로 사용 하는 디스크 공간입니다.|  
|**xtp_pending_truncation**|**varchar(18)**|KB 단위로 WAITING_FOR_LOG_TRUNCATION 상태와 검사점 파일의 총 크기입니다. 로그 잘림이 발생 한 후 정리를 대기 하는 검사점 파일에 사용 되는 디스크 공간입니다.|

경우 *objname* 은 생략 oneresultset의 값은 1, 및 *include_total_xtp_storage* 1 이면 현재 데이터베이스 크기 정보를 제공 하는 다음과 같은 단일 결과 집합이 반환 됩니다. 경우 `include_total_xtp_storage` 은 0 (기본값), 마지막 세 열 생략 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar(18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 데이터와 로그 파일이 포함 되어 있습니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹, 경우에 파일 그룹에 모든 검사점 파일의 총 디스크 크기 포함 됩니다.|
|**unallocated space**|**varchar(18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹, 경우에 파일 그룹에 PRECREATED 상태와 검사점 파일의 총 디스크 크기 포함 됩니다.|  
|**reserved**|**varchar(18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**data**|**varchar(18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar(18)**|인덱스가 사용하는 총 공간입니다.|  
|**unused**|**varchar(18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|
|**xtp_precreated**|**varchar(18)**|PRECREATED kb에서 상태와 검사점 파일의 총 크기입니다. 전체 데이터베이스에 할당 되지 않은 공간으로 계산합니다. 데이터베이스에 하나 이상의 컨테이너와 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. *이 열은만 포함 된 if @include_total_xtp_storage= 1*합니다.| 
|**xtp_used**|**varchar(18)**|UNDER CONSTRUCTION, 활성, 및 kb에서 MERGE TARGET 상태가 있는 검사점 파일의 총 크기입니다. 메모리 액세스에 최적화 된 테이블의 데이터에 적극적으로 사용 하는 디스크 공간입니다. 데이터베이스에 하나 이상의 컨테이너와 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. *이 열은만 포함 된 if @include_total_xtp_storage= 1*합니다.| 
|**xtp_pending_truncation**|**varchar(18)**|KB 단위로 WAITING_FOR_LOG_TRUNCATION 상태와 검사점 파일의 총 크기입니다. 로그 잘림이 발생 한 후 정리를 대기 하는 검사점 파일에 사용 되는 디스크 공간입니다. 데이터베이스에 하나 이상의 컨테이너와 memory_optimized_data 파일 그룹이 없는 경우 NULL을 반환 합니다. 이 열은만 포함 된 if `@include_total_xtp_storage=1`합니다.|

## <a name="remarks"></a>주의  
 **database_size** 의 합계 보다 항상 큽니다 **예약** + **할당 되지 않은 공간** 로그 파일의 크기를 포함 하기 때문에 있지만 **예약**및 **unallocated_space** 데이터 페이지만 고려 합니다.  
  
 XML 인덱스 및 전체 텍스트 인덱스에서 사용 되는 페이지에 포함 된 **index_size** 두 결과 집합에 대 한 합니다. 때 *objname* 지정, XML 인덱스 및 개체에 대 한 전체 텍스트 인덱스에 대 한 페이지 합계에도 계산 됩니다 **예약** 및 **index_size** 결과입니다.  
  
 데이터베이스 또는 공간 인덱스, 공간 크기 열을 포함 하는 개체에 대 한 공간 사용량 계산 됩니다 **database_size**, **예약**, 및 **index_size**, 포함 공간 인덱스의 크기입니다.  
  
 때 *updateusage* 지정는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 검사는 데이터 페이지에 데이터베이스와는 필요한 수정 하려면는 **sys.allocation_units** 및 **sys.partitions** 카탈로그 뷰를 각 테이블에서 사용 하는 저장소 공간입니다. 인덱스가 삭제된 후처럼 테이블에 대한 공간 정보가 최신 상태가 아닌 경우도 있습니다. *updateusage* 대형 테이블 또는 데이터베이스에서 실행 하는 데 약간의 시간이 걸릴 수 있습니다. 사용 하 여 *updateusage* 만 잘못 된 값을 반환 되는 의심 때 프로세스 없으며,는 다른 사용자 또는 프로세스에 좋지 않은 영향 데이터베이스에 있습니다. 원하는 경우에는 DBCC UPDATEUSAGE를 별도로 실행할 수 있습니다.  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 반환 하는 값 **sp_spaceused** 직후를 삭제 하거나 자른 큰 개체 사용 가능한 실제 디스크 공간을 반영 하지 않을 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
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
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>3. 스트레치 사용 테이블을와 연결 된 원격 테이블에 대 한 공간 사용 정보를 표시 합니다.  
 스트레치 사용 테이블을 사용 하 여 연관 된 원격 테이블에서 사용 하는 공간을 요약 하는 다음 예제는 **@mode** 원격 대상을 지정 하는 인수입니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>4. 집합에서 단일 결과 데이터베이스에 대 한 공간 사용 정보 표시  
 다음 예제에서는 단일 결과 집합의 현재 데이터베이스에 대 한 공간 사용량을 요약합니다.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>5. 단일 결과 집합에 MEMORY_OPTIMIZED 파일 그룹을 하나 이상으로 데이터베이스에 대 한 공간 사용 정보를 표시 
 다음 예제에서는 현재 데이터베이스는 단일 결과 집합에서 하나 이상의 MEMORY_OPTIMIZED 파일 그룹에 대 한 공간 사용량을 요약합니다.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>6. 데이터베이스에 MEMORY_OPTIMIZED 테이블 개체에 대 한 공간 사용 정보를 표시합니다.
 다음 예에서는 현재 데이터베이스 MEMORY_OPTIMIZED 파일 그룹을 하나 이상에 있는 MEMORY_OPTIMIZED 테이블 개체에 대 한 공간 사용량을 요약합니다.
 
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

## <a name="see-also"></a>관련 항목:  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact SQL&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
