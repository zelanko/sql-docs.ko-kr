---
title: suspect_pages (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70dffcbf2ac3eac13f7ef42e901c4fcd99dce769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130547"
---
# <a name="suspectpages-transact-sql"></a>suspect_pages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사소한 오류 823 또는 824 오류를 사용 하 여 실패 한 페이지당 하나의 행을 포함 합니다. 이러한 페이지는 오류가 의심되어 이 테이블에 나열되지만 실제로는 문제가 없을 수 있습니다. 해당 상태가 업데이트 됩니다 주의 대상 페이지를 복구 하는 경우는 **event_type** 열입니다.  
  
 최대 1,000 개 행 제한에는 다음 테이블에 저장 됩니다는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|이 페이지를 적용할 데이터베이스의 ID입니다.|  
|**file_id**|**int**|데이터베이스 내 파일의 ID입니다.|  
|**page_id**|**bigint**|주의 대상 페이지의 ID입니다. 모든 페이지에는 데이터베이스에서 페이지 위치를 식별하는 32비트 값인 페이지 ID가 있습니다. 합니다 **page_id** 8KB 페이지의 데이터 파일에 대 한 오프셋 됩니다. 각 페이지 ID는 파일 내에서 고유해야 합니다.|  
|**event_type**|**int**|오류 유형으로 다음 중 하나에 해당됩니다.<br /><br /> 1 = 주의 대상 페이지를 발생시키는 823 오류(예: 디스크 오류) 또는 잘못된 체크섬이나 조각난 페이지 이외의 824 오류(예: 잘못된 페이지 ID).<br /><br /> 2 = 잘못된 체크섬.<br /><br /> 3 = 조각난 페이지.<br /><br /> 4 = 복원됨(페이지가 잘못된 것으로 표시된 후 복원됨).<br /><br /> 5 = 복구됨(DBCC가 페이지를 복구함).<br /><br /> 7 = DBCC에 의해 할당 취소됨.|  
|**error_count**|**int**|오류가 발생한 횟수입니다.|  
|**last_update_date**|**datetime**|마지막 업데이트의 날짜 및 타임스탬프입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **msdb** 에 대한 액세스 권한이 있는 사용자는 **suspect_pages** 테이블의 데이터를 읽을 수 있습니다. suspect_pages 테이블에 대한 UPDATE 권한이 있는 사용자는 레코드를 업데이트할 수 있습니다. **msdb** 의 **db_owner** 고정 데이터베이스 역할 또는 **sysadmin** 고정 서버 역할의 멤버는 레코드를 삽입, 업데이트 및 삭제할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Database Suspect Data Page 이벤트 클래스](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [시스템 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
