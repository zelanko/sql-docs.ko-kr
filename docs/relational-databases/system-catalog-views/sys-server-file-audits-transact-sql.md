---
title: sys.server_file_audits (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_file_audits_TSQL
- sys.server_file_audits_TSQL
- sys.server_file_audits
- server_file_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_file_audits catalog view
ms.assetid: 553288a0-be57-4d79-ae53-b7cbd065e127
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f4e10ec5dc755f1a8487aecd40b620eb0a3eefe8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysserverfileaudits-transact-sql"></a>sys.server_file_audits(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  파일 감사 유형에 대 한 확장된 정보를 포함 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 인스턴스에서 감사 합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|audit_id|**int**|감사의 ID입니다.|  
|name|**sysname**|감사의 이름입니다.|  
|audit_guid|**uniqueidentifier**|감사의 GUID입니다.|  
|create_date|**datetime**|파일 감사를 만든 UTC 날짜입니다.|  
|modify_date|**datatime**|파일 감사를 마지막으로 수정한 UTC 날짜입니다.|  
|principal_id|**int**|서버에 등록된 감사 소유자의 ID입니다.|  
|유형|**char(2)**|감사 유형:<br /><br /> 0 = NT 보안 이벤트 로그<br /><br /> 1 = NT 응용 프로그램 이벤트 로그<br /><br /> 2 = 파일 시스템의 파일|  
|type_desc|**nvarchar(60)**|감사 유형 설명입니다.|  
|on_failure|**tinyint**|조건이 실패한 경우:<br /><br /> 0 = 계속<br /><br /> 1 = 서버 인스턴스 종료<br /><br /> 2 = 작업 실패|  
|on_failure_desc|**nvarchar(60)**|동작 항목을 쓰지 못한 경우:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL OPERATION|  
|is_state_enabled|**tinyint**|0 = 사용 안 함<br /><br /> 1 = 사용|  
|queue_delay|**int**|디스크에 쓸 때까지 대기할 최대 제안 시간(밀리초)입니다. 0인 경우 이벤트가 계속될 수 있도록 감사에 의해 쓰기가 보장됩니다.|  
|predicate|**nvarchar(8000)**|이벤트에 적용되는 조건자 식입니다.|  
|max_file_size|**bigint**|감사의 최대 크기(MB):<br /><br /> 0 = 무제한/선택한 감사 유형에 적용할 수 없음|  
|max_rollover_files|**int**|롤오버 옵션과 함께 사용할 최대 파일 수입니다.|  
|max_files|**int**|롤오버 옵션 없이 사용할 최대 파일 수입니다.|  
|reserved_disk_space|**int**|파일당 예약할 디스크 공간의 양입니다.|  
|log_file_path|**nvarchar(260)**|감사가 있는 경로입니다. 파일 감사의 경우 파일 경로이고 응용 프로그램 로그 감사의 경우 응용 프로그램 로그 경로입니다.|  
|log_file_name|**nvarchar(260)**|CREATE AUDIT DDL에서 제공하는 로그 파일의 기본 이름입니다. base_log_name 파일에 증분값을 접미사로 추가하여 로그 파일 이름을 만듭니다.|  
  
## <a name="permissions"></a>Permissions  
 있는 보안 주체는 **ALTER ANY SERVER AUDIT** 또는 **VIEW ANY DEFINITION** 권한이 카탈로그 뷰에 액세스할 수 있어야 합니다. 또한 보안 주체가 거부 되지 않아야 **VIEW ANY DEFINITION** 권한.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
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
 [sys.server_file_audits (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
