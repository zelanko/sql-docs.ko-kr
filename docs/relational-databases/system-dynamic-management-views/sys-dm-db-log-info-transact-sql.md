---
title: sys.dm_db_log_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_log_info
- sys.dm_db_log_info_TSQL
- dm_db_log_info
- dm_db_log_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_info dynamic management view
ms.assetid: f6b40060-c17d-472f-b0a3-3b350275d487
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50549b10793346331d2e5cb8668243db615a443b
ms.sourcegitcommit: ef115025e57ec342c14ed3151ce006f484d1fadc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411150"
---
# <a name="sysdmdbloginfo-transact-sql"></a>sys.dm_db_log_info (Transact SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

반환 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 트랜잭션 로그의 정보입니다. 참고 모든 트랜잭션 로그 파일은 테이블 출력에 결합 됩니다. 출력의 각 행의 트랜잭션 로그에 VLF를 나타내며 해당 VLF 로그에서 관련 된 정보를 제공 합니다.

## <a name="syntax"></a>구문  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>인수  
 *database_id* | NULL | DEFAULT  
 데이터베이스의 ID입니다. *database_id*는 **int**입니다. 유효한 입력은 database, NULL 또는 기본값의 ID 번호입니다. 기본값은 NULL입니다. NULL 및 DEFAULT는 현재 데이터베이스의 컨텍스트에서 해당 하는 값입니다.
 
 현재 데이터베이스의 VLF 정보를 반환 하려면 NULL을 지정 합니다.

 기본 제공 함수 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 지정할 수 있습니다. 사용 하는 경우 `DB_ID` 데이터베이스 이름을 지정 하지 않고 현재 데이터베이스의 호환성 수준을 90 이상 이어야 합니다.  

## <a name="table-returned"></a>반환된 테이블  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스 ID입니다.|
|file_id|**smallint**|트랜잭션 로그의 파일 id입니다.|  
|vlf_begin_offset|**bigint** |위치 오프셋 합니다 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 트랜잭션 로그 파일의 시작 부분에서.|
|vlf_size_mb |**float** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 크기 (mb)을 2 자리로 반올림 합니다.|     
|vlf_sequence_number|**bigint** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 시퀀스 번호 생성 순서에서입니다. 로그 파일에는 Vlf를 고유 하 게 식별 하는 데 사용 합니다.|
|vlf_active|**bit** |나타냅니다 여부 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 되었거나 사용에서 되지 않습니다. <br />0-VLF에에서 없는 사용 합니다.<br />1-VLF 활성 상태입니다.|
|vlf_status|**int** |상태를 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)합니다. 가능한 값은 <br />0-VLF active입니다. <br />1-VLF는 초기화 되었지만 사용 되지 않는 <br /> 2-VLF 활성 상태입니다.|
|vlf_parity|**tinyint** |패리티 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)합니다. 데 내부적으로 VLF 내에서 로그의 끝을 확인 합니다.|
|vlf_first_lsn|**nvarchar(48)** |[LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 에서 첫 번째 로그 레코드는 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)합니다.|
|vlf_create_lsn|**nvarchar(48)** |[LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 로그의 만든를 기록 합니다 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)합니다.|
|vlf_encryptor_thumbprint|**varbinary(20)**| **적용 대상:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> VLF를 사용 하 여 암호화 됩니다 VLF의 암호기의 손도장을 표시 [투명 한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md)이 고, 그렇지 않으면 NULL입니다. |

## <a name="remarks"></a>Remarks
합니다 `sys.dm_db_log_info` 동적 관리 함수를 대체 합니다 `DBCC LOGINFO` 문입니다.    
 
## <a name="permissions"></a>사용 권한  
필요는 `VIEW DATABASE STATE` 데이터베이스의 권한입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>1. 많은 Vlf 사용 하 여 SQL Server 인스턴스에서 데이터베이스 확인
다음 쿼리는 데이터베이스 시작, 복원 및 복구 시간에 영향을 줄 수 있는 로그 파일에 100 개가 넘는 Vlf 사용 하 여 데이터베이스를 결정 합니다.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>2. 마지막 위치 확인 `VLF` 로그 파일을 축소 하기 전에 트랜잭션 로그

트랜잭션 로그를 축소할 수 있는지 확인 하려면 트랜잭션 로그에 shrinkfile을 실행 하기 전에 마지막 활성 VLF의 위치를 확인 하려면 다음 쿼리를 사용할 수 있습니다.

```sql
USE AdventureWorks2016
GO

;WITH cte_vlf AS (
SELECT ROW_NUMBER() OVER(ORDER BY vlf_begin_offset) AS vlfid, DB_NAME(database_id) AS [Database Name], vlf_sequence_number, vlf_active, vlf_begin_offset, vlf_size_mb
    FROM sys.dm_db_log_info(DEFAULT)),
cte_vlf_cnt AS (SELECT [Database Name], COUNT(vlf_sequence_number) AS vlf_count,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 0) AS vlf_count_inactive,
    (SELECT COUNT(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS vlf_count_active,
    (SELECT MIN(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_min_vlf_active,
    (SELECT MIN(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS min_vlf_active,
    (SELECT MAX(vlfid) FROM cte_vlf WHERE vlf_active = 1) AS ordinal_max_vlf_active,
    (SELECT MAX(vlf_sequence_number) FROM cte_vlf WHERE vlf_active = 1) AS max_vlf_active
    FROM cte_vlf
    GROUP BY [Database Name])
SELECT [Database Name], vlf_count, min_vlf_active, ordinal_min_vlf_active, max_vlf_active, ordinal_max_vlf_active,
((ordinal_min_vlf_active-1)*100.00/vlf_count) AS free_log_pct_before_active_log,
((ordinal_max_vlf_active-(ordinal_min_vlf_active-1))*100.00/vlf_count) AS active_log_pct,
((vlf_count-ordinal_max_vlf_active)*100.00/vlf_count) AS free_log_pct_after_active_log
FROM cte_vlf_cnt
GO
```

## <a name="see-also"></a>관련 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

