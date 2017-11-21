---
title: ALTER USER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
caps.latest.revision: 75
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62651475119ba147e6823ba9e25b2cde67678dcc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-user-transact-sql"></a>ALTER USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 사용자의 이름을 바꾸거나 기본 스키마를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,… n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *사용자 이름*  
 이 데이터베이스 내에서 사용자를 식별하는 이름을 지정합니다.  
  
 로그인  **=**  *loginName*  
 사용자의 SID(보안 식별자)를 다른 로그인의 SID와 일치하도록 변경하여 사용자를 다른 로그인으로 다시 매핑합니다.  
  
 ALTER USER 문이 SQL 일괄 처리의 유일한 문인 경우 Microsoft Azure SQL Database는 WITH LOGIN 절을 지원합니다. ALTER USER 문이 SQL 일괄 처리의 유일한 문이 아니거나 동적 SQL에서 실행되는 경우 WITH LOGIN 절이 지원되지 않습니다.  
  
 이름  **=**  *newUserName*  
 이 사용자의 새 이름을 지정합니다. *newUserName* 현재 데이터베이스에 아직 없는 해야 합니다.  
  
 DEFAULT_SCHEMA  **=**  { *schemaName* | NULL}  
 서버에서 이 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색할 스키마를 지정합니다. 기본 스키마를 NULL로 설정하면 Windows 그룹에서 기본 스키마가 제거됩니다.   Windows 사용자에는 NULL 옵션을 사용할 수 없습니다.  
  
 암호  **=**  '*암호*'  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 변경할 사용자의 암호를 지정합니다. 암호는 대소문자를 구분합니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다. 참조 [Contained Databases](../../relational-databases/databases/contained-databases.md) 및 [sp_migrate_user_to_contained &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md) 자세한 정보에 대 한 합니다.  
  
 OLD_PASSWORD  **=**  *'oldpassword'*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.  
  
 대체 된 현재 사용자 암호 '*암호*'. 암호는 대소문자를 구분합니다. *OLD_PASSWORD* 암호를 변경 하는 데 없다면 **ALTER ANY USER** 권한. 필요한 *OLD_PASSWORD* 와 사용자가 방지 **가장** 암호를 변경할 권한이 있습니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 사용자에 대해서만 사용할 수 있습니다.  
  
 DEFAULT_LANGUAGE  **=**  *{NONE | \<lcid > | \<언어 이름 > | \<언어 별칭 >}*  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 사용자에게 할당할 기본 언어를 지정합니다. 이 옵션을 NONE으로 설정하면 기본 언어가 데이터베이스의 현재 기본 언어로 설정됩니다. 나중에 데이터베이스의 기본 언어가 변경되더라도 사용자의 기본 언어는 그대로 유지됩니다. *DEFAULT_LANGUAGE* 로컬 ID (lcid) 고 언어 또는 언어 별칭의 이름이 될 수 있습니다.  
  
> [!NOTE]  
>  이 옵션은 포함된 데이터베이스에서 포함된 사용자에 대해서만 지정할 수 있습니다.  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON | **OFF** ]]  
 **적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]합니다.  
  
 대량 복사 작업에서 서버에 대 한 암호화 메타 데이터 검사를 표시 하지 않습니다. 데이터를 대량 복사할 암호화 테이블 또는 데이터베이스 간에 사용자를 데이터를 해독 하지 않고 수 있습니다. 기본값은 OFF입니다.  
  
> [!WARNING]  
>  이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. 자세한 내용은 참조 [상시 암호화로 중요 한 데이터 보호 마이그레이션할](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)합니다.  
  
## <a name="remarks"></a>주의  
 기본 스키마는 서버에서 이 데이터베이스 사용자에 대한 개체 이름을 확인할 때 첫 번째로 검색하는 스키마가 됩니다. 달리 지정하지 않는 한 기본 스키마는 이 데이터베이스 사용자가 만든 개체의 소유자가 됩니다.  
  
 사용자에게 기본 스키마가 있는 경우에는 해당 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없지만 사용자가 기본 스키마가 있는 그룹의 멤버인 경우에는 그룹의 기본 스키마가 사용됩니다. 사용자에게 기본 스키마가 없고 사용자가 두 개 이상 그룹의 멤버인 경우 principle_id가 가장 낮고 명시적으로 설정된 기본 스키마가 있는 Windows 그룹의 기본 스키마가 사용자의 기본 스키마가 됩니다. 사용자에 대 한 기본 스키마를 확인할 수 없으면는 **dbo** 스키마가 사용 됩니다.  
  
 DEFAULT_SCHEMA는 현재 데이터베이스에 없는 스키마로 설정할 수 있습니다. 따라서 해당 스키마가 생성되기 전에 DEFAULT_SCHEMA를 사용자에게 할당할 수 있습니다.  
  
 인증서 또는 비대칭 키에 매핑된 사용자에는 DEFAULT_SCHEMA를 지정할 수 없습니다.  
  
> [!IMPORTANT]  
>  사용자의 멤버 이면 DEFAULT_SCHEMA 값은 무시 됩니다는 **sysadmin** 고정된 서버 역할입니다. 모든 멤버는 **sysadmin** 고정된 서버 역할의 기본 스키마가 있는데 `dbo`합니다.  
  
 새 사용자 이름의 SID가 데이터베이스에 기록된 SID와 일치할 때만 Windows 로그인 또는 그룹에 매핑된 사용자의 이름을 변경할 수 있습니다. 이 검사는 데이터베이스에서 Windows 로그인의 스푸핑을 방지하는 데 도움이 됩니다.  
  
 WITH LOGIN 절을 사용하면 사용자를 다른 로그인으로 다시 매핑할 수 있습니다. 로그인이 없는 사용자, 인증서로 매핑된 사용자 또는 비대칭 키에 매핑된 사용자는 이 절을 사용하여 다시 매핑할 수 없습니다. SQL 사용자 및 Windows 사용자(또는 그룹)만 다시 매핑할 수 있습니다. WITH LOGIN 절은 Windows 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 변경하는 것처럼 사용자 유형을 변경하는 데는 사용할 수 없습니다.  
  
 다음 조건이 충족되면 사용자 이름이 로그인 이름으로 자동 변경됩니다.  
  
-   사용자가 Windows 사용자입니다.  
  
-   이름이 Windows 이름입니다(백슬래시 포함).  
  
-   새 이름이 지정되지 않았습니다.  
  
-   현재 이름이 로그인 이름과 다릅니다.  
  
 위의 조건을 충족하지 않으면 사용자 이름이 변경되지 않으며 호출자가 NAME 절을 추가로 호출해야 합니다.  
  
이름에 매핑된 사용자의는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 인증서 또는 비대칭 키 백슬래시 문자를 포함할 수 없습니다 (\\).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>보안  
  
> [!NOTE]  
>  있는 사용자에 게 **ALTER ANY USER** 권한이 모든 사용자의 기본 스키마를 변경할 수 있습니다. 스키마가 변경된 사용자는 자신도 모르는 사이 잘못된 테이블에서 데이터를 선택하거나 잘못된 스키마의 코드를 실행할 수 있습니다.  
  
### <a name="permissions"></a>Permissions  
 사용자의 이름을 변경 하려면 필요는 **ALTER ANY USER** 권한.  
  
 사용자의 대상 로그인을 변경 하려면 필요는 **제어** 데이터베이스에 대 한 권한이 있습니다.  
  
 있는 사용자의 사용자 이름을 변경 하려면 **제어** 데이터베이스에 대 한 권한이 필요는 **제어** 데이터베이스에 대 한 권한이 있습니다.  
  
 기본 스키마 또는 언어를 변경 하려면 **ALTER** 사용자에 대 한 권한이 있습니다. 사용자는 자신의 기본 스키마 또는 언어를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  

모든 예는 사용자 데이터베이스에서 실행 됩니다.  

### <a name="a-changing-the-name-of-a-database-user"></a>1. 데이터베이스 사용자의 이름 변경  
 다음 예에서는 데이터베이스 사용자 `Mary5`의 이름을 `Mary51`로 변경합니다.  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>2. 사용자의 기본 스키마 변경  
 다음 예에서는 `Mary51` 사용자의 기본 스키마를 `Purchasing`으로 변경합니다.  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>3. 한 번에 여러 옵션 변경  
 다음 예에서는 포함된 데이터베이스 사용자에 대해 여러 옵션을 하나의 문에서 변경합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#’ OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP user&#40; Transact SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_migrate_user_to_contained&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  



