---
title: sys.security_policies (TRANSACT-SQL) | Microsoft Docs
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
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 47c2f4bd8dd55693f42f9a014c8074e4982d23f3
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079216"
---
# <a name="syssecuritypolicies-transact-sql"></a>sys.security_policies (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스의 각 보안 정책에 대 한 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|데이터베이스 내에서 고유한 보안 정책의 이름입니다.|  
|object_id|**int**|보안 정책의 ID입니다.|  
|principal_id|**int**|데이터베이스에 등록된 보안 정책 소유자의 ID입니다. 소유자가 스키마를 통해 결정되는 경우 NULL입니다.|  
|schema_id|**int**|개체가 상주하는 스키마의 ID입니다.|  
|parent_object_id|**int**|정책이 속하는 개체의 ID입니다. 0이어야 합니다.|  
|유형|**vachar(2)**|여야 **SP**합니다.|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**합니다.|  
|create_date|**datetime**|보안 정책이 만들어진 UTC 날짜입니다.|  
|modify_date|**datetime**|보안 정책이 마지막으로 수정된 UTC 날짜입니다.|  
|is_ms_shipped|**bit**|항상 false입니다.|  
|is_enabled|**bit**|보안 정책 사양 상태:<br /><br /> 0 = 사용 안 함<br /><br /> 1 = 사용|  
|is_not_for_replication|**bit**|정책이 NOT FOR REPLICATION 옵션으로 생성되었습니다.|  
|uses_database_collation|**bit**|동일한 데이터 정렬을 데이터베이스로 사용합니다.|  
|is_schemabinding_enabled|**bit**|보안 정책에 대 한 Schemabinding 상태:<br /><br /> 0 또는 NULL = 사용<br /><br /> 1 = 사용 안 함|  
  
## <a name="permissions"></a>사용 권한  
 사용 하 여 보안 주체를 **ALTER ANY SECURITY POLICY** 이 카탈로그 뷰에 뿐만 아니라 사용 하 여 사용자의 모든 개체에 액세스할 권한이 **VIEW DEFINITION** 개체에서.  
  
## <a name="see-also"></a>관련 항목  
 [행 수준 보안](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
