---
title: 정책 기반 관리 저장 프로시저 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Policy-Based Management, stored procedures
- stored procedures [Policy-Based Management]
ms.assetid: df64ab19-4e66-4702-96bd-32ad587d00f0
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7b941921556665ef27fc20f8af706d45f44dbcd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238084"
---
# <a name="policy-based-management-stored-procedures-transact-sql"></a>정책 기반 관리 저장 프로시저(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음과 같은 시스템 정책 기반 관리에 사용 되는 프로시저를 저장 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에 문서화된 정책 기반 관리 저장 프로시저만 지원됩니다. 문서화되지 않은 저장 프로시저는 내부 정책 기반 관리 구성 요소에서만 사용하기 위한 것이므로 정책 기반 관리에 사용하면 안 됩니다.  
  
|||  
|-|-|  
|[sp_syspolicy_add_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-transact-sql.md)|[sp_syspolicy_rename_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-category-transact-sql.md)|  
|[sp_syspolicy_add_policy_category_subscription](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)|[sp_syspolicy_repair_policy_automation](../../relational-databases/system-stored-procedures/sp-syspolicy-repair-policy-automation-transact-sql.md)|  
|[sp_syspolicy_configure](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md)|[sp_syspolicy_set_config_enabled](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)|  
|[sp_syspolicy_delete_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-transact-sql.md)|[sp_syspolicy_set_config_history_retention](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)|  
|[sp_syspolicy_delete_policy_category_subscription](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-category-subscription-transact-sql.md)|[sp_syspolicy_set_log_on_success](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)|  
|[sp_syspolicy_delete_policy_execution_history](../../relational-databases/system-stored-procedures/sp-syspolicy-delete-policy-execution-history-transact-sql.md)|[sp_syspolicy_subscribe_to_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-subscribe-to-policy-category-transact-sql.md)|  
|[sp_syspolicy_purge_health_state](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-health-state-transact-sql.md)|[sp_syspolicy_unsubscribe_from_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-unsubscribe-from-policy-category-transact-sql.md)|  
|[sp_syspolicy_purge_history](../../relational-databases/system-stored-procedures/sp-syspolicy-purge-history-transact-sql.md)|[sp_syspolicy_update_policy_category](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)|  
|[sp_syspolicy_rename_condition](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-condition-transact-sql.md)|[sp_syspolicy_update_policy_category_subscription](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-subscription-transact-sql.md)|  
|[sp_syspolicy_rename_policy](../../relational-databases/system-stored-procedures/sp-syspolicy-rename-policy-transact-sql.md)||  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
