---
description: sys. security_predicates (Transact-sql)
title: sys. security_predicates (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c2ba8b6c9c4a2fc2f6b3beb562edfac0728678fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490140"
---
# <a name="syssecurity_predicates-transact-sql"></a>sys. security_predicates (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  데이터베이스의 각 보안 조건자에 대해 하나의 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|이 조건자를 포함하는 보안 정책의 ID입니다.|  
|security_predicate_id|**int**|이 보안 정책 내의 조건자 ID입니다.|  
|target_object_id|**int**|보안 조건자가 바인딩되는 개체의 ID입니다.|  
|predicate_definition|**nvarchar(max)**|인수를 포함하여 보안 조건자로 사용될 함수의 정규화된 이름입니다. 일관성을 위해 텍스트에 있는 다른 요소뿐만 아니라 `schema.function` 이름도 정규화(즉, 이스케이프)할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|보안 정책에서 사용 하는 조건자의 유형입니다.<br /><br /> 0 = 필터 조건자<br /><br /> 1 = 차단 조건자|  
|predicate_type_desc|**nvarchar(60)**|보안 정책에서 사용 하는 조건자의 유형입니다.<br /><br /> FILTER<br /><br /> 차단|  
|operation|**int**|조건자에 대해 지정 된 작업의 유형입니다.<br /><br /> NULL = 적용 가능한 모든 작업<br /><br /> 1 = 삽입 후<br /><br /> 2 = 업데이트 후<br /><br /> 3 = 업데이트 전<br /><br /> 4 = 삭제 전|  
|operation_desc|**nvarchar(60)**|조건자에 대해 지정 된 작업의 유형입니다.<br /><br /> NULL<br /><br /> 삽입 후<br /><br /> AFTER UPDATE<br /><br /> 업데이트 전<br /><br /> 삭제 전|  
  
## <a name="permissions"></a>사용 권한  
 **ALTER ANY SECURITY POLICY** 권한이 있는 보안 주체는이 카탈로그 뷰의 모든 개체 뿐만 아니라 개체에 대 한 **뷰 정의가** 있는 모든 사용자에 게 액세스할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
