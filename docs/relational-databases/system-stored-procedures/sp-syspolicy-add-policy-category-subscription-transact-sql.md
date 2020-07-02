---
title: sp_syspolicy_add_policy_category_subscription (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category_subscription
- sp_syspolicy_add_policy_category_subscription_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category_subscription
ms.assetid: 4284f550-9a3f-4726-8181-15e407fbf08f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9f4f60a56dff14fd06318899fdf89c5602f7029b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718644"
---
# <a name="sp_syspolicy_add_policy_category_subscription-transact-sql"></a>sp_syspolicy_add_policy_category_subscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정된 데이터베이스에 정책 범주 구독을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_add_policy_category_subscription [ @target_type = ] 'target_type'  
    , [ @target_object = ] 'target_object'  
    , [ @policy_category = ] 'policy_category'  
    [ , [ @policy_category_subscription_id = ] policy_category_subscription_id OUTPUT ]  
```  
  
## <a name="arguments"></a>인수  
`[ @target_type = ] 'target_type'`범주 구독의 대상 유형입니다. *target_type* 는 **sysname**이며, 필수 이며 ' 데이터베이스 '로 설정 해야 합니다.  
  
`[ @target_object = ] 'target_object'`범주를 구독할 데이터베이스의 이름입니다. *target_object* 는 **sysname**이며 필수입니다.  
  
`[ @policy_category = ] 'policy_category'`구독할 정책 범주의 이름입니다. *policy_category* 는 **sysname**이며 필수입니다.  
  
 *Policy_category*에 대 한 값을 가져오려면 msdb.dbo.syspolicy_policy_categories 시스템 뷰를 쿼리 합니다.  
  
`[ @policy_category_subscription_id = ] policy_category_subscription_id`범주 구독의 식별자입니다. *policy_category_subscription_id* 은 **int**이며 OUTPUT으로 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_add_policy_category_subscription은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 없는 정책 범주를 지정하면 새 정책 범주가 만들어지고 저장 프로시저를 실행할 때 모든 데이터베이스에 대해 구독이 위임됩니다. 이후에 새 범주의 위임된 구독을 제거하면 *target_object*로 지정한 데이터베이스에 대해서만 구독이 적용됩니다. 위임된 구독 설정을 변경하는 방법은 [sp_syspolicy_update_policy_category&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저는 현재 저장 프로시저 소유자의 컨텍스트에서 실행됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 'Table Naming Policies'라는 정책 범주를 구독하도록 지정된 데이터베이스를 구성합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
, @target_object = N'AdventureWorks2012'  
, @policy_category = N'Table Naming Policies';  
  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_update_policy_category_subscription &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_unsubscribe_from_policy_category &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)  
  
  
