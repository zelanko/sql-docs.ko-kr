---
title: sp_syspolicy_delete_policy_category_subscription (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_syspolicy_delete_policy_category_subscription_TSQL
- sp_syspolicy_delete_policy_category_subscription
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_delete_policy_category_subscription
ms.assetid: eeab0120-c869-4c95-a79d-6dc418d0b23a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed35ec758bbdf05594275f47482169db93a1e088
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spsyspolicydeletepolicycategorysubscription-transact-sql"></a>sp_syspolicy_delete_policy_category_subscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특정 데이터베이스의 정책 범주 구독을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_delete_policy_category_subscription [ @policy_category_subscription_id = ] policy_category_subscription_id  
```  
  
## <a name="arguments"></a>인수  
 [ **@policy_category_subscription_id=** ] *policy_category_subscription_id*  
 정책 범주 구독의 식별자입니다. *policy_category_subscription_id* 은 **int**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syspolicy_delete_policy_category_subscription은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 구독이 위임된 경우에는 정책 범주 구독을 삭제할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저는 현재 저장 프로시저 소유자의 컨텍스트에서 실행됩니다.  
  
 에 대 한 값을 가져오려면 *policy_category_subscription_id*, 다음 쿼리를 사용할 수 있습니다.  
  
```  
SELECT a.policy_category_subscription_id, a.target_object, b.name AS category_name  
FROM msdb.dbo.syspolicy_policy_category_subscriptions AS a  
INNER JOIN msdb.dbo.syspolicy_policy_categories AS b  
ON a.policy_category_id = b.policy_category_id;  
```  
  
## <a name="examples"></a>예  
 다음 예에서는 ID가 1인 정책 범주 구독을 삭제합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_delete_policy_category_subscription @policy_category_subscription_id = 1;  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_update_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)  
  
  
