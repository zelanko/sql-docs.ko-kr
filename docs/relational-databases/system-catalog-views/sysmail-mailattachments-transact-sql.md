---
description: sysmail_mailattachments(Transact-SQL)
title: sysmail_mailattachments (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3bdec861d8793d2943111a692d5bcde98b582cfe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460539"
---
# <a name="sysmail_mailattachments-transact-sql"></a>sysmail_mailattachments(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 메일로 제출된 각 첨부 파일당 한 개의 행을 포함합니다. 이 뷰를 사용하여 데이터베이스 메일 첨부 파일에 대한 정보를 볼 수 있습니다. 데이터베이스 메일에서 처리 하는 모든 전자 메일을 검토 하려면 [transact-sql&#41;&#40;sysmail_allitems ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|첨부 파일의 ID입니다.|  
|**mailitem_id**|**int**|첨부 파일을 포함하는 메일 항목의 식별자입니다.|  
|**filename**|**nvarchar (520)**|첨부 파일의 파일 이름입니다. **Attach_query_result** 1이 고 **query_attachment_filename** 가 NULL 이면 데이터베이스 메일는 임의의 파일 이름을 만듭니다.|  
|**filesize**|**int**|첨부 파일의 크기(바이트)입니다.|  
|**파일로**|**varbinary(max)**|첨부 파일의 내용입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 문제를 해결할 때 이 뷰를 사용하여 첨부 파일을 속성을 확인할 수 있습니다.  
  
 시스템 테이블에 저장 된 첨부 파일은 **msdb** 데이터베이스의 증가를 일으킬 수 있습니다. **Sysmail_delete_mailitems_sp** 를 사용 하 여 메일 항목 및 연결 된 첨부 파일을 삭제 합니다. 자세한 내용은 [데이터베이스 메일 메시지 및 이벤트 로그를 보관 하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 및 **DatabaseMailUserRole** 데이터베이스 역할에 부여 됩니다. **Sysadmin** 고정 서버 역할의 멤버에 의해 실행 되는 경우이 뷰는 모든 첨부 파일을 표시 합니다. 다른 모든 사용자는 자신이 제출한 메시지의 첨부 파일만 볼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sysmail_allitems &#40;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [Transact-sql&#41;sysmail_faileditems &#40;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Transact-sql&#41;sysmail_sentitems &#40;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [Transact-sql&#41;sysmail_unsentitems &#40;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
