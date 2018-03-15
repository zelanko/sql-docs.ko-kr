---
title: END CONVERSATION(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- END DIALOG
- END CONVERSATION
- END_DIALOG_TSQL
- END_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [Service Broker], conversations
- dialogs [Service Broker], ending
- closing conversations
- END CONVERSATION statement
- conversations [Service Broker], ending
- ending conversations [SQL Server]
ms.assetid: 4415a126-cd22-4a5e-b84a-d8c68515c83b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d68dcecf84cb24b0c06876d40742c8f5ffe8124d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="end-conversation-transact-sql"></a>END CONVERSATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 대화의 한 쪽을 종료합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
END CONVERSATION conversation_handle  
   [   [ WITH ERROR = failure_code DESCRIPTION = 'failure_text' ]  
     | [ WITH CLEANUP ]  
    ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *conversation_handle*  
 종료할 대화의 대화 핸들입니다.  
  
 WITH ERROR =*failure_code*  
 오류 코드입니다. *failure_code*는 **int** 형식입니다. 오류 코드는 대화의 다른 쪽으로 보낸 오류 메시지에 포함되는 사용자 정의 코드입니다. 오류 코드는 0보다 커야 합니다.  
  
 DESCRIPTION =*failure_text*  
 오류 메시지입니다. *failure_text*는 **nvarchar(3000)** 형식입니다. 오류 텍스트는 다른 쪽의 대화로 보낸 오류 메시지에 포함되는 사용자 정의 텍스트입니다.  
  
 WITH CLEANUP  
 대화에 참가하는 양자 중 정상적으로 완료할 수 없는 한쪽의 모든 메시지와 카탈로그 뷰 항목을 제거합니다. 다른 쪽은 정리에 대한 알림을 받지 못합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 대화 끝점, 전송 큐의 모든 대화 메시지 및 서비스 큐의 모든 대화 메시지를 삭제합니다. 관리자는 이 옵션을 사용하여 정상적으로 완료할 수 없는 대화를 제거할 수 있습니다. 예를 들어 원격 서비스가 영구적으로 제거된 경우 관리자는 WITH CLEANUP을 사용하여 해당 서비스에 대한 대화를 제거할 수 있습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 응용 프로그램의 코드에서는 WITH CLEANUP을 사용하지 마십시오. 수신 끝점에서 메시지 수신 사실을 알리기 전에 END CONVERSATION WITH CLEANUP이 실행되면 전송 끝점이 해당 메시지를 다시 전송합니다. 이 경우 대화가 다시 실행될 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 대화를 종료하면 제공된 *conversation_handle*이 속하는 대화 그룹이 잠깁니다. 대화가 종료되면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 서비스 큐에서 모든 대화 메시지를 제거합니다.  
  
 대화가 종료되면 응용 프로그램은 해당 대화의 메시지를 더 이상 보내거나 받을 수 없습니다. 대화 참가자 모두 END CONVERSATION을 호출하여 대화를 완료해야 합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]이 대화의 다른 참가자로부터 대화 종료 메시지나 오류 메시지를 받지 못한 경우에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 대화의 다른 참가자에게 대화가 종료되었음을 알립니다. 이런 경우 대화 핸들이 더 이상 유효하지 않아도 대화의 끝점은 원격 서비스를 호스팅하는 인스턴스가 메시지를 승인할 때까지 활성 상태로 유지됩니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]이 대화에 대한 대화 종료 또는 오류 메시지를 아직 처리하지 못한 경우에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 원격 대화 상대에게 대화가 종료되었음을 알립니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 원격 서비스로 보내는 메시지는 지정된 옵션에 따라 다릅니다.  
  
-   오류 없이 대화가 종료되고 원격 서비스에 대한 대화가 아직 활성 상태인 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]은 원격 서비스로 `http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog` 유형의 메시지를 보냅니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 이 메시지를 대화 순서에 따라 전송 큐에 추가합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 이 메시지를 보내기 전에 현재 전송 큐에 있는 이 대화의 모든 메시지를 보냅니다.  
  
-   오류가 발생하여 대화가 종료되고 원격 서비스에 대한 대화가 아직 활성 상태인 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 원격 서비스로 `http://schemas.microsoft.com/SQL/ServiceBroker/Error` 유형의 메시지를 보냅니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 현재 전송 큐에 있는 이 대화의 다른 모든 메시지를 삭제합니다.  
  
-   WITH CLEANUP 절을 사용하여 데이터베이스 관리자는 정상적으로 완료할 수 없는 대화를 제거할 수 있습니다. 이 옵션은 대화의 모든 메시지와 카탈로그 뷰 항목을 제거합니다. 이런 경우 대화의 원격측은 대화가 종료되었다는 어떠한 표시도 받지 못하며 응용 프로그램에서 보냈지만 네트워크를 통해 아직 전송되지 않은 메시지도 받을 수 없습니다. 따라서 대화를 정상적으로 완료할 수 없는 경우에는 이 옵션을 사용하지 않는 것이 좋습니다.  
  
 대화가 종료되면 대화 핸들을 지정하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 문에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오류가 발생합니다. 대화의 다른 쪽에서 이 대화에 대한 메시지가 도착하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 해당 메시지를 무시합니다.  
  
 원격 서비스에 아직 보내지 않은 대화 메시지가 있을 때 대화가 종료되면 원격 서비스는 보내지 않은 메시지를 삭제합니다. 이런 경우는 오류로 간주되지 않으며 원격 서비스는 메시지가 삭제되었다는 알림을 받지 않습니다.  
  
 WITH ERROR 절에 지정된 오류 코드는 양수여야 합니다. 음수는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 오류 메시지용으로 예약된 것입니다.  
  
 END CONVERSATION은 사용자 정의 함수에 유효하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 활성 대화를 종료하려면 현재 사용자가 대화의 소유자, sysadmin 고정 서버 역할의 멤버 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.  
  
 sysadmin 고정 서버 역할의 멤버 또는 db_owner 고정 데이터베이스 역할의 멤버는 WITH CLEANUP을 사용하여 이미 완료된 대화에 대한 메타데이터를 제거할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-ending-a-conversation"></a>1. 대화 종료  
 다음 예에서는 `@dialog_handle`로 지정된 대화를 종료합니다.  
  
```  
END CONVERSATION @dialog_handle ;  
```  
  
### <a name="b-ending-a-conversation-with-an-error"></a>2. 오류가 발생하여 대화 종료  
 다음 예에서는 처리 문이 오류를 보고할 경우 오류가 발생한 `@dialog_handle` 대화를 종료합니다. 이는 가장 간단한 오류 처리 방법이지만 일부 응용 프로그램에는 적합하지 않을 수 있습니다.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ErrorSave INT,  
        @ErrorDesc NVARCHAR(100) ;  
BEGIN TRANSACTION ;  
  
<receive and process message>  
  
SET @ErrorSave = @@ERROR ;  
  
IF (@ErrorSave <> 0)  
  BEGIN  
      ROLLBACK TRANSACTION ;  
      SET @ErrorDesc = N'An error has occurred.' ;  
      END CONVERSATION @dialog_handle   
      WITH ERROR = @ErrorSave DESCRIPTION = @ErrorDesc ;  
  END  
ELSE  
  
COMMIT TRANSACTION ;  
```  
  
### <a name="c-cleaning-up-a-conversation-that-cannot-complete-normally"></a>3. 정상적으로 완료할 수 없는 대화 정리  
 다음 예에서는 `@dialog_handle`로 지정된 대화를 종료합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 원격 서비스에게 알리지 않고 서비스 큐와 전송 큐에서 모든 메시지를 즉시 제거합니다. 정리를 사용하여 대화 상자를 종료하면 원격 서비스에 알리지 않으므로 이 방법은 원격 서비스가 **EndDialog** 또는 **Error** 메시지를 받을 수 없는 경우에만 사용해야 합니다.  
  
```  
END CONVERSATION @dialog_handle WITH CLEANUP ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN CONVERSATION TIMER&#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION&#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [sys.conversation_endpoints&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
