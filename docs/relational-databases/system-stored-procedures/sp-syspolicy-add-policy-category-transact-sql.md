---
title: sp_syspolicy_add_policy_category (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_syspolicy_add_policy_category
- sp_syspolicy_add_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category
ms.assetid: b682fac4-23c6-4662-8d05-c38f3b45507e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90e8fdea1ed8f177526574c5911e69fd1bc01bff
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spsyspolicyaddpolicycategory-transact-sql"></a>sp_syspolicy_add_policy_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  정책 기반 관리에 사용할 수 있는 정책 범주를 추가합니다. 정책 범주를 사용하면 정책을 구성하고 정책 범위를 설정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_add_policy_category [ @name = ] 'name'  
    [ , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
    , [ @policy_category_id = ] policy_category_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ **@name=** ] **'***name***'**  
 정책 범주의 이름입니다. *이름* 은 **sysname**, 이며 필수입니다. *이름* NULL 또는 빈 문자열일 수 없습니다.  
  
 [ **@mandate_database_subscriptions =** ] *mandate_database_subscriptions*  
 정책 범주에 대해 데이터베이스 구독이 위임되는지 여부를 결정합니다. *mandate_database_subscriptions* 는 **비트** 값 이며 기본값은 1 (사용).  
  
 [ **@policy_category_id=** ] *policy_category_id*  
 정책 범주의 식별자입니다. *policy_category_id* 은 **int**를 출력으로 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syspolicy_add_policy_categor는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  자격 증명 승격할 수: PolicyAdministratorRole 역할의 사용자가 서버 트리거를 만들 하 고 인스턴스의 작업에 영향을 줄 수 있는 정책 실행을 예약할 수는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]합니다. 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 범주 구독이 위임되지 않는 정책 범주를 만듭니다. 즉, 범주의 정책에 참여하거나 참여하지 않도록 개별 데이터베이스를 구성할 수 있습니다.  
  
```  
DECLARE @policy_category_id int;  
  
EXEC msdb.dbo.sp_syspolicy_add_policy_category  
  @name = N'Table Naming Policies'  
, @mandate_database_subscriptions = 0  
, @policy_category_id = @policy_category_id OUTPUT;  
  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_add_policy_category_subscription &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)   
 [sp_syspolicy_delete_policy_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)  
  
  
