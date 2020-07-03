---
title: sys. dm_server_audit_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_audit_status_TSQL
- sys.dm_server_audit_status
- dm_server_audit_status
- sys.dm_server_audit_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_audit_status dynamic management view
ms.assetid: 4aa32d54-2ae1-437e-bbaa-7f1df1404b44
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 982ebf62124a392c98ea2357e112cdb8bb56d45b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898675"
---
# <a name="sysdm_server_audit_status-transact-sql"></a>sys.dm_server_audit_status(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  감사의 현재 상태를 나타내는 각 서버 감사의 행을 반환합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|감사의 ID입니다. 는 **sys. 감사** 카탈로그 뷰의 **audit_id** 필드에 매핑됩니다.|  
|**name**|**sysname**|감사의 이름입니다. **Server_audits** 카탈로그 뷰의 **이름** 필드와 동일 합니다.|  
|**status**|**smallint**|서버 감사의 숫자 상태입니다.<br /><br /> 0 = 시작 되지 않음<br /><br /> 1 =<br />        시작됨<br /><br /> 2 =<br />      런타임 실패<br /><br /> 3 = 대상 만들기 실패<br /><br /> 4 = 종료 중|  
|**status_desc**|**nvarchar(256)**|서버 감사의 상태를 보여 주는 문자열입니다.<br /><br /> NOT_STARTED<br /><br /> STARTED<br /><br /> RUNTIME_FAIL<br /><br /> TARGET_CREATION_FAILED<br /><br /> SHUTTING_DOWN|  
|**status_time**|**datetime2**|감사의 마지막 상태 변경에 대한 UTC의 타임스탬프입니다.|  
|**event_session_address**|**varbinary(8)**|감사와 연결된 확장 이벤트 세션의 주소입니다. **Dm_xe_sessions. 주소** 카탈로그 뷰와 관련 됩니다.|  
|**audit_file_path**|**nvarchar(256)**|현재 사용되고 있는 감사 파일 대상의 전체 경로 및 파일 이름입니다. 파일 감사에 대해서만 채워집니다.|  
|**audit_file_size**|**bigint**|감사 파일의 대략적인 크기(바이트)입니다. 파일 감사에 대해서만 채워집니다.|  
  
## <a name="permissions"></a>사용 권한  
 보안 주체에 **VIEW SERVER STATE** 및 **SELECT** 권한이 있어야 합니다.  
  
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
 [database_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys. dm_server_audit_status](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [dm_audit_actions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [dm_audit_class_type_map &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
