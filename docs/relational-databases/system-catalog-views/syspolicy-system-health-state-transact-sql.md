---
title: syspolicy_system_health_state (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_system_health_state_TSQL
- syspolicy_system_health_state
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_system_health_state view
ms.assetid: 00815106-9fe4-481d-a9e1-a256101887f4
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97759823fe4b4979da359f3ef0497466424c068b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syspolicysystemhealthstate-transact-sql"></a>syspolicy_system_health_state(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 정책 기반 관리 정책과 대상 쿼리 식 조합에 대해 하나의 행을 표시합니다. syspolicy_system_health_state 뷰를 사용하여 서버의 정책 상태를 프로그래밍 방식으로 확인할 수 있습니다. 다음 표에서는 syspolicy_system_health_state 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|health_state_id|**bigint**|정책 상태 레코드의 ID입니다.|  
|policy_id|**int**|정책의 ID입니다.|  
|last_run_date|**datetime**|정책이 마지막으로 실행된 날짜와 시간입니다.|  
|target_query_expression_with_id|**nvarchar(400)**|정책을 준수하는지 평가하는 대상을 정의하는 대상 식으로 변수를 식별하는 값이 할당되어 있습니다.|  
|target_query_expression|**nvarchar(max)**|정책을 준수하는지 평가하는 대상을 정의하는 식입니다.|  
|result|**bit**|이 대상의 정책 관련 상태입니다.<br /><br /> 0 = 실패<br /><br /> 1 = 성공|  
  
## <a name="remarks"></a>주의  
 syspolicy_system_health_state 뷰는 사용 가능한 각 활성 정책과 관련된 대상 쿼리 식의 최근 상태를 표시합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기 및 개체 탐색기 정보 페이지는 이 뷰에서 정책 상태를 집계하여 중요한 상태를 표시합니다.  
  
## <a name="permissions"></a>Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
