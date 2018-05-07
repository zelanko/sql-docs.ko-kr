---
title: sp_syspolicy_update_policy_category_subscription (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_update_policy_category_subscription_TSQL
- sp_syspolicy_update_policy_category_subscription
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_update_policy_category_subscription
ms.assetid: d0769566-8f5c-4c8a-84d3-ee17ea6e0cb4
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46ca3100a203d3afc9e3b618d4264629ddf1ce58
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyspolicyupdatepolicycategorysubscription-transact-sql"></a>sp_syspolicy_update_policy_category_subscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 데이터베이스의 정책 범주 구독을 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_update_policy_category_subscription [ @policy_category_subscription_id = ] policy_category_subscription_id  
    [ , [ @target_type = ] 'target_type' ]  
    [ , [ @target_object = ] 'target_object' ]  
    , [ @policy_category = ] 'policy_category'  
```  
  
## <a name="arguments"></a>인수  
 [ **@policy_category_subscription_id=** ] *policy_category_subscription_id*  
 업데이트할 정책 범주 구독의 식별자입니다. *policy_category_subscription_id* 은 **int**, 이며 필수입니다.  
  
 [ **@target_type=** ] **'** target_type **'**  
 범주 구독의 대상 유형입니다. *target_type* 은 **sysname**, 기본값은 NULL입니다.  
  
 지정 하는 경우 *target_type*, 값 'DATABASE'으로 설정 되어 있어야 합니다.  
  
 [  **@target_object=** ] **'** target_object **'**  
 정책 범주를 구독할 데이터베이스의 이름이입니다. *target_object* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@policy_category=** ] **'** policy_category **'**  
 데이터베이스에서 구독하도록 할 정책 범주의 이름입니다. *policy_category* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syspolicy_update_policy_category_subscription은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 에 대 한 값을 가져오려면 *policy_category_subscription_id* 및 *policy_category*, 다음 쿼리를 사용할 수 있습니다.  
  
```  
SELECT a.policy_category_subscription_id, a.target_type, a.target_object  
    , b.name AS policy_category  
FROM msdb.dbo.syspolicy_policy_category_subscriptions AS a  
INNER JOIN msdb.dbo.syspolicy_policy_categories AS b  
ON a.policy_category_id = b.policy_category_id;  
```  
  
## <a name="permissions"></a>Permissions  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  자격 증명 승격할 수: PolicyAdministratorRole 역할의 사용자가 서버 트리거를 만들 하 고 인스턴스의 작업에 영향을 줄 수 있는 정책 실행을 예약할 수는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 AdventureWorks2012 데이터베이스에서 'Finance' 정책 범주를 구독하도록 기존 정책 범주 구독을 업데이트합니다.  
  
```  
EXEC msdb.dbo.sp_syspolicy_update_policy_category_subscription @policy_category_subscription_id = 1  
, @target_object = 'AdventureWorks2012'  
, @policy_category = 'Finance';  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category_subscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_delete_policy_category_subscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-subscription-transact-sql.md)  
  
  
