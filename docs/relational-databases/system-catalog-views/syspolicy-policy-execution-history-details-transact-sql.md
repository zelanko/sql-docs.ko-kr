---
title: syspolicy_policy_execution_history_details (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_details
- syspolicy_policy_execution_history_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history_details view
ms.assetid: 97ef6573-5e8b-4ba5-8ae0-7901e79a9683
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b761d0e056037c134a3be837be04cba9395d9273
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900035"
---
# <a name="syspolicy_policy_execution_history_details-transact-sql"></a>syspolicy_policy_execution_history_details(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  실행한 조건 식, 식 대상, 각 실행 결과, 오류(발생한 경우)에 대한 정보를 표시합니다. 다음 표에서는 syspolicy_execution_history_details 뷰의 열에 대해 설명합니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|detail_id|**bigint**|이 레코드의 ID입니다. 각 레코드는 정책에 있는 하나의 조건 식을 평가하거나 적용하는 시도를 나타냅니다. 조건이 여러 대상에 적용되는 경우 각 조건에는 각 대상에 대한 세부 레코드가 포함됩니다.|  
|history_id|**bigint**|기록 이벤트의 식별자입니다. 각 기록 이벤트는 정책을 실행하는 한 번의 시도를 나타냅니다. 조건에 여러 조건 식과 여러 대상이 있을 수 있으므로 history_id에서 여러 세부 레코드를 만들 수 있습니다. History_id 열을 사용 하 여이 뷰를 [syspolicy_policy_execution_history](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-transact-sql.md) 뷰에 조인 합니다.|  
|target_query_expression|**nvarchar(max)**|정책 및 syspolicy_policy_execution_history 뷰의 대상입니다.|  
|execution_date|**datetime**|세부 레코드가 생성된 날짜 및 시간입니다.|  
|result|**bit**|이 대상 및 조건 식 평가의 성공 또는 실패입니다.<br /><br /> 0(성공) 또는 1(실패).|  
|result_detail|**nvarchar(max)**|결과 메시지입니다. 패싯에서 제공한 경우에만 사용할 수 있습니다.|  
|exception_message|**nvarchar(max)**|예외가 발생한 경우 예외에서 생성한 메시지입니다.|  
|exception|**nvarchar(max)**|예외가 발생한 경우 예외에 대한 설명입니다.|  
  
## <a name="remarks"></a>설명  
 정책 기반 관리의 문제를 해결하는 경우 syspolicy_policy_execution_history_details 뷰를 쿼리하여 어떤 대상 및 조건 식 조합이 실패했는지와 해당 조합이 실패한 경우를 확인하고 관련 오류를 검토합니다.  
  
 다음 쿼리는 `syspolicy_policy_execution_history_details` 뷰와 `syspolicy_policy_execution_history_details` 및 `syspolicy_policies` 뷰를 조합하여 정책 이름, 조건 이름 및 오류 정보를 표시합니다.  
  
```  
SELECT Pol.name AS Policy,   
Cond.name AS Condition,   
PolHistDet.target_query_expression,   
PolHistDet.execution_date,   
PolHistDet.result,   
PolHistDet.result_detail,   
PolHistDet.exception_message,   
PolHistDet.exception   
FROM msdb.dbo.syspolicy_policies AS Pol  
JOIN msdb.dbo.syspolicy_conditions AS Cond  
    ON Pol.condition_id = Cond.condition_id  
JOIN msdb.dbo.syspolicy_policy_execution_history AS PolHist  
    ON Pol.policy_id = PolHist.policy_id  
JOIN msdb.dbo.syspolicy_policy_execution_history_details AS PolHistDet  
    ON PolHist.history_id = PolHistDet.history_id  
WHERE PolHistDet.result = 0 ;  
```  
  
## <a name="permissions"></a>사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용 하 여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
