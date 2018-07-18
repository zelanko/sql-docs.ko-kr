---
title: sys.security_predicates (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 539ca48e5c55485a5a4b3fdecb3044c1feae6826
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993855"
---
# <a name="syssecuritypredicates-transact-sql"></a>sys.security_predicates (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스의 각 보안 조건자에 대 한 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 조건자를 포함하는 보안 정책의 ID입니다.|  
|security_predicate_id|**int**|이 보안 정책 내의 조건자 ID입니다.|  
|target_object_id|**int**|보안 조건자가 바인딩되는 개체의 ID입니다.|  
|predicate_definition|**nvarchar(max)**|인수를 포함하여 보안 조건자로 사용될 함수의 정규화된 이름입니다. `schema.function` 이름도 정규화 (즉, 이스케이프) 일관성을 위해 텍스트에 있는 다른 요소 뿐만 아니라 합니다. 예를 들어:<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|유형 보안 정책에 의해 사용 되는 조건자입니다.<br /><br /> 0 = 필터 조건자<br /><br /> 1 = 차단 조건자|  
|predicate_type_desc|**nvarchar(60)**|유형 보안 정책에 의해 사용 되는 조건자입니다.<br /><br /> FILTER<br /><br /> 블록|  
|operation(작업)|**int**|지정한 조건자에 대 한 작업의 유형:<br /><br /> NULL = 모든 적용 가능한 작업<br /><br /> 1 = 삽입 후<br /><br /> 2 = 업데이트 후<br /><br /> 3 = 업데이트 하기 전에<br /><br /> 4 = 삭제 하기 전에|  
|operation_desc|**nvarchar(60)**|지정한 조건자에 대 한 작업의 유형:<br /><br /> NULL<br /><br /> 삽입 후<br /><br /> AFTER UPDATE<br /><br /> 업데이트 하기 전에<br /><br /> 삭제 전|  
  
## <a name="permissions"></a>사용 권한  
 사용 하 여 보안 주체를 **ALTER ANY SECURITY POLICY** 이 카탈로그 뷰에 뿐만 아니라 사용 하 여 사용자의 모든 개체에 액세스할 권한이 **VIEW DEFINITION** 개체에서.  
  
## <a name="see-also"></a>관련 항목  
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
