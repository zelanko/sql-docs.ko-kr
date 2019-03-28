---
title: sp_syspolicy_update_policy_category (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_TSQL
- sp_syspolicy_update_policy_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category
ms.assetid: 6b6413c2-7a3b-4eff-91d9-5db2011869d6
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3dfe649892c30a26024f3053c7a8a0f6c596d7c7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530615"
---
# <a name="spsyspolicyupdatepolicycategory-transact-sql"></a>sp_syspolicy_update_policy_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 구독을 위임하도록 정책 범주가 설정되는지 여부를 업데이트합니다. 구독이 위임되면 모든 데이터베이스에 정책 범주가 적용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_update_policy_category { [ @name = ] 'name' | [ @policy_category_id = ] policy_category_id }  
    , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'` 정책 범주의 이름이입니다. *이름* 됩니다 **sysname**, 경우 지정 해야 합니다 *policy_category_id* NULL입니다.  
  
`[ @policy_category_id = ] policy_category_id` 정책 범주의 식별자가입니다. *policy_category_id* 됩니다 **int**, 경우 지정 해야 합니다 *이름* NULL입니다.  
  
`[ @mandate_database_subscriptions = ] mandate_database_subscriptions` 정책 범주에 대해 데이터베이스 구독이 위임 되는지 여부를 결정 합니다. *mandate_database_subscriptions* 되는 **비트** 값 이며 기본값은 NULL입니다. 다음 값 중 하나를 사용할 수 있습니다.  
  
-   0 = 위임되지 않음  
  
-   1 = 위임됨  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 sp_syspolicy_update_policy_category는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 에 대 한 값을 지정 해야 합니다 *이름을* 용인지 *policy_category_id*합니다. 둘 다 NULL일 수는 없습니다. 이러한 값을 가져오려면 msdb.dbo.syspolicy_policy_categories 시스템 뷰를 쿼리합니다.  
  
## <a name="permissions"></a>사용 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  가능한 자격 증명 승격: PolicyAdministratorRole 역할의 사용자는 서버 트리거를 만들고 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 작업에 영향을 줄 수 있는 정책 실행을 예약할 수 있습니다. 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터베이스 구독을 위임하도록 'Finance' 범주를 업데이트합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category @name = N'Finance'  
, @mandate_database_subscriptions = 1;  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)   
 [sp_syspolicy_rename_policy_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)  
  
  
