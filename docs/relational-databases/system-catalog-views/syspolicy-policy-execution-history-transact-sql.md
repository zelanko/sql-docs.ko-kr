---
title: syspolicy_policy_execution_history (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_TSQL
- syspolicy_policy_execution_history
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history view
ms.assetid: b13c44a7-6d49-4d50-abe1-e657fc52bb05
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ed3bca383e5f6ad1960274145327f915c6e8ca5c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85663769"
---
# <a name="syspolicy_policy_execution_history-transact-sql"></a>syspolicy_policy_execution_history(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  정책이 실행된 시간, 각 실행의 결과 및 오류가 있는 경우 오류에 대한 자세한 내용을 표시합니다. 다음 표에서는 syspolicy_policy_execution_history 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|history_id|**bigint**|이 레코드의 ID입니다. 각 레코드는 정책과 시작된 시간을 하나씩 나타냅니다.|  
|policy_id|**int**|정책의 ID입니다.|  
|start_date|**datetime**|이 정책을 실행하려고 시도한 날짜와 시간입니다.|  
|end_date|**datetime**|이 정책이 실행을 마친 시간입니다.|  
|result|**bit**|정책의 성공 또는 실패를 나타냅니다. 0 = 실패, 1 = 성공입니다.|  
|exception_message|**nvarchar(max)**|예외가 발생한 경우 예외에서 생성한 메시지입니다.|  
|exception|**nvarchar(max)**|예외가 발생한 경우 예외에 대한 설명입니다.|  
  
## <a name="remarks"></a>설명  
 [Syspolicy_policy_execution_history_details](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-details-transact-sql.md) 뷰에는 정책 대상 및 테스트 된 조건 식에 대 한 관련 정보가 포함 되어 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용 하 여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
