---
title: 데이터베이스 메일 메시징 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
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
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71445835763436cae2e37fa114ff06db8e8855d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="database-mail-messaging-objects"></a>데이터베이스 메일 메시징 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **msdb** 데이터베이스는 데이터베이스 메일 호스트 데이터베이스입니다. 이 데이터베이스에는 데이터베이스 메일 지원을 위한 저장 프로시저와 메시징 개체가 있습니다. Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 데이터베이스 메일을 사용하고 프로필과 계정을 만들어 관리하고 데이터베이스 메일 옵션을 구성하기 위한 데이터베이스 메일 구성 마법사가 포함되어 있습니다.  
  
##  <a name="ComponentsAndConcepts"></a>**msdb** 데이터베이스의 개체  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 **msdb** 데이터베이스에서 사용할 수 있어야 합니다. 그러나 데이터베이스 메일은 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 네트워킹을 사용하지 않습니다. 따라서 사용자는 데이터베이스 메일을 사용하기 위해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 끝점을 만들 필요가 없습니다. 외부 데이터베이스 메일 프로세스는 표준 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신합니다.  
  
 데이터베이스 메일은 데이터베이스 메일을 설정할 때 **msdb** 데이터베이스에 다음 개체를 표시합니다.  
  
 이러한 개체는 메일 호스트 데이터베이스 내에서 데이터베이스 메일에 대한 인터페이스입니다. 위에 나열된 개체에서 제공하는 기능을 구현하도록 다른 개체가 설치됩니다. 그러나 해당 개체는 내부 사용을 위해 예약됩니다.  
  
|속성|형식|Description|  
|----------|----------|-----------------|  
|[sysmail_allitems&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)|**보기**|데이터베이스 메일에 제출된 모든 메시지를 나열합니다.|  
|[sysmail_event_log&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)|**보기**|[Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md)의 동작에 대한 메시지를 나열합니다.|  
|[sysmail_faileditems&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)|**보기**|데이터베이스 메일에서 전송할 수 없었던 메시지에 대한 정보입니다.|  
|[sysmail_mailattachments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)|**보기**|데이터베이스 메일 메시지의 첨부 파일에 대한 정보입니다.|  
|[sysmail_sentitems&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)|**보기**|데이터베이스 메일을 사용하여 전송된 메시지에 대한 정보입니다.|  
|[sysmail_unsentitems&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)|**보기**|데이터베이스 메일이 현재 전송 시도 중인 메시지에 대한 정보입니다.|  
|[sp_send_dbmail&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)|**저장 프로시저**|데이터베이스 메일을 사용하여 전자 메일 메시지를 보냅니다.|  
|[sysmail_delete_log_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|**저장 프로시저**|데이터베이스 메일 로그에서 메시지를 삭제합니다.|  
|[sysmail_delete_mailitems_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)|**저장 프로시저**|데이터베이스 메일 큐에서 메일 항목을 삭제합니다.|  
|[sysmail_help_status_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql.md)|**저장 프로시저**|데이터베이스 메일이 시작되었는지 여부를 나타냅니다.|  
|[sysmail_start_sp(Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)|**저장 프로시저**|외부 프로그램에서 사용하는 Service Broker 개체를 시작합니다. 이러한 개체는 기본적으로 시작됩니다.|  
|[sysmail_stop_sp(Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)|**저장 프로시저**|외부 프로그램에서 사용하는 Service Broker 개체를 중지합니다.|  
  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
