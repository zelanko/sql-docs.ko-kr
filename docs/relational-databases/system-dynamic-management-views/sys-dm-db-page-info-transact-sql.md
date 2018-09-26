---
title: sys.dm_db_page_info (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
author: ''
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 04a301601d9313f3b7cfe38b7914e12984bdc235
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715448"
---
# <a name="sysdmdbpageinfo-transact-sql"></a>sys.dm_db_page_info (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

데이터베이스의 페이지에 대 한 정보를 반환합니다.  페이지에서 헤더 정보를 포함 하는 하나의 행을 반환 하는 함수 등을 `object_id`, `index_id`, 및 `partition_id`합니다.  이 함수를 사용 해야 대체 `DBCC PAGE` 대부분의 경우에서.

## <a name="syntax"></a>구문  
  
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>인수  
 *DatabaseId* | NULL | 기본  

 데이터베이스의 ID입니다. *DatabaseId* 됩니다 **smallint**합니다. 유효한 입력은 데이터베이스의 ID 번호. 하지만 기본값은 NULL,이 매개 변수에 대해 NULL 값을 오류가 발생 하면를 전송 합니다.
 
*FileId* | NULL | 기본

파일 ID입니다. *FileId* 됩니다 **int**합니다.  유효한 입력은 지정한 데이터베이스에 있는 파일의 ID 번호 *DatabaseId*합니다. 하지만 기본값은 NULL,이 매개 변수에 대해 NULL 값을 오류가 발생 하면를 전송 합니다.

*PageId* | NULL | 기본

페이지의 ID입니다.  *PageId* 됩니다 **int**합니다.  유효한 입력은 지정한 파일에서 페이지의 ID 번호 *FileId*합니다. 하지만 기본값은 NULL,이 매개 변수에 대해 NULL 값을 오류가 발생 하면를 전송 합니다.

*모드* | NULL | 기본

함수 출력의 세부 수준을 결정합니다. 모든 설명 열에 대해 NULL 값을 반환 합니다 '제한', '자세한' 채워집니다 설명 열입니다.  기본값은 '제한'.

## <a name="table-returned"></a>반환된 테이블  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id |ssNoversion |데이터베이스 ID |
|file_id |ssNoversion |파일 ID |
|page_id |ssNoversion |페이지 ID |
|page_type |ssNoversion |페이지 유형 |
|page_type_desc |Nvarchar(64) |페이지 유형에 대 한 설명 |
|page_flag_bits |Nvarchar(64) |페이지 머리글 플래그 비트 |
|page_flag_bits_desc |nvarchar(256) |페이지 머리글에서 플래그 비트 설명 |
|page_type_flag_bits |Nvarchar(64) |페이지 머리글에서 플래그 비트를 입력 합니다. |
|page_type_flag_bits_desc |Nvarchar(64) |페이지 머리글에서 형식 플래그 비트 설명 |
|object_id |ssNoversion |페이지를 소유 하는 개체의 ID |
|index_id |ssNoversion |인덱스 (힙 데이터 페이지에 대 한 0)의 ID |
|partition_id |BIGINT |파티션의 ID |
|alloc_unit_id |BIGINT |할당 단위 ID |
|page_level |ssNoversion |인덱스에서 페이지의 수준 (리프 = 0) |
|slot_count |SMALLINT |슬롯 개수 (사용 및 사용 하지 않는) <br> 데이터 페이지에 대 한이 숫자 행 개수와 동일합니다. |
|ghost_rec_count |SMALLINT |페이지에서 삭제할 것으로 표시 하는 레코드 수 <br> 고스트 레코드는 삭제 하도록 표시 되었지만 아직 제거할입니다. |
|torn_bits |ssNoversion |조각난된 쓰기가 검색 섹터당 1 비트입니다. 체크섬을 저장 하는 데도 사용 <br> 이 값은 데이터 손상을 검색할 사용 |
|is_iam_pg |bit |페이지는 IAM 페이지 인지 여부를 나타내는 비트  |
|is_mixed_ext |bit |비트 나타내면 혼합 익스텐트에서 할당 |
|pfs_file_id |SMALLINT |해당 하는 PFS 페이지의 파일 ID |
|pfs_page_id |ssNoversion |해당 PFS 페이지의 페이지 ID |
|pfs_alloc_percent |ssNoversion |PFS 바이트에 의해 표시 된 대로 할당 비율 |
|pfs_status |Nvarchar(64) |PFS 바이트 |
|pfs_status_desc |Nvarchar(64) |PFS 바이트의 설명 |
|gam_file_id |SMALLINT |해당 하는 GAM 페이지의 파일 ID |
|gam_page_id |ssNoversion |해당 하는 GAM 페이지의 페이지 ID |
|gam_status |bit |비트 나타내면 GAM에 할당 |
|gam_status_desc |Nvarchar(64) |GAM 상태 비트 설명 |
|sgam_file_id |SMALLINT |해당 하는 SGAM 페이지의 파일 ID |
|sgam_page_id |ssNoversion |해당 하는 SGAM 페이지의 페이지 ID |
|sgam_status |bit |비트 나타내면 SGAM에 할당 |
|sgam_status_desc |Nvarchar(64) |설명은 SGAM 상태 비트 |
|diff_map_file_id |SMALLINT |해당 하는 차등 비트맵 페이지의 파일 ID |
|diff_map_page_id |ssNoversion |해당 하는 차등 비트맵 페이지의 페이지 ID |
|diff_status |bit |Diff 상태가 변경 되는 경우를 나타내는 비트 |
|diff_status_desc |Nvarchar(64) |Diff 상태 비트 설명 |
|ml_file_id |SMALLINT |해당 하는 최소 로깅 비트맵 페이지의 파일 ID |
|ml_page_id |ssNoversion |해당 하는 최소 로깅 비트맵 페이지의 페이지 ID |
|ml_status |bit |페이지 작업이 최소한으로 로깅되는 경우를 나타내는 비트 |
|ml_status_desc |Nvarchar(64) |비트 최소 로깅의 상태에 대 한 |
|free_bytes |SMALLINT |페이지의 사용 가능한 바이트 수 |
|free_data_offset |ssNoversion |공간 데이터 영역의 끝 오프셋 |
|reserved_bytes |SMALLINT |모든 트랜잭션이 예약한 가능한 바이트 수 (하는 경우 힙) <br> 고스트 행 (경우 인덱스 리프) 수 |
|reserved_xdes_id |SMALLINT |M_xdesID m_reservedCnt 제공한 공간 <br> 디버깅 목적 으로만 |
|xdes_id |Nvarchar(64) |M_reserved 제공한 최신 트랜잭션 <br> 디버깅 목적 으로만 |
|prev_page_file_id |SMALLINT |이전 페이지 파일 ID |
|prev_page_page_id |ssNoversion |이전 페이지의 페이지 ID |
|next_page_file_id |SMALLINT |다음 페이지 파일 ID |
|next_page_page_id |ssNoversion |다음 페이지의 페이지 ID |
|min_len |SMALLINT |고정된 크기의 행의 길이 |
|lsn |Nvarchar(64) |로그 시퀀스 번호 / 타임 스탬프 |
|header_version |ssNoversion |페이지 헤더 버전 |

## <a name="remarks"></a>Remarks
합니다 `sys.dm_db_page_info` 동적 관리 함수 같은 페이지 정보를 반환 합니다. `page_id`를 `file_id`, `index_id`, `object_id` 페이지 머리글에 존재 하는 등입니다. 이 정보는 문제 해결 및 다양 한 성능 (잠금 및 래치 경합) 및 손상 문제를 디버깅 하는 데 유용 합니다.

`sys.dm_db_page_info` 대신 사용할 수는 `DBCC PAGE` 하지만 대부분의 경우에 문이 페이지 헤더 정보만 반환, 페이지의 본문에 없습니다. `DBCC PAGE` 여기서 전체 페이지의 내용이 필요한 사용 사례에 여전히 필요 합니다.

## <a name="using-in-conjunction-with-other-dmvs"></a>다른 Dmv와 함께 사용
중요 한 사용 사례 중 `sys.dm_db_page_info` 페이지 정보를 노출 하는 다른 Dmv와 조인 하는 것입니다.  새 열이 사용 사례를 용이 하 게 호출 `page_resource` 8 바이트 16 진수 형식으로 페이지 정보를 노출 하는 추가 되었습니다. 이 열에 추가 되었습니다 `sys.dm_exec_processes` 고 `sys.sysprocesses` 및 필요에 따라 나중에 다른 Dmv에 추가 됩니다.

새 함수 `sys.fn_PageResCracker`를 사용 합니다 `page_resource` 입력 및 출력 포함 된 단일 행으로 `database_id`, `file_id` 및 `page_id`.  이 함수는 간 조인이 용이 하도록 한 다음 사용할 수 있습니다 `sys.dm_exec_requests` 나 `sys.sysprocesses` 고 `sys.dm_db_page_info`입니다.

## <a name="permissions"></a>사용 권한  
필요는 `VIEW DATABASE STATE` 데이터베이스의 권한입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>1. 페이지의 모든 속성 표시
모든 페이지 정보를 사용 하 여 하나의 행을 반환 하는 다음 쿼리는 주어진 `database_id`, `file_id`, `page_id` 기본 모드 ('제한')와 함께

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdmdbpageinfo-with-other-dmvs"></a>2. 다른 Dmv sys.dm_db_page_info 사용 

다음 쿼리는 행을 하나씩 반환 `wait_resource` 에 의해 노출 `sys.dm_exec_requests` 행에 null이 아닌를 포함 하는 경우 `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```

## <a name="see-also"></a>관련 항목  
[동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[데이터베이스 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   


