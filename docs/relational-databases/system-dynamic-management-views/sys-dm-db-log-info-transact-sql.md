---
title: sys.dm_db_log_info (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
caps.latest.revision: "4"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: b7250943f4e92d60888a75d9e577388f3cc6b1ed
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

반환 `VLF` 트랜잭션 로그 파일의 정보입니다. (모든 로그 파일 출력 테이블에에서 결합 됩니다). 출력의 각 행 나타냅니다는 `VLF` 트랜잭션 로그에 로그에 해당 VLF와 관련 된 정보를 제공 합니다.

## <a name="syntax"></a>구문  
  
```  
sys.dm_db_log_info ( database_id )  
```  
## <a name="arguments"></a>인수  
 *database_id* | NULL | 기본값  
 데이터베이스의 ID입니다. *database_id* 은 **int**합니다. 유효한 입력은 데이터베이스, NULL 또는 기본값의 ID 번호입니다. 기본값은 NULL입니다. NULL 및 DEFAULT는 현재 데이터베이스의 컨텍스트에서 해당 하는 값입니다.
 
 반환 하려면 NULL을 지정 `VLF` 현재 데이터베이스의 정보입니다.

 기본 제공 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 지정할 수 있습니다. 데이터베이스 이름을 지정하지 않고 DB_ID를 사용하는 경우 현재 데이터베이스의 호환성 수준은 90 이상이어야 합니다.  

## <a name="table-returned"></a>반환된 테이블  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스 ID입니다.|
|file_id|**smallint**|트랜잭션 로그의 파일 id입니다.|  
|vlf_begin_offset|**bigint** |오프셋의 위치는 `VLF` 트랜잭션 로그 파일의 처음부터 합니다.|
|vlf_size_mb |**float** |`VLF`크기 (MB) 2 자리로 반올림 합니다.|     
|vlf_sequence_number|**bigint** |`VLF`생성된 된 순서에서 시퀀스 번호입니다. 고유 하 게 식별 하는 데 `VLFs` 로그 파일에 있습니다.|
|vlf_active|**bit** |VLF가 사용 중인지 여부를 나타냅니다. <br />0-vlf에에서 없는 경우 사용<br />1- `VLF` 활성화 되어 있습니다.|
|vlf_status|**int** |상태는 `VLF`합니다. 가능한 값에는 <br />0- `VLF` 활성 상태가 아니거나 <br />1-vlf은 초기화 되었지만 사용 되지 않는 <br /> 2- `VLF` 활성화 되어 있습니다.|
|vlf_parity|**tinyint** |패리티 `VLF`합니다. 내 로그의 끝을 확인 하도록 내부적으로 사용 된 `VLF`합니다.|
|vlf_first_lsn|**nvarchar(48)** |첫 번째 로그 레코드의 LSN은 `VLF`합니다.|
|vlf_create_lsn|**nvarchar(48)** |로그의 LSN을 기록 만든는 `VLF`합니다.|

## <a name="remarks"></a>주의
 `sys.dm_db_log_info` 동적 관리 함수 대체는 `DBCC LOGINFO` 문. 
 
## <a name="permissions"></a>Permissions  
 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>1. 높은 수의 SQL Server 인스턴스의 데이터베이스 확인`VLFs`
다음 쿼리는 100 개 이상 포함 된 데이터베이스를 결정 `VLFs` 로그 파일에 데이터베이스 시작, 복원 및 복구 시간 달라질 수 있습니다.

```sql
SELECT name,count(l.database_id) as 'vlf_count' from sys.databases s
cross apply sys.dm_db_log_info(s.database_id) l
group by name
having count(l.database_id)> 100
```

### <a name="b-determing-the-status-of-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>2. 마지막 상태 확인 `VLF` 로그 파일을 축소 하기 전에 트랜잭션 로그에

마지막 상태를 확인 하려면 다음 쿼리를 사용할 수 `VLF` 트랜잭션 로그를 축소할 수를 확인 하려면 트랜잭션 로그에 shrinkfile을 실행 하기 전에.

```sql
USE <database name>
GO

SELECT top 1 DB_NAME(database_id) as "Database Name",file_id,vlf_size_mb,vlf_sequence_number, vlf_active, vlf_status
from sys.dm_db_log_info(DEFAULT)
order by vlf_sequence_number desc
```


## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [데이터베이스 관련된 동적 관리 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  



