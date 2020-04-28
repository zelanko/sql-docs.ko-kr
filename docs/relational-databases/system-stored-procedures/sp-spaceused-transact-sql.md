---
title: sp_spaceused (Transact-sql) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b0bd2f253dede1c427eda826eba0e998a144736
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72252025"
---
# <a name="sp_spaceused-transact-sql"></a>sp_spaceused(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  행의 수, 예약된 디스크 공간 및 현재 데이터베이스의 테이블, 인덱싱된 뷰 또는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 사용하는 디스크 공간을 표시하거나, 전체 데이터베이스가 예약하여 사용하는 디스크 공간을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>인수  

및 [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)]의 경우 `sp_spaceused` 은 `sp_spaceused (@objname= N'Table1');` 매개 변수의 서 수 위치에 의존 하지 않고 명명 된 매개 변수를 지정 해야 합니다. 

`[ @objname = ] 'objname'`
   
 공간 사용 정보가 요청된 테이블, 인덱싱된 뷰 또는 큐의 정규화되거나 정규화되지 않은 이름입니다. 정규화된 개체 이름이 지정된 경우에만 따옴표가 필요합니다. 데이터베이스 이름을 포함하는 정규화된 개체 이름인 경우 데이터베이스 이름이 반드시 현재 데이터베이스의 이름이어야 합니다.  
*Objname* 을 지정 하지 않으면 전체 데이터베이스에 대해 결과가 반환 됩니다.  
*objname* 은 **nvarchar (776)** 이며 기본값은 NULL입니다.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)]및 [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] 는 데이터베이스 및 테이블 개체만 지원 합니다.
  
`[ @updateusage = ] 'updateusage'`공간 사용량 정보를 업데이트 하기 위해 DBCC UPDATEUSAGE을 실행 해야 함을 나타냅니다. *Objname* 을 지정 하지 않으면 전체 데이터베이스에서 문이 실행 됩니다. 그렇지 않으면 문이 *objname*에 대해 실행 됩니다. 값은 **true** 또는 **false**일 수 있습니다. *updateusage* 은 **varchar (5)** 이며 기본값은 **false**입니다.  
  
`[ @mode = ] 'mode'`결과의 범위를 나타냅니다. 스트레치 된 테이블이 나 데이터베이스의 경우 *mode* 매개 변수를 사용 하 여 개체의 원격 부분을 포함 하거나 제외할 수 있습니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
 *Mode* 인수는 다음과 같은 값을 가질 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|ALL|로컬 부분과 원격 부분을 모두 포함 하는 개체 또는 데이터베이스의 저장소 통계를 반환 합니다.|  
|LOCAL_ONLY|개체 또는 데이터베이스의 로컬 부분에 대 한 저장소 통계만 반환 합니다. 스트레치를 사용 하지 않는 개체 또는 데이터베이스는 when @mode = ALL과 동일한 통계를 반환 합니다.|  
|REMOTE_ONLY|개체 또는 데이터베이스의 원격 부분만의 저장소 통계만 반환 합니다. 이 옵션은 다음 조건 중 하나에 해당 하는 경우 오류를 발생 시킵니다.<br /><br /> 스트레치에 대해 테이블을 사용할 수 없습니다.<br /><br /> 테이블이 스트레치에 대해 사용 하도록 설정 되어 있지만 데이터 마이그레이션을 사용 하도록 설정 하지 않았습니다. 이 경우 원격 테이블에는 아직 스키마가 없습니다.<br /><br /> 사용자가 원격 테이블을 수동으로 삭제 했습니다.<br /><br /> 원격 데이터 보관의 프로 비전이 성공 상태를 반환 했지만 실제로 실패 했습니다.|  
  
 *모드* 는 **varchar (11)** 이며 기본값은 **N'ALL '** 입니다.  
  
`[ @oneresultset = ] oneresultset`단일 결과 집합을 반환할지 여부를 나타냅니다. *Oneresultset* 인수에는 다음 값을 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|* \@Objname* 이 null 이거나 지정 되지 않은 경우 두 개의 결과 집합이 반환 됩니다. 두 개의 결과 집합이 기본 동작입니다.|  
|1|Objname = null 또는를 지정 하지 않으면 단일 결과 집합이 반환 됩니다. * \@*|  
  
 *oneresultset* 는 **bit**이며 기본값은 **0**입니다.  

`[ @include_total_xtp_storage] 'include_total_xtp_storage'`
**적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)].  
  
 = @oneresultset1 일 경우 매개 변수 @include_total_xtp_storage 는 단일 resultset에 MEMORY_OPTIMIZED_DATA 저장소에 대 한 열이 포함 되어 있는지 여부를 확인 합니다. 기본값은 0입니다. 즉, 기본적으로 매개 변수를 생략 하면 XTP 열이 resultset에 포함 되지 않습니다.  

## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 *Objname* 이 생략 되 고 *oneresultset* 값이 0 이면 현재 데이터베이스 크기 정보를 제공 하는 다음 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar (18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 에는 데이터 파일과 로그 파일이 모두 포함 됩니다.|  
|**할당 되지 않은 공간**|**varchar (18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**쓰이는**|**varchar (18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**데이터**|**varchar (18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar (18)**|인덱스가 사용하는 총 공간입니다.|  
|**사용 되지 않는**|**varchar (18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 *Objname* 을 생략 하 고 *oneresultset* 값을 1로 설정 하면 현재 데이터베이스 크기 정보를 제공 하기 위해 다음과 같은 단일 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar (18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 에는 데이터 파일과 로그 파일이 모두 포함 됩니다.|  
|**할당 되지 않은 공간**|**varchar (18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다.|  
|**쓰이는**|**varchar (18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**데이터**|**varchar (18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar (18)**|인덱스가 사용하는 총 공간입니다.|  
|**사용 되지 않는**|**varchar (18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|  
  
 *Objname* 을 지정 하면 지정 된 개체에 대해 다음 결과 집합이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|공간 사용 정보가 필요한 개체의 이름입니다.<br /><br /> 개체의 스키마 이름은 반환되지 않습니다. 스키마 이름이 필요한 경우 [dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) 또는 [dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) 동적 관리 뷰를 사용 하 여 해당 하는 크기 정보를 가져옵니다.|  
|**열**|**char (20)**|테이블에 있는 행 수입니다. 지정된 개체가 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 큐일 경우 이 열은 큐에 있는 메시지 수를 나타냅니다.|  
|**쓰이는**|**varchar (18)**|*Objname*에 대해 예약 된 공간의 전체 크기입니다.|  
|**데이터**|**varchar (18)**|*Objname*의 데이터에 사용 되는 총 공간입니다.|  
|**index_size**|**varchar (18)**|*Objname*의 인덱스에서 사용 하는 총 공간입니다.|  
|**사용 되지 않는**|**varchar (18)**|*Objname* 에 대해 예약 되었지만 아직 사용 되지 않은 총 공간입니다.|  
 
매개 변수가 지정 되지 않은 경우 기본 모드입니다. 다음 결과 집합은 디스크에 대 한 데이터베이스 크기 정보를 자세히 반환 합니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar (18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 에는 데이터 파일과 로그 파일이 모두 포함 됩니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 경우 파일 그룹에 있는 모든 검사점 파일의 전체 디스크 크기를 포함 합니다.|  
|**할당 되지 않은 공간**|**varchar (18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 경우 파일 그룹에 사전 생성 된 검사점 파일의 전체 디스크 크기를 포함 합니다.|  

데이터베이스의 테이블에 사용 되는 공간: (이 resultset은 메모리 최적화 테이블을 반영 하지 않습니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**쓰이는**|**varchar (18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**데이터**|**varchar (18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar (18)**|인덱스가 사용하는 총 공간입니다.|  
|**사용 되지 않는**|**varchar (18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|

다음 결과 집합은 데이터베이스에 하나 이상의 컨테이너가 있는 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 **경우에만** 반환 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar (18)**|상태가 사전 생성 된 검사점 파일의 총 크기 (KB)입니다. 전체적으로 데이터베이스의 할당 되지 않은 공간을 계산 합니다. 예를 들어 사전 생성 된 검사점 파일이 60만 KB 인 경우이 열에는 ' 60만 KB '가 포함 됩니다.|  
|**xtp_used**|**varchar (18)**|생성, 활성 및 병합 대상에서 상태의 검사점 파일의 총 크기 (KB)입니다. 메모리 최적화 테이블의 데이터에 적극적으로 사용 되는 디스크 공간입니다.|  
|**xtp_pending_truncation**|**varchar (18)**|상태 WAITING_FOR_LOG_TRUNCATION의 전체 검사점 파일 크기 (KB)입니다. 로그 잘림이 발생 한 후 정리를 대기 중인 검사점 파일에 사용 되는 디스크 공간입니다.|

*Objname* 이 생략 된 경우 oneresultset의 값은 1이 고 *include_total_xtp_storage* 1 이면 현재 데이터베이스 크기 정보를 제공 하기 위해 다음과 같은 단일 결과 집합이 반환 됩니다. 이 `include_total_xtp_storage` 0 (기본값) 이면 마지막 세 개의 열이 생략 됩니다. 

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|현재 데이터베이스의 이름입니다.|  
|**database_size**|**varchar (18)**|현재 데이터베이스의 크기(메가바이트)입니다. **database_size** 에는 데이터 파일과 로그 파일이 모두 포함 됩니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 경우 파일 그룹에 있는 모든 검사점 파일의 전체 디스크 크기를 포함 합니다.|
|**할당 되지 않은 공간**|**varchar (18)**|데이터베이스 개체용으로 예약되지 않은 데이터베이스 공간입니다. 데이터베이스에 MEMORY_OPTIMIZED_DATA 파일 그룹이 있는 경우 파일 그룹에 사전 생성 된 검사점 파일의 전체 디스크 크기를 포함 합니다.|  
|**쓰이는**|**varchar (18)**|데이터베이스의 개체에 의해 할당된 총 공간입니다.|  
|**데이터**|**varchar (18)**|데이터가 사용하는 총 공간입니다.|  
|**index_size**|**varchar (18)**|인덱스가 사용하는 총 공간입니다.|  
|**사용 되지 않는**|**varchar (18)**|데이터베이스의 개체에 예약되었지만 아직 사용되지 않은 총 공간입니다.|
|**xtp_precreated**|**varchar (18)**|상태가 사전 생성 된 검사점 파일의 총 크기 (KB)입니다. 이는 전체 데이터베이스의 할당 되지 않은 공간을 계산 합니다. 하나 이상의 컨테이너를 포함 하는 memory_optimized_data 파일 그룹이 데이터베이스에 없는 경우 NULL을 반환 합니다. *이 열은 = 1 인 @include_total_xtp_storage경우에만 포함 됩니다*.| 
|**xtp_used**|**varchar (18)**|생성, 활성 및 병합 대상에서 상태의 검사점 파일의 총 크기 (KB)입니다. 메모리 최적화 테이블의 데이터에 적극적으로 사용 되는 디스크 공간입니다. 하나 이상의 컨테이너를 포함 하는 memory_optimized_data 파일 그룹이 데이터베이스에 없는 경우 NULL을 반환 합니다. *이 열은 = 1 인 @include_total_xtp_storage경우에만 포함 됩니다*.| 
|**xtp_pending_truncation**|**varchar (18)**|상태 WAITING_FOR_LOG_TRUNCATION의 전체 검사점 파일 크기 (KB)입니다. 로그 잘림이 발생 한 후 정리를 대기 중인 검사점 파일에 사용 되는 디스크 공간입니다. 하나 이상의 컨테이너를 포함 하는 memory_optimized_data 파일 그룹이 데이터베이스에 없는 경우 NULL을 반환 합니다. 이 열은 인 경우 `@include_total_xtp_storage=1`에만 포함 됩니다.|

## <a name="remarks"></a>설명  
 **database_size** 은 로그 파일의 크기를 포함 하기 때문에 **예약** + **된 할당 되지 않은 공간의** 합계 보다 항상 큽니다. **예약** 된 공간 및 **unallocated_space** 데이터 페이지만 고려 합니다.  
  
 XML 인덱스 및 전체 텍스트 인덱스에 사용 되는 페이지는 두 결과 집합의 **index_size** 에 포함 됩니다. *Objname* 을 지정 하면 개체의 XML 인덱스 및 전체 텍스트 인덱스에 대 한 페이지도 총 **예약** 된 결과와 **index_size** 결과에 계산 됩니다.  
  
 데이터베이스 또는 공간 인덱스를 포함 하는 개체에 대해 공간 사용량이 계산 된 경우 **database_size**, **예약 됨**, **index_size**등의 공간 크기 열에는 공간 인덱스의 크기가 포함 됩니다.  
  
 *Updateusage* 를 지정 하면는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스의 데이터 페이지를 검색 하 고, 각 테이블에서 사용 하는 저장소 공간에 대 한 및 **sys. 파티션** 카탈로그 뷰에 필요한 **allocation_units** 수정 사항을 만듭니다. 인덱스가 삭제된 후처럼 테이블에 대한 공간 정보가 최신 상태가 아닌 경우도 있습니다. *updateusage* 는 많은 테이블이 나 데이터베이스에서 실행 하는 데 다소 시간이 걸릴 수 있습니다. 잘못 된 값이 반환 되 고 의심 되는 경우와 데이터베이스의 다른 사용자 또는 프로세스에 부정적인 영향을 주지 않는 경우에만 *updateusage* 를 사용 합니다. 원하는 경우에는 DBCC UPDATEUSAGE를 별도로 실행할 수 있습니다.  
  
> [!NOTE]  
>  대형 인덱스를 삭제하거나 다시 작성할 때 또는 대형 테이블을 삭제하거나 자를 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 트랜잭션이 커밋될 때까지 실제 페이지 할당 해제 및 관련 잠금을 연기합니다. 삭제 작업이 지연되어도 할당된 공간이 즉시 해제되지는 않습니다. 따라서 대량 개체를 삭제 하거나 자른 직후 **sp_spaceused** 에서 반환 하는 값에는 사용 가능한 실제 디스크 공간이 반영 되지 않을 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **sp_spaceused** 를 실행할 수 있는 사용 권한은 **public** 역할에 부여됩니다. **db_owner** 고정 데이터베이스 역할의 멤버만 **\@updateusage** 매개 변수를 지정할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>A. 테이블에 관한 디스크 공간 정보 표시  
 다음 예에서는 `Vendor` 테이블 및 해당 인덱스의 디스크 공간 정보를 알려 줍니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>B. 데이터베이스에 관한 업데이트된 공간 정보 표시  
 다음 예에서는 현재 데이터베이스에서 사용하는 공간을 요약하고 선택적 매개 변수 `@updateusage`를 사용하여 현재 값이 반환되도록 합니다.  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. 스트레치 사용 테이블에 연결 된 원격 테이블에 대 한 공간 사용량 정보 표시  
 다음 예에서는 ** \@mode** 인수를 사용 하 여 원격 대상을 지정 하 여 스트레치 사용 테이블에 연결 된 원격 테이블에 사용 되는 공간을 요약 합니다. 자세한 내용은 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)를 참조하십시오.  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. 단일 결과 집합에서 데이터베이스에 대 한 공간 사용량 정보 표시  
 다음 예에서는 단일 결과 집합에서 현재 데이터베이스의 공간 사용량을 요약 합니다.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memory_optimized-file-group-in-a-single-result-set"></a>E. 단일 결과 집합에 하나 이상의 MEMORY_OPTIMIZED 파일 그룹이 있는 데이터베이스에 대 한 공간 사용량 정보 표시 
 다음 예에서는 단일 결과 집합에 하나 이상의 MEMORY_OPTIMIZED 파일 그룹이 있는 현재 데이터베이스에 대 한 공간 사용량을 요약 합니다.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memory_optimized-table-object-in-a-database"></a>F. 데이터베이스의 MEMORY_OPTIMIZED table 개체에 대 한 공간 사용량 정보를 표시 합니다.
 다음 예에서는 현재 데이터베이스에서 하나 이상의 MEMORY_OPTIMIZED 파일 그룹이 있는 MEMORY_OPTIMIZED table 개체에 대 한 공간 사용량을 요약 합니다.
 
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

## <a name="see-also"></a>참고 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [allocation_units &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [index_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys. 개체 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [&#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
