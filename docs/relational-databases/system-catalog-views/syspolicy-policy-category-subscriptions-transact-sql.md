---
title: syspolicy_policy_category_subscriptions (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_category_subscriptions_TSQL
- syspolicy_policy_category_subscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_group_subscriptions view
ms.assetid: b3b3a7d7-0b78-46c0-9755-045f7a5692b9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00769d103e49a06beb4c70ca52eff8d09afd3f9b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="syspolicypolicycategorysubscriptions-transact-sql"></a>syspolicy_policy_category_subscriptions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 정책 기반 관리 구독에 대해 한 행을 표시합니다. 각 행에 대상 및 정책 범주 쌍에 설명 합니다. 다음 표에서는 syspolicy_policy_group_subscriptions 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|policy_category_subscription_id|**int**|이 레코드의 ID입니다.|  
|target_type|**sysname**|이 구독의 대상인 데이터베이스 개체의 유형입니다.|  
|target_object|**sysname**|대상 개체의 이름입니다.|  
|policy_category_id|**int**|대상에 적용된 정책 범주의 ID입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 정책 범주로 구독되는 대상을 표시합니다.  
  
## <a name="permissions"></a>Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
