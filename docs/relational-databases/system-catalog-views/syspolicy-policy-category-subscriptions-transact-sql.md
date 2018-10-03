---
title: syspolicy_policy_category_subscriptions (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 845b665c108c2d91ef5876667e71a5c883ec8e80
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735021"
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 정책 기반 관리 구독에 대해 한 행을 표시합니다. 각 행에는 대상 및 정책 범주 쌍을 설명합니다. 다음 표에서는 syspolicy_policy_group_subscriptions 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|이 레코드의 ID입니다.|  
|target_type|**sysname**|이 구독의 대상인 데이터베이스 개체의 유형입니다.|  
|target_object|**sysname**|대상 개체의 이름입니다.|  
|policy_category_id|**int**|대상에 적용된 정책 범주의 ID입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 정책 범주로 구독되는 대상을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
