---
title: LOGON 트리거 | Microsoft 문서
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68058619"
---
# <a name="logon-triggers"></a>LOGON 트리거
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  LOGON 트리거는 LOGON 이벤트에 대한 응답으로 저장 프로시저를 실행합니다. 이 이벤트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 사용자 세션이 설정된 경우 발생합니다. LOGON 트리거는 로그인의 인증 단계가 완료되었지만 사용자 세션이 실제로 설정되기 전에 발생합니다. 따라서 오류 메시지 및 PRINT 문의 메시지와 같이 일반적으로 사용자에게 전달되는 모든 트리거 내 발생 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그로 전달됩니다. 인증에 실패할 경우 LOGON 트리거는 실행되지 않습니다.  
  
 LOGON 트리거를 사용하면 로그인 작업 추적, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 로그인 제한, 특정 로그인에 대한 세션 수 제한 등의 작업을 수행하여 서버 세션을 감사하고 제어할 수 있습니다. 예를 들어 다음 코드에서 LOGON 트리거는 로그인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login_test *가 이미 3개의 사용자 세션을 만든 상태에서* 에 대한 로그인을 시도하면 해당 요청을 거부합니다.  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 LOGON 이벤트는 [이벤트 알림](../../relational-databases/service-broker/event-notifications.md)에 사용될 수 있는 AUDIT_LOGIN SQL 추적 이벤트에 해당합니다. 트리거와 이벤트 알림의 주요 차이점은 트리거는 이벤트와 동기적으로 발생하지만 이벤트 알림은 비동기적으로 발생한다는 점입니다. 즉, 세션이 설정되지 않도록 하려는 경우 등에서 LOGON 트리거를 사용해야 합니다. 이런 경우에는 AUDIT_LOGIN 이벤트의 이벤트 알림을 사용할 수 없습니다.  
  
## <a name="specifying-first-and-last-trigger"></a>첫 번째 트리거 및 마지막 트리거 지정  
 LOGON 이벤트에 여러 트리거를 정의할 수 있습니다. [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) 시스템 저장 프로시저를 사용하여 이러한 트리거 중 하나를 이벤트에서 실행될 첫 번째 트리거나 마지막 트리거로 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 남은 트리거의 실행 순서를 보장하지 않습니다.  
  
## <a name="managing-transactions"></a>트랜잭션 관리  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 LOGON 트리거를 실행하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 어느 사용자 트랜잭션에도 종속되지 않은 암시적 트랜잭션을 만듭니다. 따라서 첫 번째 LOGON 트리거가 실행을 시작하면 트랜잭션 개수가 1개입니다. 모든 LOGON 트리거가 실행을 마친 후 트랜잭션은 커밋됩니다. 다른 트리거 유형과 마찬가지로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 LOGON 트리거가 0개의 트랜잭션 개수로 실행을 마칠 경우 오류가 반환됩니다. ROLLBACK TRANSACTION 문은 중첩된 트랜잭션 내에서 문이 실행될 경우에도 트랜잭션 개수를 0으로 다시 설정합니다. COMMIT TRANSACTION은 트랜잭션 개수를 0으로 감소시킬 수 있으므로 로그온 트리거 내에서 COMMIT TRANSACTION 문을 실행하지 않는 것이 좋습니다.  
  
 LOGON 트리거 내에서 ROLLBACK TRANSACTION 문을 사용할 때는 다음을 고려하십시오.  
  
-   ROLLBACK TRANSACTION에 대한 모든 데이터 수정 사항은 롤백됩니다. 이러한 수정 사항에는 동일한 이벤트에서 실행된 이전 트리거와 현재 트리거에 의해 수정된 내용이 포함됩니다. 특정 이벤트에 대한 남은 트리거는 모두 실행되지 않습니다.  
  
-   현재 트리거는 ROLLBACK 문 다음에 표시되는 남아 있는 모든 문을 계속 실행합니다. 이 문 중에서 데이터를 수정한 경우 수정 사항은 롤백되지 않습니다.  
  
 LOGON 이벤트의 트리거가 실행되는 동안 다음 조건 중 하나라도 발생할 경우 사용자 세션이 설정되지 않습니다.  
  
-   원래 암시적 트랜잭션이 롤백되거나 실패합니다.  
  
-   심각도가 20 이상인 오류가 트리거 본문 내에 발생합니다.  
  
## <a name="disabling-a-logon-trigger"></a>로그온 트리거 비활성화  
 로그온 트리거를 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sysadmin **고정 서버 역할의 멤버를 비롯한 모든 사용자에 대해** 에 성공적으로 연결하지 못하도록 효과적으로 차단할 수 있습니다. 로그온 트리거가 연결을 차단 중인 경우 **sysadmin** 고정 서버 역할의 멤버는 관리자 전용 연결을 사용하거나 최소 구성 모드(-f)로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 시작하여 연결할 수 있습니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|Task|항목|  
|----------|-----------|  
|로그온 트리거를 만드는 방법에 대해 설명합니다. LOGON 트리거는 모든 데이터베이스에서 만들 수 있지만 서버 수준에서 등록되며 **master** 데이터베이스에 저장됩니다.|[CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)|  
|로그온 트리거를 수정하는 방법에 대해 설명합니다.|[ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|로그온 트리거를 삭제하는 방법에 대해 설명합니다.|[DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|로그온 트리거에 대한 정보를 반환하는 방법에 대해 설명합니다.|[sys.server_triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|로그온 트리거 이벤트 데이터를 캡처하는 방법에 대해 설명합니다.||  
  
## <a name="see-also"></a>참고 항목  
 [DDL 트리거](../../relational-databases/triggers/ddl-triggers.md)  
  
  
