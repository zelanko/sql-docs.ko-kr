---
title: sys. database_audit_specification_details (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_audit_specification_details
- sys.database_audit_specification_details_TSQL
- sys.database_audit_specification_details
- database_audit_specification_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_audit_specification_details catalog view
ms.assetid: 03fc60a9-1696-4109-b15e-a50046310859
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3a691e994c4c8389847c86bcba2283f5ef72decc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896055"
---
# <a name="sysdatabase_audit_specification_details-transact-sql"></a>sys.database_audit_specification_details(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  서버 인스턴스에 있는 모든 데이터베이스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit의 데이터베이스 감사 사양 정보를 포함합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요. 모든 audit_action_id 및 해당 이름 목록을 보려면 [transact-sql&#41;&#40;dm_audit_actions ](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)를 쿼리 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_specification_id**|**int**|감사 사양의 ID입니다.|  
|**audit_action_id**|**int**|감사 동작의 ID입니다.|  
|**audit_action_name**|**Sysname 이며**|감사 동작 또는 감사 동작 그룹의 이름입니다.|  
|**클래스**|**int**|감사 중인 개체의 클래스를 식별합니다.|  
|**class_ desc**|**Nvarchar (60)**|감사 중인 개체의 클래스에 대한 설명:<br /><br /> - SCHEMA<br /><br /> - TABLE|  
|**major_id**|**int**|Table Audit 동작의 Table ID와 같이 감사 중인 개체의 주 ID입니다.|  
|**minor_id**|**정수**|Table Audit 동작의 열 ID와 같이 클래스에 따라 해석되어 감사 중인 개체의 보조 ID입니다.|  
|**audited_principal_id**|**int**|감사 중인 보안 주체입니다.|  
|**audited_result**|**Nvarchar (60)**|감사 동작 결과:<br /><br /> - SUCCESS AND FAILURE - SUCCESS<br /><br /> - FAILURE|  
|**is_group**|**조금**|다음은 개체가 그룹인지 여부를 보여 줍니다.<br /><br /> 0 - 그룹 아님<br /><br /> 1 - 그룹임|  
  
## <a name="permissions"></a>사용 권한  
 **ALTER ANY DATABASE AUDIT** 또는 **VIEW DEFINITION** 권한이 있는 보안 주체, **dbo** 역할 및 **db_owners** 고정 데이터베이스 역할의 멤버는이 카탈로그 뷰에 액세스할 수 있습니다. 또한 보안 주체에 게 **VIEW DEFINITION** 권한이 거부 되지 않아야 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 감사 &#40;Transact-sql&#41;만들기](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-sql&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-sql&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [Transact-sql&#41;&#40;서버 감사 사양 만들기](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [Transact-sql&#41;&#40;데이터베이스 감사 사양 만들기](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-sql&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-sql&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [fn_get_audit_file &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [server_audits &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [server_file_audits &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [server_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [database_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [dm_server_audit_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [dm_audit_actions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [dm_audit_class_type_map &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
