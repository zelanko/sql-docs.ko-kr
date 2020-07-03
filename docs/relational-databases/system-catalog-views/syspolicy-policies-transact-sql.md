---
title: syspolicy_policies (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 49ef90e030c2899e49adcb69e8765a57f623ace7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900588"
---
# <a name="syspolicy_policies-transact-sql"></a>syspolicy_policies(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 정책 기반 관리 정책에 대해 하나의 행을 표시합니다. syspolicy_policies는 msdb 데이터베이스의 dbo 스키마에 속합니다. 다음 표에서는 syspolicy_policies 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|정책의 ID입니다.|  
|name|**sysname**|정책의 이름입니다.|  
|condition_id|**int**|이 정책에 의해 적용되거나 테스트되는 조건의 ID입니다.|  
|root_condition_id|**int**|내부 전용입니다.|  
|date_created|**datetime**|정책을 만든 날짜와 시간입니다.|  
|execution_mode|**int**|정책에 대한 평가 모드입니다. 가능한 값은 다음과 같습니다.<br /><br /> 0 = 요청 시<br /><br /> 이 모드는 사용자가 직접 지정한 경우 정책을 평가합니다.<br /><br /> 1 = 변경 시: 방지<br /><br /> 이 자동화된 모드에서는 DDL 트리거를 사용하여 정책 위반을 방지합니다.<br /><br /> 2 = 변경 시: 로그만<br /><br /> 이 자동화된 모드에서는 이벤트 알림을 사용하여 관련된 변경이 발생할 때 정책을 평가하고 정책 위반을 기록합니다.<br /><br /> 4 = 예약 시<br /><br /> 이 자동화된 모드에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 사용하여 주기적으로 정책을 평가합니다. 이 모드는 정책 위반을 기록합니다.<br /><br /> 참고: 값 3은 사용할 수 없는 값입니다.|  
|policy_category|**int**|이 정책이 속한 정책 기반 관리 정책 범주의 ID입니다. 기본 정책 그룹의 경우 NULL입니다.|  
|schedule_uid|**uniqueidentifier**|execution_mode가 예약 시로 설정된 경우 일정의 ID를 포함하고, 그렇지 않으면 NULL입니다.|  
|description|**nvarchar(max)**|정책에 대한 설명입니다. description 열은 선택 사항이며 NULL일 수 있습니다.|  
|help_text|**nvarchar(4000)**|help_link에 속한 하이퍼링크 텍스트입니다.|  
|help_link|**nvarchar (2083)**|정책을 만든 사람이 정책에 할당한 추가 도움말 하이퍼링크입니다.|  
|object_set_id|**int**|정책을 평가하는 개체 집합의 ID입니다.|  
|is_enabled|**bit**|정책이 현재 사용되는지(1) 사용되지 않는지(0)를 나타냅니다.|  
|job_id|**uniqueidentifier**|execution_mode가 예약 시로 설정된 경우 정책을 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 ID를 포함합니다.|  
|created_by|**sysname**|정책을 만든 로그인입니다.|  
|modified_by|**sysname**|정책을 가장 최근에 수정한 로그인입니다. 수정한 적이 없으면 NULL입니다.|  
|date_modified|**datetime**|정책을 만든 날짜와 시간입니다. 수정한 적이 없으면 NULL입니다.|  
  
## <a name="remarks"></a>설명  
 정책 기반 관리의 문제를 해결 하는 경우 [syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md) 보기를 쿼리하여 정책이 사용 되는지 여부를 확인 합니다. 이 뷰는 정책을 만든 사용자 또는 마지막으로 변경한 사용자도 표시합니다.  
  
## <a name="permissions"></a>사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용 하 여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
