---
title: sysmail_help_queue_sp (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c95bdba93f23bc3343a64cbf8f5ab63a2fbd209d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일에는 메일 큐와 상태 큐의 두 가지 큐가 있습니다. 메일 큐는 전송 대기 중인 메일 항목을 저장합니다. 상태 큐는 이미 전송된 항목의 상태를 저장합니다. 이 저장 프로시저를 사용하여 메일 또는 상태 큐의 상태를 볼 수 있습니다. 경우 매개 변수 **@queue_type** 를 지정 하지 않으면 저장된 프로시저가 각 큐에 대 한 하나의 행을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>인수  
 [ **@queue_type** = ] **'***queue_type***'**  
 로 지정 된 유형의 전자 메일을 삭제 하는 선택적 인수는 *queue_type*합니다. *queue_type* 은 **nvarchar(6)** 이며 기본값은 없습니다. 유효한 항목은 **메일** 및 **상태**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|큐의 유형입니다. 가능한 값은 **메일** 및 **상태**합니다.|  
|**length**|**int**|지정된 큐의 메일 항목 수입니다.|  
|**상태**|**nvarchar(64)**|모니터의 상태입니다. 가능한 값은 **비활성** (큐가 비활성 상태인), **NOTIFIED** (큐 되었습니다 되려면 확인 메일 알림을), 및 **RECEIVES_OCCURRING** (큐 수신) 합니다.|  
|**last_empty_rowset_time**|**날짜/시간**|쿼리가 마지막으로 비워진 날짜와 시간입니다. 군대식 시간 형식 및 GMT 표준 시간대로 표시됩니다.|  
|**last_activated_time**|**날짜/시간**|큐가 마지막으로 활성화된 날짜와 시간입니다. 군대식 시간 형식 및 GMT 표준 시간대로 표시됩니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 문제를 해결할 때 사용 하 여 **sysmail_help_queue_sp** 마지막 및 큐의 상태 큐에 있는 항목 수를 보려면 활성화 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만 기본적으로는 **sysadmin** 고정된 서버 역할에서이 절차를 사용할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
  
