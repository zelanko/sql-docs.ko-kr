---
title: '데이터베이스 메일: 메일이 지연되고 배달되지 않음 | Microsoft Docs'
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92ff867d98b83f1934972a576df8295c3f9ca79d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70228416"
---
# <a name="database-mail-mail-queued-not-delivered"></a>데이터베이스 메일: 메일이 지연되고 배달되지 않음 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

이 항목은 전자 메일 메시지가 정상적으로 큐에 들어가지만 메시지가 배달되지 않는 문제의 해결 방법을 설명합니다.

## <a name="diagnose-the-problem"></a>문제 진단 

데이터베이스 메일 외부 프로그램은 이메일 작업을 **msdb** 데이터베이스에 기록합니다.

먼저 데이터베이스 메일을 사용하는지 확인하기 위해 다음 예제에서처럼 **sp_configure** 시스템 저장 프로시저의 [Database Mail XPs 옵션](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)을 사용합니다.

```sql 
EXEC sp_configure 'show advanced', 1;  
RECONFIGURE; 
EXEC sp_configure; 
GO
```

그런 다음, **msdb** 데이터베이스에서 다음 명령문을 실행하여 메일 큐의 상태를 확인합니다.

```sql
sysmail_help_queue_sp @queue_type = 'Mail' ;
```

열에 대한 자세한 설명은 [sysmail_help_queue_sp(Transact-SQL)](../system-stored-procedures/sysmail-help-queue-sp-transact-sql.md#result-set)를 참조하세요.

**sysmail_event_log** 뷰에서 작업을 확인합니다. 뷰에는 데이터베이스 메일 외부 프로그램이 시작되었음을 나타내는 항목이 있어야 합니다. **sysmail_event_log** 뷰에 항목이 없는 경우 **sysmail_event_log**에서 [메시지가 지연되고 항목이 없음](database-mail-common-errors.md#database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log) 증상을 참조하세요. **sysmail_event_log** 뷰에 오류가 있는 경우 특정 오류의 문제를 해결하세요.

**sysmail_event_log** 뷰에 항목이 있는 경우 **sysmail_allitems** 뷰에서 메시지의 상태를 확인합니다.

## <a name="message-status-unsent"></a>메시지 상태 unsent 

**unsent** 상태는 [데이터베이스 메일 외부 프로그램](database-mail-external-program.md)이 아직 이메일 메시지를 처리하지 않았음을 나타냅니다. 데이터베이스 메일 외부 프로그램의 메시지 처리가 지연되었을 수 있습니다. 외부 프로그램의 메시지 처리 속도는 네트워크 상태, 다시 시도 제한 시간, 메시지 양 및 SMTP 서버 용량에 따라 달라집니다. 문제가 지속될 경우 둘 이상의 프로필을 사용하여 둘 이상의 SMTP 서버에 메시지를 분산하는 방법을 고려해 보십시오.

성공적으로 배달된 메시지의 최근 수정 날짜를 확인하십시오. 마지막 배달 성공 날짜로부터 상당 시간이 지난 경우 sysmail_event_log 뷰를 확인하여 Service Broker가 외부 프로그램을 정상적으로 시작했는지 확인합니다. 마지막 외부 프로그램 시작 시도가 실패한 경우 데이터베이스 메일 외부 프로그램이 올바른 디렉터리에 있는지, SQL Server의 서비스 계정에 실행 파일을 실행할 권한이 있는지 확인합니다.

   > [!NOTE]
   > 보내지 않은 오래된 메시지를 삭제하려면 전달할 수 없는 메시지가 큐에서 가장 오래된 메시지가 될 때까지 기다린 다음 [sysmail_delete_mailitems_sp](../system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)를 사용하여 해당 메시지를 삭제합니다.

## <a name="message-status-retrying"></a>메시지 상태 retrying

retrying 상태는 데이터베이스 메일이 메시지를 SMTP 서버로 배달하려고 했으나 실패했음을 나타냅니다. 일반적으로 이 상태는 네트워크 손상, SMTP 서버 오류 또는 잘못 구성된 데이터베이스 메일 계정 때문에 발생합니다. 궁극적으로 메시지는 성공하거나 실패하여 이벤트 로그에 메시지를 게시해야 합니다.

## <a name="message-status-sent"></a>메시지 상태 sent

**sent** 상태는 데이터베이스 메일 외부 프로그램이 이메일 메시지를 SMTP 서버에 성공적으로 배달했음을 나타냅니다. 메시지가 대상에 도착하지 않은 경우는 SMTP 서버가 데이터베이스 메일에서 메시지를 받았으나 최종으로 받는 사람에게 메시지를 배달하지 못한 것입니다. SMTP 서버의 로그를 확인하거나 SMTP 서버 관리자에게 문의하십시오. Outlook Express와 같은 다른 클라이언트를 사용하여 SMTP 메일 서버를 테스트할 수도 있습니다.

## <a name="message-status-failed"></a>메시지 상태 failed

failed 상태는 데이터베이스 메일 외부 프로그램이 메시지를 SMTP 서버로 배달하지 못했음을 나타냅니다. 이 경우 **sysmail_event_log** 뷰에 외부 프로그램에서 받은 자세한 정보가 포함됩니다. **sysmail_faileditems**와 **sysmail_event_log**를 조인하여 자세한 오류 메시지를 검색하는 예제 쿼리는 [데이터베이스 메일을 통해 보낸 이메일 메시지의 상태 확인](check-the-status-of-e-mail-messages-sent-with-database-mail.md)을 참조하세요. 가장 일반적인 실패 원인은 잘못된 대상 주소이거나 외부 프로그램이 하나 이상의 장애 조치(Failover) 계정에 접근하지 못하게 하는 네트워크 문제입니다. SMTP 서버의 문제로 인해 서버가 메일을 거부할 수도 있습니다. 데이터베이스 메일 구성 마법사를 사용하여 **로깅 수준**을 **자세히**로 변경하고 테스트 메일을 보내 오류 지점을 조사합니다.



##  <a name="RelatedContent"></a> 참고 항목
  
-  [데이터베이스 메일 개요](database-mail.md)

  
  
