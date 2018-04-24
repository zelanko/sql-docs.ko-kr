---
title: ALTER DATABASE AUDIT SPECIFICATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5ca329329e12aead0f41c59e96c31067e3c44c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 기능을 사용하여 데이터베이스 감사 사양 개체를 변경합니다. 자세한 내용은 [SQL Server Audit&#40;데이터베이스 엔진&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
  
```  
  
## <a name="arguments"></a>인수  
 *audit_specification_name*  
 감사 사양의 이름입니다.  
  
 *audit_name*  
 이 사양이 적용되는 감사의 이름입니다.  
  
 *audit_action_specification*  
 하나 이상의 데이터베이스 수준 감사 가능 동작의 이름입니다. 감사 동작 그룹의 목록에 대해서는 [SQL Server 감사 동작 그룹 및 동작](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)을 참조합니다.  
  
 *audit_action_group_name*  
 하나 이상의 데이터베이스 수준 감사 가능 동작 그룹의 이름입니다. 감사 동작 그룹의 목록에 대해서는 [SQL Server 감사 동작 그룹 및 동작](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)을 참조합니다.  
  
 *class*  
 보안 개체의 클래스 이름(해당 사항이 있을 경우)입니다.  
  
 *securable*  
 감사 동작 또는 감사 동작 그룹을 적용할 데이터베이스의 테이블, 뷰 또는 기타 보안 개체입니다. 자세한 내용은 [Securables](../../relational-databases/security/securables.md)을 참조하세요.  
  
 *column*  
 보안 개체의 열 이름(해당 사항이 있을 경우)입니다.  
  
 *principal*  
 감사 동작 또는 감사 동작 그룹을 적용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 주체의 이름입니다. 자세한 내용은 [보안 주체 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)를 참조하세요.  
  
 WITH **(** STATE **=** { ON | OFF } **)**  
 감사에서 이 감사 사양에 대한 레코드를 수집하거나 수집하지 못하도록 설정합니다. 감사 사양 상태 변경은 사용자 트랜잭션 외부에서 수행해야 하며 ON에서 OFF로 전환되는 경우 동일한 문에 다른 변경 사항이 있어서는 안 됩니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 감사 사양은 지정된 데이터베이스에 있는 비보안 개체입니다. 데이터베이스 감사 사양을 변경하려면 감사 사양의 상태를 OFF 옵션으로 설정해야 합니다. 감사 사양에 STATE=OFF 외의 옵션이 설정되었을 때 이 ALTER DATABASE AUDIT SPECIFICATION 실행되면 오류 메시지가 표시됩니다. 자세한 내용은 [tempdb Database](../../relational-databases/databases/tempdb-database.md)을(를) 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY DATABASE AUDIT 권한이 있는 사용자는 데이터베이스 감사 사양을 변경하여 모든 감사에 바인딩할 수 있습니다.  
  
 만들어진 데이터베이스 감사 사양은 CONTROL SERVER, ALTER ANY DATABASE AUDIT 권한이 있는 보안 주체, sysadmin 계정 또는 해당 감사에 대한 명시적 액세스 권한이 있는 보안 주체가 볼 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `HIPPA_Audit_DB_Specification`라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit에 대해 `SELECT` 사용자의 `dbo` 문을 감사하는 `HIPPA_Audit`이라는 데이터베이스 감사 사양을 변경합니다.  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 감사를 만드는 방법에 대한 전체 예에 대해서는 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [서버 감사 및 서버 감사 사양 만들기](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
