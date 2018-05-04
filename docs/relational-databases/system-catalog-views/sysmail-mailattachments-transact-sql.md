---
title: sysmail_mailattachments (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d4d4e5088f0ec91fc8de28b1c82886b7bc26419
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일로 제출된 각 첨부 파일당 한 개의 행을 포함합니다. 이 뷰를 사용하여 데이터베이스 메일 첨부 파일에 대한 정보를 볼 수 있습니다. 데이터베이스 메일을 사용 하 여 처리 하는 모든 전자 메일을 검토 하려면 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|첨부 파일의 ID입니다.|  
|**mailitem_id**|**int**|첨부 파일을 포함하는 메일 항목의 식별자입니다.|  
|**filename**|**nvarchar(520)**|첨부 파일의 파일 이름입니다. 때 **attach_query_result** 는 1 및 **query_attachment_filename** 가 NULL 이면 데이터베이스 메일에서 임의로 파일 이름을 만듭니다.|  
|**filesize**|**int**|첨부 파일의 크기(바이트)입니다.|  
|**attachment**|**varbinary(max)**|첨부 파일의 내용입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 문제를 해결할 때 이 뷰를 사용하여 첨부 파일을 속성을 확인할 수 있습니다.  
  
 첨부 파일 시스템 테이블에 저장 될 수 있습니다는 **msdb** 증가 하는 데이터베이스입니다. 사용 하 여 **sysmail_delete_mailitems_sp** 메일 항목 및 관련된 첨부 파일을 삭제 하려면. 자세한 내용은 참조 [보관 데이터베이스 메일 메시지 및 이벤트 로그와 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 에 부여 된 **sysadmin** 고정된 서버 역할 및 **DatabaseMailUserRole** 데이터베이스 역할입니다. 멤버에 의해 실행 된 **sysadmin** 이 뷰는 모든 첨부 파일이 표시 고정 서버 역할입니다. 다른 모든 사용자는 자신이 제출한 메시지의 첨부 파일만 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
