---
title: 분리된 사용자 문제 해결
description: 분리된 사용자는 데이터베이스 사용자 로그인이 master 데이터베이스에 더 이상 존재하지 않는 경우 발생합니다. 이 문서에서는 분리된 사용자를 식별 및 해결하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e302910a5a7870ed7c57a7325e6686f42a15707
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999728"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>분리된 사용자 문제 해결(SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 분리된 사용자는 데이터베이스 사용자가 **마스터** 데이터베이스의 로그인을 기반으로 하지만 해당 로그인이 **마스터**에 더 이상 존재하지 않는 경우 발생합니다. 이는 로그인이 삭제되었거나 데이터베이스가 로그인이 존재하지 않는 다른 서버로 이동된 경우에 발생할 수 있습니다. 이 항목에서는 분리된 사용자를 찾아서 로그인에 다시 매핑하는 방법을 설명합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스 사용자를 이동될 수 있는 데이터베이스에 사용하면 분리된 사용자가 발생할 가능성이 감소합니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
## <a name="background"></a>배경  
 로그인을 기반으로 하는 보안 주체(데이터베이스 사용자 ID)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 있는 데이터베이스에 연결하려면 해당 주체가 **master** 데이터베이스에 유효한 로그인을 가지고 있어야 합니다. 이 로그인은 주체의 ID를 확인하고 해당 주체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결할 수 있는지 여부를 확인하는 인증 프로세스에서 사용됩니다. 서버 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 **sys.server_principals** 카탈로그 뷰 및 **sys.sql_logins** 호환성 뷰에서 볼 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑된 "데이터베이스 사용자"를 사용하여 개별 데이터베이스에 액세스합니다. 이 규칙에는 세 가지 예외가 있습니다.  
  
-   포함된 데이터베이스 사용자  
  
     포함된 데이터베이스 사용자는 사용자 데이터베이스 수준에서 인증하며 로그인과 연결되지 않습니다. 이 방법은 데이터베이스의 이식성이 개선되고 포함된 데이터베이스 사용자가 분리될 수 없기 때문에 권장됩니다. 그러나 각 데이터베이스에 대해 사용자를 다시 만들어야 합니다. 데이터베이스가 많은 환경에서는 이렇게 하는 것이 어렵습니다.  
  
-   **게스트** 계정.  
  
     데이터베이스에서 사용하도록 설정된 경우, 이 계정은 데이터베이스 사용자에 매핑되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 **게스트** 사용자로 데이터베이스에 액세스할 수 있도록 합니다. **게스트** 계정은 기본적으로 사용하지 않도록 설정되어 있습니다.  
  
-   Microsoft Windows 그룹 멤버 자격  
  
     Windows 사용자로부터 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 해당 Windows 사용자가 Windows 그룹의 멤버인 동시에 데이터베이스의 사용자인 경우 데이터베이스에 액세스할 수 있습니다.  
  
 데이터베이스 사용자로의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 매핑에 대한 정보는 데이터베이스 내에 저장됩니다. 데이터베이스 사용자 이름과 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 SID가 여기에 포함됩니다. 이 데이터베이스 사용자의 사용 권한은 데이터베이스에서 권한 부여에 적용됩니다.  
  
 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 인스턴스에서 정의되지 않았거나 잘못 정의되어 있는 데이터베이스 사용자(로그인 기반)는 이 인스턴스에 로그인할 수 없습니다. 이러한 사용자는 해당 서버 인스턴스에 있는 데이터베이스의 *분리된 사용자* 라고 합니다. 데이터베이스 사용자가 `master` 인스턴스에 없는 로그인 SID로 매핑되는 경우 사용자가 분리될 수 있습니다. 로그인이 생성되지 않은 경우 데이터베이스가 복원되거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다른 인스턴스에 연결된 후 데이터베이스 사용자가 분리될 수 있습니다. 또한 데이터베이스 사용자는 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 삭제되면 분리될 수 있습니다. 로그인을 다시 만들더라도 SID가 다르므로 여전히 데이터베이스 사용자가 분리됩니다.  
  
## <a name="detect-orphaned-users"></a>분리된 사용자 검색  

**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 PDW의 경우**

누락된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인을 기준으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 분리된 사용자를 검색하려면 사용자 데이터베이스에서 다음 문을 실행합니다.  
  
```  
SELECT dp.type_desc, dp.SID, dp.name AS user_name  
FROM sys.database_principals AS dp  
LEFT JOIN sys.server_principals AS sp  
    ON dp.SID = sp.SID  
WHERE sp.SID IS NULL  
    AND authentication_type_desc = 'INSTANCE';  
```  
  
 현재 데이터베이스에 있으며 어떤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에도 연결되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 사용자와 이에 해당되는 SID(보안 ID)가 나열됩니다.  

**SQL 데이터베이스 및 SQL 데이터 웨어하우스의 경우**

SQL 데이터베이스 또는 SQL 데이터 웨어하우스에서는 `sys.server_principals` 테이블을 사용할 수 없습니다. 이러한 환경에서 분리된 사용자를 확인하려면 다음 단계를 따르세요.

1. `master` 데이터베이스에 연결하고 다음 쿼리를 사용하여 로그인의 SID를 선택합니다.
    ```
    SELECT sid 
    FROM sys.sql_logins 
    WHERE type = 'S'; 
    ```

2. 사용자 데이터베이스에 연결하고 다음 쿼리를 사용하여 `sys.database_principals` 테이블의 사용자 SID를 검토합니다.

    ```
    SELECT name, sid, principal_id
    FROM sys.database_principals 
    WHERE type = 'S' 
      AND name NOT IN ('guest', 'INFORMATION_SCHEMA', 'sys')
      AND authentication_type_desc = 'INSTANCE';
    ```

3. 두 목록을 비교하여 사용자 데이터베이스 `sys.database_principals` 테이블에 master 데이터베이스 `sql_logins` 테이블의 로그인 SID와 일치하지 않는 사용자 SID가 있는지 확인합니다. 
  
## <a name="resolve-an-orphaned-user"></a>분리된 사용자 해결  
master 데이터베이스에서 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 문을 SID 옵션과 함께 사용하고 이전 섹션에서 받은 데이터베이스 사용자의 `SID` 를 제공하여 누락된 로그인을 다시 만듭니다.  
  
```  
CREATE LOGIN <login_name>   
WITH PASSWORD = '<use_a_strong_password_here>',  
SID = <SID>;  
```  
  
 분리된 사용자를 **master**에 이미 존재하는 로그인에 매핑하려면 사용자 데이터베이스에서 로그인 이름을 지정하여 [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) 문을 실행합니다.  
  
```  
ALTER USER <user_name> WITH Login = <login_name>;  
```  
  
 누락된 로그인을 다시 만들 때 사용자가 제공된 암호를 사용하여 데이터베이스에 액세스할 수 있습니다. 그런 다음 ALTER LOGIN 문을 사용하여 로그인 계정의 암호를 변경할 수 있습니다.  
  
```  
ALTER LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
> [!IMPORTANT]  
>  어떤 로그인으로도 자신의 암호를 변경할 수 있습니다. `ALTER ANY LOGIN` 사용 권한이 있는 로그인으로만 다른 사용자의 로그인 암호를 변경할 수 있습니다. 그러나 **sysadmin** 역할의 멤버만 **sysadmin** 역할 멤버의 암호를 수정할 수 있습니다.  
  
 사용되지 않는 프로시저 [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md) 은 분리된 사용자에 대해서도 작동합니다. `sp_change_users_login` 에 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER USER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_change_users_login&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_password&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)   
 [sys.sysusers&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)   
 [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md) [sys.syslogins&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
  
  
