---
title: sys.dm_cdc_log_scan_sessions (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs: TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6db4f34391cf36757ed086b24ddfe3618ebbe529
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="change-data-capture---sysdmcdclogscansessions"></a>변경 데이터 캡처-sys.dm_cdc_log_scan_sessions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스의 각 로그 검색 세션에 대해 한 개의 행을 반환합니다. 반환된 마지막 행은 현재 세션을 나타냅니다. 이 뷰를 사용하면 현재 로그 검색 세션에 대한 상태 정보, 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 마지막으로 시작된 이후의 모든 세션에 대한 집계 정보를 반환할 수 있습니다.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|세션의 ID입니다.<br /><br /> 0일 경우 이 행에서 반환된 데이터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 마지막으로 시작된 이후의 모든 세션에 대한 집계입니다.|  
|**start_time**|**datetime**|세션의 시작 시간입니다.<br /><br /> 때 **session_id** 가 0 일에서 집계 된 데이터 수집을 시작한 시간입니다.|  
|**end_time**|**datetime**|세션의 종료 시간입니다.<br /><br /> NULL인 경우 세션이 활성 상태입니다.<br /><br /> 때 **session_id** = 0 인 마지막 세션이 종료 된 시간입니다.|  
|**duration**|**bigint**|세션의 기간(초)입니다.<br /><br /> 0인 경우 세션에 변경 데이터 캡처 트랜잭션이 포함되어 있지 않습니다.<br /><br /> 때 **session_id** = 0, 기간 (초)의 변경 데이터 캡처 트랜잭션 포함 된 모든 세션의 합계입니다.|  
|**scan_phase**|**nvarchar(200)**|세션의 현재 단계입니다. 가능한 값 및 해당 설명을 보려면은 다음과 같습니다.<br /><br /> 1: 구성 읽기<br />2: 첫 번째 검색, 해시 테이블 작성<br />3: 두 번째 검색<br />4: 두 번째 검색<br />5: 두 번째 검색<br />6: 스키마 버전 관리<br />7: 마지막 검사<br />8: 완료<br /><br /> 때 **session_id** = 0 이면이 값은 항상 "Aggregate"입니다.|  
|**error_count**|**int**|오류가 발생한 횟수입니다.<br /><br /> 때 **session_id** = 0, 모든 세션에 있는 오류의 총 수입니다.|  
|**start_lsn**|**nvarchar(23)**|세션의 시작 LSN입니다.<br /><br /> 때 **session_id** = 0, 마지막 세션에 대 한 시작 LSN입니다.|  
|**current_lsn**|**nvarchar(23)**|현재 검색 중인 LSN입니다.<br /><br /> 때 **session_id** = 0, 현재 LSN은 0입니다.|  
|**end_lsn**|**nvarchar(23)**|세션의 종료 LSN입니다.<br /><br /> NULL인 경우 세션이 활성 상태입니다.<br /><br /> 때 **session_id** = 0, 마지막 세션에 대 한 끝 LSN입니다.|  
|**tran_count**|**bigint**|처리된 변경 데이터 캡처 트랜잭션의 수입니다. 이 카운터는 2 단계에서 채워집니다.<br /><br /> 때 **session_id** = 0, 모든 세션에서 처리 된 트랜잭션의 수입니다.|  
|**last_commit_lsn**|**nvarchar(23)**|처리된 마지막 커밋 로그 레코드의 LSN입니다.<br /><br /> 때 **session_id** = 0, 마지막 커밋 로그 레코드 LSN 모든 세션에 대 한 합니다.|  
|**last_commit_time**|**datetime**|마지막 커밋 로그 레코드가 처리된 시간입니다.<br /><br /> 때 **session_id** = 0, 모든 세션에 대 한 마지막 커밋 로그 레코드 시간입니다.|  
|**log_record_count**|**bigint**|검색된 로그 레코드 수입니다.<br /><br /> 때 **session_id** = 0, 모든 세션에 대해 검색 된 레코드 수입니다.|  
|**schema_change_count**|**int**|탐지된 DDL(데이터 정의 언어) 작업 수입니다. 이 카운터는 6단계에서 채워집니다.<br /><br /> 때 **session_id** = 0, 모든 세션에서 처리 된 DDL 작업의 수입니다.|  
|**command_count**|**bigint**|처리된 명령 수입니다.<br /><br /> 때 **session_id** = 0, 모든 세션에서 처리 된 명령 수입니다.|  
|**first_begin_cdc_lsn**|**nvarchar(23)**|변경 데이터 캡처 트랜잭션을 포함하는 첫 번째 LSN입니다.<br /><br /> 때 **session_id** = 0, 변경 데이터 캡처 트랜잭션을 포함 하는 첫 번째 LSN입니다.|  
|**last_commit_cdc_lsn**|**nvarchar(23)**|변경 데이터 캡처 트랜잭션을 포함하는 마지막 커밋 로그 레코드의 LSN입니다.<br /><br /> 때 **session_id** 세션이 포함 된 변경 데이터 캡처 트랜잭션을 대 한이 0 이면 마지막 커밋 로그 레코드 LSN|  
|**last_commit_cdc_time**|**datetime**|변경 데이터 캡처 트랜잭션을 포함하는 마지막 커밋 로그 레코드가 처리된 시간입니다.<br /><br /> 때 **session_id** = 0, 세션이 포함 된 변경 데이터 캡처 트랜잭션을 대 한 마지막 커밋 로그 레코드 시간입니다.|  
|**대기 시간**|**int**|차이 (초) 사이 **end_time** 및 **last_commit_cdc_time** 세션에서 합니다. 이 카운터는 7단계의 마지막에 채워집니다.<br /><br /> 때 **session_id** = 0 인 세션에 기록 된 마지막 대기 시간은 0이 아닌 값입니다.|  
|**empty_scan_count**|**int**|변경 데이터 캡처 트랜잭션을 포함하지 않은 연속적인 세션 수입니다.|  
|**failed_sessions_count**|**int**|실패한 세션 수입니다.|  
  
## <a name="remarks"></a>주의  
 이 동적 관리 뷰의 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작할 때마다 다시 설정됩니다.  
  
## <a name="permissions"></a>Permissions  
 쿼리하려면 VIEW DATABASE STATE 권한이 필요는 **sys.dm_cdc_log_scan_sessions** 동적 관리 뷰. 동적 관리 뷰 사용 권한에 대 한 자세한 내용은 참조 [동적 관리 뷰 및 함수 &#40; Transact SQL &#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 세션에 대한 정보를 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase  
    error_count, start_lsn, current_lsn, end_lsn, tran_count  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_cdc_errors &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

