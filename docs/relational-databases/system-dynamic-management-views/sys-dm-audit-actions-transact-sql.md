---
title: sys. dm_audit_actions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1532cc75fdcfa10e92c8fa000ab069f3bc679b2
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394851"
---
# <a name="sysdm_audit_actions-transact-sql"></a>sys.dm_audit_actions(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  감사 로그에 보고할 수 있는 모든 감사 동작 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit의 일부로 구성할 수 있는 모든 감사 동작 그룹에 대한 행을 반환합니다. 감사에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 감사 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)를 참조 하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar(4)**|감사 동작의 ID입니다. 각 감사 레코드에 기록 된 **action_id** 값과 관련 됩니다. Null을 허용합니다. 감사 그룹의 경우 NULL입니다.|  
|**action_in_log**|**bit**|동작을 감사 로그에 기록할 수 있는지 여부를 나타냅니다. 값은 다음과 같습니다.<br /><br /> 1 = 예<br /><br /> 0 = 아니요|  
|**name**|**sysname**|감사 동작 또는 동작 그룹의 이름입니다. Null을 허용하지 않습니다.|  
|**class_desc**|**nvarchar(120)**|감사 동작이 적용되는 개체 클래스의 이름입니다. 서버, 데이터베이스 또는 스키마 범위 개체 중 하나일 수 있지만 스키마 개체를 포함하지 않습니다. Null을 허용하지 않습니다.|  
|**parent_class_desc**|**nvarchar(120)**|class_desc에서 설명하는 개체의 부모 클래스 이름입니다. class_desc가 서버인 경우 NULL입니다.|  
|**covering_parent_action_name**|**nvarchar(120)**|이 행에 설명된 감사 동작을 포함하는 감사 동작 또는 감사 그룹의 이름입니다. 동작 계층 및 포함 동작을 만드는 데 사용됩니다. Null을 허용합니다.|  
|**configuration_level**|**nvarchar (10)**|이 행에 지정된 동작 또는 동작 그룹을 그룹 또는 동작 수준에서 구성할 수 있음을 나타냅니다. 동작을 구성할 수 없는 경우 NULL입니다.|  
|**containing_group_name**|**nvarchar(120)**|지정된 동작이 포함된 감사 그룹의 이름입니다. 이름의 값이 그룹인 경우 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 보안 주체에 **SELECT** 권한이 있어야 합니다. 기본적으로 이 권한은 Public에 부여됩니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 감사 &#40;Transact-sql&#41;만들기](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
