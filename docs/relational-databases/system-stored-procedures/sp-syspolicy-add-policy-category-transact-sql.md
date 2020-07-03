---
title: sp_syspolicy_add_policy_category (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_add_policy_category
- sp_syspolicy_add_policy_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_add_policy_category
ms.assetid: b682fac4-23c6-4662-8d05-c38f3b45507e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ca8eca5643fb0021111c00abdce45e6de2c09878
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892764"
---
# <a name="sp_syspolicy_add_policy_category-transact-sql"></a>sp_syspolicy_add_policy_category(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  정책 기반 관리에 사용할 수 있는 정책 범주를 추가합니다. 정책 범주를 사용하면 정책을 구성하고 정책 범위를 설정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syspolicy_add_policy_category [ @name = ] 'name'  
    [ , [ @mandate_database_subscriptions = ] mandate_database_subscriptions ]  
    , [ @policy_category_id = ] policy_category_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'`정책 범주의 이름입니다. *name* 은 **sysname**이며 필수입니다. *이름은* NULL 이거나 빈 문자열일 수 없습니다.  
  
`[ @mandate_database_subscriptions = ] mandate_database_subscriptions`정책 범주에 대해 데이터베이스 구독이 위임 되는지 여부를 결정 합니다. *mandate_database_subscriptions* 은 **비트** 값 이며 기본값은 1 (사용)입니다.  
  
`[ @policy_category_id = ] policy_category_id`정책 범주의 식별자입니다. *policy_category_id* 은 **int**이며 OUTPUT으로 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syspolicy_add_policy_categor는 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 PolicyAdministratorRole 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
> [!IMPORTANT]  
>  자격 증명의 승격 가능: Policy관리자 역할 역할의 사용자는 서버 트리거를 만들고 인스턴스 작업에 영향을 줄 수 있는 정책 실행을 예약할 수 있습니다 [!INCLUDE[ssDE](../../includes/ssde-md.md)] . 예를 들어 PolicyAdministratorRole 역할의 사용자는 대부분의 개체가 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 생성되지 않도록 할 수 있는 정책을 만들 수 있습니다. 이렇게 자격 증명을 승격할 수 있기 때문에 PolicyAdministratorRole 역할은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성을 제어할 수 있도록 신뢰할 수 있는 사용자에게만 부여되어야 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;정책 기반 관리 저장 프로시저](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_add_policy_category_subscription &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)   
 [Transact-sql&#41;sp_syspolicy_delete_policy_category &#40;](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)  
  
  
