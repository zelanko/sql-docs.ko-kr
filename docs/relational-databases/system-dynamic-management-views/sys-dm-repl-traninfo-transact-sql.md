---
description: sys.dm_repl_traninfo(Transact-SQL)
title: sys. dm_repl_traninfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_traninfo
- dm_repl_traninfo
- sys.dm_repl_traninfo_TSQL
- dm_repl_traninfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_traninfo dynamic management view
ms.assetid: 5abe2605-0506-46ec-82b5-6ec08428ba13
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ccac1a54db0fb5395f76205713fe65c9cba3f8e1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542110"
---
# <a name="sysdm_repl_traninfo-transact-sql"></a>sys.dm_repl_traninfo(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 복제 트랜잭션 또는 변경 데이터 캡처 트랜잭션에 대한 정보를 반환합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fp2p_pub_exists**|**tinyint**|트랜잭션이 피어 투 피어 트랜잭션 복제를 통해 게시된 데이터베이스에 있는지 여부를 지정합니다. true이면 값이 1이고, 그렇지 않으면 0입니다.|  
|**db_ver**|**int**|데이터베이스 버전입니다.|  
|**comp_range_address**|**varbinary(8)**|건너 뛰어야 할 부분 롤백 범위를 정의합니다.|  
|**textinfo_address**|**varbinary(8)**|캐시된 텍스트 정보 구조의 메모리 내 주소입니다.|  
|**fsinfo_address**|**varbinary(8)**|캐시된 파일 스트림 정보 구조의 메모리 내 주소입니다.|  
|**begin_lsn**|**nvarchar (64)**|트랜잭션에 대한 시작 로그 레코드의 LSN(로그 시퀀스 번호)입니다.|  
|**commit_lsn**|**nvarchar (64)**|트랜잭션에 대한 커밋 로그 레코드의 LSN입니다.|  
|**dbid**|**smallint**|데이터베이스 ID입니다.|  
|**rows**|**int**|트랜잭션 내 복제된 명령의 ID입니다.|  
|**xdesid**|**nvarchar (64)**|트랜잭션 ID입니다.|  
|**artcache_table_address**|**varbinary(8)**|이 트랜잭션에 대해 마지막으로 사용된 캐시된 테이블 아티클 구조의 메모리 내 주소입니다.|  
|**server**|**nvarchar (514)**|서버 이름입니다.|  
|**server_len_in_bytes**|**smallint**|서버 이름의 문자 길이(바이트)입니다.|  
|**database**|**nvarchar (514)**|데이터베이스 이름|  
|**db_len_in_bytes**|**smallint**|데이터베이스 이름의 문자 길이(바이트)입니다.|  
|**송신자**|**nvarchar (514)**|트랜잭션이 시작된 서버의 이름입니다.|  
|**originator_len_in_bytes**|**smallint**|트랜잭션이 시작된 서버의 문자 길이(바이트)입니다.|  
|**orig_db**|**nvarchar (514)**|트랜잭션이 시작된 데이터베이스의 이름입니다.|  
|**orig_db_len_in_bytes**|**smallint**|트랜잭션이 시작된 데이터베이스의 문자 길이(바이트)입니다.|  
|**cmds_in_tran**|**int**|현재 트랜잭션에서 복제된 명령의 수이며 논리적 트랜잭션의 커밋 시기를 결정하는 데 사용됩니다.|  
|**is_boundedupdate_singleton**|**tinyint**|고유 열 업데이트가 단일 행에만 영향을 주는지 여부를 지정합니다.|  
|**begin_update_lsn**|**nvarchar (64)**|고유 열 업데이트에 사용된 LSN입니다.|  
|**delete_lsn**|**nvarchar (64)**|업데이트의 일부로 삭제할 LSN입니다.|  
|**last_end_lsn**|**nvarchar (64)**|논리적 트랜잭션의 마지막 LSN입니다.|  
|**fcomplete**|**tinyint**|명령이 부분 업데이트인지 여부를 지정합니다.|  
|**fcompensated**|**tinyint**|트랜잭션이 부분 롤백에 사용되는지 여부를 지정합니다.|  
|**fprocessingtext**|**tinyint**|트랜잭션에 BLOB(Binary Large Object) 데이터 형식 열이 포함되는지 여부를 지정합니다.|  
|**max_cmds_in_tran**|**int**|논리적 트랜잭션의 최대 명령 수이며 로그 판독기 에이전트가 지정합니다.|  
|**begin_time**|**datetime**|트랜잭션의 시작 시간입니다.|  
|**commit_time**|**datetime**|트랜잭션이 커밋된 시간입니다.|  
|**session_id**|**int**|변경 데이터 캡처 로그 스캔 세션의 ID입니다. 이 열은 [dm_cdc_logscan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)의 **session_id** 열에 매핑됩니다.|  
|**session_phase**|**int**|오류 발생한 시점의 세션 단계를 나타내는 번호입니다. 이 열은 [dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)의 **phase_number** 열에 매핑됩니다.|  
|**is_known_cdc_tran**|**bit**|변경 데이터 캡처로 추적된 트랜잭션을 나타냅니다.<br /><br /> 0 = 트랜잭션 복제 트랜잭션<br /><br /> 1 = 변경 데이터 캡처 트랜잭션|  
|**error_count**|**int**|오류가 발생한 횟수입니다.|  
  
## <a name="permissions"></a>사용 권한  
 변경 데이터 캡처에 설정된 데이터베이스 또는 게시 데이터베이스에 대한 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 현재 아티클 캐시에 로드되어 있는 변경 데이터 캡처에 설정된 테이블이나 복제된 데이터베이스 개체에 대한 정보만 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [복제 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)   
 [변경 데이터 캡처 관련 동적 관리 뷰&#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)  
  
  

