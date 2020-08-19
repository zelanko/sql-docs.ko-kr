---
description: sys. dm_db_log_info (Transact-sql)
title: sys. dm_db_log_info (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: aba965d4a0289db9ef7def58b90f15a1479cb485
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447665"
---
# <a name="sysdm_db_log_info-transact-sql"></a>sys. dm_db_log_info (Transact-sql)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

트랜잭션 로그의 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 정보를 반환 합니다. 모든 트랜잭션 로그 파일은 테이블 출력에 결합 됩니다. 출력의 각 행은 트랜잭션 로그의 VLF를 나타내며 로그에서 해당 VLF와 관련 된 정보를 제공 합니다.

## <a name="syntax"></a>구문  
  
```  
sys.dm_db_log_info ( database_id )  
``` 

## <a name="arguments"></a>인수  
 *database_id* | NULL | 기본  
 데이터베이스의 ID입니다. *database_id* 은 **int**입니다. 올바른 입력은 데이터베이스의 ID 번호, NULL 또는 DEFAULT입니다. 기본값은 NULL입니다. NULL 및 기본값은 현재 데이터베이스의 컨텍스트에서 동일한 값입니다.
 
 현재 데이터베이스의 VLF 정보를 반환 하려면 NULL을 지정 합니다.

 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) 기본 제공 함수를 지정할 수 있습니다. `DB_ID`데이터베이스 이름을 지정 하지 않고를 사용 하는 경우 현재 데이터베이스의 호환성 수준은 90 이상 이어야 합니다.  

## <a name="table-returned"></a>반환된 테이블  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스 ID입니다.|
|file_id|**smallint**|트랜잭션 로그의 파일 id입니다.|  
|vlf_begin_offset|**bigint** |트랜잭션 로그 파일의 시작 부분에서 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 의 오프셋 위치입니다.|
|vlf_size_mb |**float** |[가상 로그 파일 (VLF) 크기 (MB)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 로, 소수 자릿수 2 자리로 반올림 됩니다.|     
|vlf_sequence_number|**bigint** |만든 주문의 [가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 시퀀스 번호입니다. 로그 파일에서 Vlf를 고유 하 게 식별 하는 데 사용 됩니다.|
|vlf_active|**bit** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) 이 사용 중인지 여부를 나타냅니다. <br />0-VLF를 사용 하 고 있지 않습니다.<br />1-VLF가 활성 상태입니다.|
|vlf_status|**int** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)의 상태입니다. 가능한 값은 다음과 같습니다. <br />0-VLF가 비활성 상태임 <br />1-VLF가 초기화 되었지만 사용 되지 않음 <br /> 2-VLF가 활성 상태입니다.|
|vlf_parity|**tinyint** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)의 패리티입니다. VLF 내에서 로그의 끝을 확인 하기 위해 내부적으로 사용 됩니다.|
|vlf_first_lsn|**nvarchar (48)** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)에 있는 첫 번째 로그 레코드의 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 입니다.|
|vlf_create_lsn|**nvarchar (48)** |[가상 로그 파일 (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)을 만든 로그 레코드의 [LSN (로그 시퀀스 번호)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 입니다.|
|vlf_encryptor_thumbprint|**varbinary(20)**| **적용 대상:** [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br><br> [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md)를 사용 하 여 vlf가 암호화 된 경우 vlf의 암호기 지문을 표시 합니다. 그렇지 않으면 NULL입니다. |

## <a name="remarks"></a>설명
`sys.dm_db_log_info`동적 관리 함수는 문을 대체 합니다 `DBCC LOGINFO` .    
 
## <a name="permissions"></a>사용 권한  
데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` .  
  
## <a name="examples"></a>예제  
  
### <a name="a-determing-databases-in-a-sql-server-instance-with-high-number-of-vlfs"></a>A. Vlf 수가 많은 SQL Server 인스턴스의 데이터베이스 판단
다음 쿼리는 데이터베이스 시작, 복원 및 복구 시간에 영향을 줄 수 있는 로그 파일의 Vlf가 100 이상인 데이터베이스를 결정 합니다.

```sql
SELECT [name], COUNT(l.database_id) AS 'vlf_count' 
FROM sys.databases s
CROSS APPLY sys.dm_db_log_info(s.database_id) l
GROUP BY [name]
HAVING COUNT(l.database_id) > 100
```

### <a name="b-determing-the-position-of-the-last-vlf-in-transaction-log-before-shrinking-the-log-file"></a>B. `VLF`로그 파일을 축소 하기 전에 트랜잭션 로그의 마지막 위치를 판단 합니다.

다음 쿼리를 사용 하면 트랜잭션 로그에서 shrinkfile를 실행 하기 전에 마지막 활성 VLF의 위치를 확인 하 여 트랜잭션 로그를 축소할 수 있는지 여부를 확인할 수 있습니다.

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

## <a name="see-also"></a>참고 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_stats&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)

