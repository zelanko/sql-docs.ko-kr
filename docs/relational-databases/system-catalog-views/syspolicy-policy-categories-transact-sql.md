---
title: syspolicy_policy_categories (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_categories
- syspolicy_policy_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_groups view
ms.assetid: 65f080c7-771f-4cf6-a7a0-88882c637f8d
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: dde80a20278fc49532e1bbb083a75c0b590d7a39
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024694"
---
# <a name="syspolicypolicycategories-transact-sql"></a>syspolicy_policy_categories(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 정책 기반 관리 정책 범주를 한 행으로 표시합니다. 정책 범주에는 많은 정책이 있을 때 정책을 구성할 수 있습니다. 다음 표에서는 syspolicy_policy_groups 뷰의 열을 설명합니다.  
 
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|정책 범주의 ID입니다.|  
|NAME|**sysname**|정책 범주의 이름입니다.|  
|mandate_database_subscriptions|**bit**|명시적 구독을 사용하지 않고 정책 범주를 인스턴스의 모든 데이터베이스에 적용할 것인지(1) 아니면 명시적 구독을 사용하여 정책 범주를 데이터베이스에 적용해야 하는지(0)를 표시합니다.|  
  
## <a name="remarks"></a>Remarks  
 정책 기반 관리 정책 그룹의 목록을 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
