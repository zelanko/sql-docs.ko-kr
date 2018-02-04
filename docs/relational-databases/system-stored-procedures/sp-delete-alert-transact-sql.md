---
title: sp_delete_alert (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_alert_TSQL
- sp_delete_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_alert
ms.assetid: a831315e-793d-41c4-8333-b324bb2bc614
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 379b9f37c84528b2ca1e03cdde2686e5c7a8a254
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spdeletealert-transact-sql"></a>sp_delete_alert(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_alert [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@name=** ] **'***name***'**  
 경고의 이름입니다. *이름* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 경고를 제거하면 해당 경고와 연관된 모든 알림도 함께 제거됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Test Alert`라는 경고를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_alert  
   @name = N'Test Alert' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_alert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
