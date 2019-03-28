---
title: sysmail_help_queue_sp (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73ca766827c1b6149bcb40cec8adefe86e944890
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531705"
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일에는 메일 큐와 상태 큐의 두 가지 큐가 있습니다. 메일 큐는 전송 대기 중인 메일 항목을 저장합니다. 상태 큐는 이미 전송된 항목의 상태를 저장합니다. 이 저장 프로시저를 사용하여 메일 또는 상태 큐의 상태를 볼 수 있습니다. 경우 매개 변수 **@queue_type** 지정 하지 않으면 저장된 프로시저는 각 큐에 대 한 하나의 행을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>인수  
`[ @queue_type = ] 'queue_type'` 로 지정 된 유형의 전자 메일을 삭제 하는 선택적 인수를 *queue_type*합니다. *queue_type* 됩니다 **nvarchar(6)** 기본값은 없습니다. 유효한 항목은 **mail** 하 고 **상태**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|큐의 유형입니다. 가능한 값은 **mail** 하 고 **상태**합니다.|  
|**length**|**int**|지정된 큐의 메일 항목 수입니다.|  
|**state**|**nvarchar(64)**|모니터의 상태입니다. 가능한 값은 **비활성** (큐가 비활성), **NOTIFIED** (큐 되었습니다 notified), 및 **RECEIVES_OCCURRING** (큐는 수신).|  
|**last_empty_rowset_time**|**DATETIME**|쿼리가 마지막으로 비워진 날짜와 시간입니다. 군대식 시간 형식 및 GMT 표준 시간대로 표시됩니다.|  
|**last_activated_time**|**DATETIME**|큐가 마지막으로 활성화된 날짜와 시간입니다. 군대식 시간 형식 및 GMT 표준 시간대로 표시됩니다.|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 메일 문제를 해결할 때 사용할 **sysmail_help_queue_sp** 큐에 있는 항목 수를 확인 하려면 마지막 및 큐의 상태를 활성화 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로의 멤버만 합니다 **sysadmin** 고정된 서버 역할에서이 절차를 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 메일 및 상태 큐를 모두 반환합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 다음 예에서는 줄 길이에 맞추어 편집된 결과 집합입니다.  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
  
