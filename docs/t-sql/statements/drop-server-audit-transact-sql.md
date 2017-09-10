---
title: DROP SERVER AUDIT (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SERVER AUDIT
- DROP_SERVER_AUDIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SERVER AUDIT statement
ms.assetid: faace8a3-daa9-4208-a2cd-4249eb32175c
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 83d383f58c4ebf5bcc7492057b142d4db311992e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-server-audit--transact-sql"></a>DROP SERVER AUDIT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server Audit 기능을 사용하여 서버 감사 개체를 삭제합니다. SQL Server Audit에 대 한 자세한 내용은 참조 하십시오. [SQL Server audit&#40; 데이터베이스 엔진 &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP SERVER AUDIT audit_name  
    [ ; ]  
```  
  
## <a name="remarks"></a>주의  
 감사를 변경하려면 감사 상태를 OFF 옵션으로 설정해야 합니다. 감사가 STATE=OFF 외의 옵션으로 설정되었을 때 DROP AUDIT를 실행하면 MSG_NEED_AUDIT_DISABLED 오류 메시지가 표시됩니다.  
  
 DROP SERVER AUDIT는 명령이 실행되기 전에 수집된 감사 데이터를 제외한 감사의 메타데이터를 제거합니다.  
  
 DROP SERVER AUDIT는 연결된 서버 또는 데이터베이스 감사 사양을 삭제하지 않습니다. 이러한 사양은 수동으로 삭제하거나 분리하여 나중에 새 서버 감사에 매핑해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 서버 감사 보안 주체를 생성, 변경 또는 삭제하려면 ALTER ANY SERVER AUDIT 또는 CONTROL SERVER 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HIPAA_Audit`라는 감사를 삭제합니다.  
  
```  
ALTER SERVER AUDIT HIPAA_Audit  
STATE = OFF;  
GO  
DROP SERVER AUDIT HIPAA_Audit;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [서버 감사 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER audit&#40; Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [SERVER AUDIT specification&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [DATABASE AUDIT specification&#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT specification&#40; Transact SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER authorization&#40; Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file&#40; Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map&#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
