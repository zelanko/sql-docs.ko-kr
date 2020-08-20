---
description: sys.dm_db_page_info(Transact SQL)
title: sys. dm_db_page_info (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 60df2ed8bf279bf7da8193282768124815aa6ab3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493696"
---
# <a name="sysdm_db_page_info-transact-sql"></a>sys.dm_db_page_info(Transact SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

데이터베이스의 페이지에 대 한 정보를 반환 합니다.  함수는, 및를 포함 하 여 페이지의 헤더 정보를 포함 하는 하나의 행을 반환 합니다 `object_id` `index_id` `partition_id` .  이 함수를 사용하면 대부분의 경우에서 `DBCC PAGE`를 사용할 필요가 없습니다.

> [!NOTE]
> `sys.dm_db_page_info` 는 현재 이상 에서만 지원 됩니다 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] .


## <a name="syntax"></a>구문   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>인수  
*DatabaseId* | NULL | 기본     
데이터베이스의 ID입니다. *DatabaseId* 는 **smallint**입니다. 올바른 입력은 데이터베이스의 ID 번호입니다. 기본값은 NULL 이지만이 매개 변수에 NULL 값을 전송 하면 오류가 발생 합니다.
 
*FileId* | NULL | 기본   
파일 ID입니다. *FileId* 는 **int**입니다.  유효한 입력은 *DatabaseId*로 지정 된 데이터베이스에 있는 파일의 ID 번호입니다. 기본값은 NULL 이지만이 매개 변수에 NULL 값을 전송 하면 오류가 발생 합니다.

*PageId* | NULL | 기본   
페이지의 ID입니다.  *PageId* 는 **int**입니다.  유효한 입력은 *FileId*로 지정 된 파일에 있는 페이지의 ID 번호입니다. 기본값은 NULL 이지만이 매개 변수에 NULL 값을 전송 하면 오류가 발생 합니다.

*모드* | NULL | 기본   
함수 출력의 세부 수준을 결정 합니다. ' 제한 됨 '은 모든 설명 열에 대해 NULL 값을 반환 하 고 ' DETAILED '는 설명 열을 채웁니다.  기본값은 ' 제한 됨 '입니다.

## <a name="table-returned"></a>반환된 테이블  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id |int |데이터베이스 ID |
|file_id |int |파일 ID |
|page_id |int |페이지 ID |
|page_header_version |int |페이지 머리글 버전 |
|page_type |int |페이지 유형 |
|page_type_desc |nvarchar (64) |페이지 종류에 대 한 설명 |
|page_type_flag_bits |nvarchar (64) |페이지 머리글에 플래그 비트 입력 |
|page_type_flag_bits_desc |nvarchar (64) |페이지 머리글에 플래그 비트 설명 입력 |
|page_flag_bits |nvarchar (64) |페이지 머리글의 플래그 비트 |
|page_flag_bits_desc |nvarchar(256) |페이지 헤더의 플래그 비트 설명 |
|page_lsn |nvarchar (64) |로그 시퀀스 번호/타임 스탬프 |
|page_level |int |인덱스의 페이지 수준 (리프 = 0) |
|object_id |int |페이지를 소유 하는 개체의 ID입니다. |
|index_id |int |인덱스의 ID입니다 (힙 데이터 페이지의 경우 0). |
|partition_id |bigint |파티션의 ID입니다. |
|alloc_unit_id |bigint |할당 단위의 ID입니다. |
|is_encrypted |bit |페이지가 암호화 되는지 여부를 나타내는 비트입니다. |
|has_checksum |bit |페이지에 체크섬 값이 있는지 여부를 나타내는 비트 |
|체크섬(checksum) |int |데이터 손상을 검색 하는 데 사용 되는 체크섬 값을 저장 합니다. |
|is_iam_pg |bit |페이지가 IAM 페이지 인지 여부를 나타내는 비트입니다.  |
|is_mixed_ext |bit |혼합 익스텐트에 할당 되었는지 여부를 나타내는 비트 |
|has_ghost_records |bit |페이지에 고스트 레코드가 포함 되어 있는지 여부를 나타내는 비트 <br> 삭제 된 레코드는 삭제 하도록 표시 되었지만 아직 제거 되지 않은 레코드입니다.|
|has_version_records |bit |페이지에 [가속화 된 데이터베이스 복구](../backup-restore/restore-and-recovery-overview-sql-server.md#adr) 에 사용 되는 버전 레코드가 포함 되어 있는지 여부를 나타내는 비트 |
|pfs_page_id |int |해당 PFS 페이지의 페이지 ID |
|pfs_is_allocated |bit |해당 PFS 페이지에서 페이지가 할당 된 것으로 표시 되는지 여부를 나타내는 비트입니다. |
|pfs_alloc_percent |int |해당 PFS 바이트로 표시 되는 할당 백분율 |
|pfs_status |nvarchar (64) |PFS 바이트 |
|pfs_status_desc |nvarchar (64) |PFS 바이트에 대 한 설명 |
|gam_page_id |int |해당 GAM 페이지의 페이지 ID입니다. |
|gam_status |bit |GAM에서 할당 되었는지 여부를 나타내는 비트 |
|gam_status_desc |nvarchar (64) |GAM 상태 비트에 대 한 설명 |
|sgam_page_id |int |해당 SGAM 페이지의 페이지 ID입니다. |
|sgam_status |bit |SGAM에서 할당 되었는지 여부를 나타내는 비트입니다. |
|sgam_status_desc |nvarchar (64) |SGAM 상태 비트에 대 한 설명 |
|diff_map_page_id |int |해당 하는 차등 비트맵 페이지의 페이지 ID입니다. |
|diff_status |bit |Diff 상태가 변경 되었는지 여부를 나타내는 비트 |
|diff_status_desc |nvarchar (64) |Diff 상태 비트에 대 한 설명 |
|ml_map_page_id |int |해당 하는 최소 로깅 비트맵 페이지의 페이지 ID입니다. |
|ml_status |bit |페이지가 최소 기록 되는지 여부를 나타내는 비트 |
|ml_status_desc |nvarchar (64) |최소 로깅 상태 비트의 설명입니다. |
|prev_page_file_id |smallint |이전 페이지 파일 ID |
|prev_page_page_id |int |이전 페이지 페이지 ID |
|next_page_file_id |smallint |다음 페이지 파일 ID |
|next_page_page_id |int |다음 페이지 페이지 ID |
|fixed_length |smallint |고정 크기 행의 길이 |
|slot_count |smallint |총 슬롯 수 (사용 및 사용 안 함) <br> 데이터 페이지의 경우이 숫자는 행 수와 같습니다. |
|ghost_rec_count |smallint |페이지에서 고스트로 표시 된 레코드 수 <br> 삭제 된 레코드는 삭제 하도록 표시 되었지만 아직 제거 되지 않은 레코드입니다. |
|free_bytes |smallint |페이지의 사용 가능한 바이트 수 |
|free_data_offset |int |데이터 영역 끝에서 사용 가능한 공간의 오프셋 |
|reserved_bytes |smallint |모든 트랜잭션에 예약 된 사용 가능한 바이트 수 (힙) <br> 삭제할 행 수 (인덱스 리프 인 경우) |
|reserved_bytes_by_xdes_id |smallint |M_xdesID에서 제공 하는 공간 m_reservedCnt <br> 디버깅 목적 으로만 사용 |
|xdes_id |nvarchar (64) |M_reserved에서 제공 하는 최신 트랜잭션 <br> 디버깅 목적 으로만 사용 |
||||

## <a name="remarks"></a>설명
`sys.dm_db_page_info`동적 관리 함수는 `page_id` `file_id` `index_id` `object_id` 페이지 머리글에 표시 되는,, 등의 페이지 정보를 반환 합니다. 이 정보는 다양 한 성능 (잠금 및 래치 경합) 및 손상 문제를 해결 하 고 디버깅 하는 데 유용 합니다.

`sys.dm_db_page_info` 는 `DBCC PAGE` 대부분의 경우 문 대신 사용할 수 있지만 페이지의 본문이 아닌 페이지 헤더 정보만 반환 합니다. `DBCC PAGE` 는 페이지의 전체 내용이 필요한 사용 사례에도 필요 합니다.

## <a name="using-in-conjunction-with-other-dmvs"></a>다른 Dmv와 함께 사용
의 중요 한 사용 사례 중 하나는 `sys.dm_db_page_info` 페이지 정보를 노출 하는 다른 dmv와 조인 하는 것입니다.  이 사용 사례를 용이 하 게 하기 위해 라는 새 열이 `page_resource` 추가 되어 페이지 정보를 8 바이트 16 진수 형식으로 노출 합니다. 이 열은 및에 추가 `sys.dm_exec_requests` 되었으며 `sys.sysprocesses` 나중에 필요에 따라 다른 dmv에 추가 될 예정입니다.

새 함수인는를 `sys.fn_PageResCracker` `page_resource` 입력으로 사용 하 고 `database_id` , 및를 포함 하는 단일 행을 출력 합니다 `file_id` `page_id` .  그런 다음이 함수를 사용 하 여 또는와 간의 조인을 편리 하 게 수행할 수 있습니다 `sys.dm_exec_requests` `sys.sysprocesses` `sys.dm_db_page_info` .

## <a name="permissions"></a>사용 권한  
데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` .  
  
## <a name="examples"></a>예제  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. 페이지의 모든 속성 표시
다음 쿼리는 지정 된에 대 한 모든 페이지 정보를 포함 하는 하나의 행을 `database_id` `file_id` `page_id` 기본 모드 (' 제한 됨 ')와 함께 반환 합니다.

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdm_db_page_info-with-other-dmvs"></a>B. 다른 Dmv와 함께 dm_db_page_info 사용 

다음 쿼리는 행이 null이 `wait_resource` 아닌 값 `sys.dm_exec_requests` 을 포함 하는 경우에 의해 노출 된 한 행을 반환 합니다. `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>관련 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;데이터베이스 관련 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


