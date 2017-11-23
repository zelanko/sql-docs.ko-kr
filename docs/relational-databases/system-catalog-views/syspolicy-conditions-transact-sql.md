---
title: syspolicy_conditions (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs: TSQL
helpviewer_keywords: syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0628b0913358fd5fb80f3c36fbcf8e5a5c05170
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syspolicyconditions-transact-sql"></a>syspolicy_conditions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 각 정책 기반 관리 조건에 대해 한 행을 표시합니다. syspolicy_ conditions는 msdb 데이터베이스의 dbo 스키마에 속합니다. 다음 표에서는 syspolicy_conditions 뷰의 열을 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|이 조건의 ID입니다. 각 조건은 하나 이상의 조건 식의 컬렉션을 나타냅니다.|  
|name|**sysname**|조건의 이름입니다.|  
|date_created|**datetime**|조건을 만든 날짜와 시간입니다.|  
|description|**nvarchar(max)**|조건에 대한 설명입니다. description 열은 선택 사항이며 NULL일 수 있습니다.|  
|created_by|**sysname**|조건을 만든 로그인입니다.|  
|modified_by|**sysname**|조건을 최근에 수정한 로그인입니다. 수정한 적이 없으면 NULL입니다.|  
|date_modified|**datetime**|조건을 만든 날짜와 시간입니다. 수정한 적이 없으면 NULL입니다.|  
|is_name_condition|**smallint**|조건이 명명 조건인지를 지정합니다.<br /><br /> 0 = 조건 식에 @Name 변수를 포함하지 않습니다.<br /><br /> 1 = 조건 식에 @Name 변수를 포함합니다.|  
|패싯(facet)|**nvarchar(max)**|조건이 기반으로 하는 패싯의 이름입니다.|  
|식|**nvarchar(max)**|패싯 상태의 식입니다.|  
|obj_name|**sysname**|조건 식에서 @Name 변수를 포함하는 경우 이 변수에 할당된 개체 이름입니다.|  
  
## <a name="remarks"></a>주의  
 정책 기반 관리의 문제를 해결 중인 경우 syspolicy_conditions 뷰를 쿼리하여 조건을 만들거나 마지막으로 변경한 사람을 확인합니다.  
  
## <a name="permissions"></a>Permissions  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
