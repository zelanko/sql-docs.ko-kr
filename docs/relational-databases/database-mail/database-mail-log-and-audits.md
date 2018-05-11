---
title: 데이터베이스 메일 로그 및 감사 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: database-mail
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d711750d21bef54ace3d99979aaffc3a6930bfbe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="database-mail-log-and-audits"></a>데이터베이스 메일 로그 및 감사
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 메일 로깅 기능은 문제를 격리하여 수정하는 방법을 제공하도록 설계되었습니다. 데이터베이스 메일은 **msdb** 데이터베이스에 로그 정보를 저장합니다. 데이터베이스 메일 전자 메일 콘텐츠, 전자 메일의 상태, 받은 메시지(예: 오류)에 대한 정보는 데이터베이스 메일에서 로깅되며 문제 해결 및 감사 용도에 사용할 수 있습니다.  
  
## <a name="database-mail-logs"></a>데이터베이스 메일 로그  
 **msdb** 데이터베이스의 테이블은 [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md)의 정보를 기록하고 [데이터베이스 메일 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)는 문제 해결을 위해 이러한 테이블을 표시합니다. Service Broker에서 외부 프로그램을 활성화할 수 없거나 외부 프로그램에 네트워크 오류가 발생하거나 SMTP(Simple Mail Transport Protocol) 서버에서 메일 메시지를 거부하는 경우 [sysmail_event_log&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) 뷰에 오류가 나타납니다. 외부 프로그램에서 **msdb** 테이블에 기록할 수 없는 경우 해당 프로그램은 Windows 응용 프로그램 이벤트 로그에 오류를 기록합니다.  
  
 **msdb** 데이터베이스의 내부 테이블에는 데이터베이스 메일에서 전송된 메일 메시지와 첨부 파일이 각 메시지의 현재 상태와 함께 들어 있습니다. 데이터베이스 메일은 각 메시지가 처리될 때마다 이러한 테이블을 업데이트합니다.  
  
## <a name="database-mail-auditing-tasks"></a>데이터베이스 메일 감사 태스크  
  
|||  
|-|-|  
|**데이터베이스 메일 로그 검토 및 관리**|**항목 링크**|  
|개별 메시지의 배달 상태 확인|[데이터베이스 메일을 통해 보낸 전자 메일 메시지의 상태 확인](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|데이터베이스 메일 메시지, 첨부 파일 및 로그 항목 정리|[sysmail_delete_mailitems_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|데이터베이스 전자 메일 메시지 및 로그 보관|[데이터베이스 메일 메시지 및 이벤트 로그 보관을 처리하는 SQL Server 에이전트 작업 만들기](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
