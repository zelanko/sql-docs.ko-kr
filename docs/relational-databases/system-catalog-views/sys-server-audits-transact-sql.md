---
title: sys. server_audits (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a00f6843a0ef379c12aa1d1d00df9380efbd139
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124998"
---
# <a name="sysserver_audits-transact-sql"></a>sys.server_audits(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 인스턴스에 있는 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit에 대해 하나의 행을 포함합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|감사의 ID입니다.|  
|**name**|**sysname**|감사의 이름입니다.|  
|**audit_guid**|**uniqueidentifier**|서버 시작 및 데이터베이스 연결 작업 중에 멤버 서버&#124;데이터베이스 감사 사양을 사용 하 여 감사를 열거 하는 데 사용 되는 감사에 대 한 GUID입니다.|  
|**create_date**|**datetime**|감사를 만든 UTC 날짜입니다.|  
|**modify_date**|**datetime**|감사를 마지막으로 수정한 UTC 날짜입니다.|  
|**principal_id**|**int**|서버에 등록된 감사 소유자의 ID입니다.|  
|**type**|**char(2)**|감사 유형:<br /><br /> SL-NT 보안 이벤트 로그<br /><br /> AL-NT 응용 프로그램 이벤트 로그<br /><br /> FL-파일 시스템의 파일|  
|**type_desc**|**nvarchar(60)**|SECURITY LOG<br /><br /> APPICATION LOG<br /><br /> FILE|  
|**on_failure**|**tinyint**|동작 항목을 쓰지 못한 경우:<br /><br /> 0-계속<br /><br /> 1-서버 인스턴스 종료<br /><br /> 2-작업 실패|  
|**on_failure_desc**|**nvarchar(60)**|동작 항목을 쓰지 못한 경우:<br /><br /> CONTINUE<br /><br /> SHUTDOWN SERVER INSTANCE<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0-사용 안 함<br /><br /> 1 - 사용|  
|**queue_delay**|**int**|디스크에 쓸 때까지 대기할 최대 시간(밀리초)입니다. 0인 경우 이벤트가 계속될 수 있도록 감사에 의해 쓰기가 보장됩니다.|  
|**가**|**nvarchar (3000)**|이벤트에 적용되는 조건자 식입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **ALTER ANY SERVER AUDIT** 또는 **VIEW any DEFINITION** 권한이 있는 보안 주체가이 카탈로그 뷰에 액세스할 수 있습니다. 또한 보안 주체는 **VIEW ANY DEFINITION** 권한을 거부 해서는 안 됩니다.  
  
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
 [server_file_audits &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [server_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [server_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [database_audit_specifications &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [database_audit_specification_details &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [dm_server_audit_status &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [dm_audit_actions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [dm_audit_class_type_map &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
