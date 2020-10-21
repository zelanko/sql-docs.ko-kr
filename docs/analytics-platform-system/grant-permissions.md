---
title: T-SQL 권한 부여
description: 병렬 데이터 웨어하우스의 데이터베이스 작업에 대해 T-sql 사용 권한을 부여 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257476"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에 대 한 T-sql 권한 부여
병렬 데이터 웨어하우스의 데이터베이스 작업에 대해 T-sql 사용 권한을 부여 합니다.

## <a name="grant-permissions-to-submit-database-queries"></a>데이터베이스 쿼리를 제출할 수 있는 권한 부여
이 섹션에서는 SQL Server PDW 어플라이언스에서 데이터를 쿼리할 수 있도록 데이터베이스 역할 및 사용자에 게 권한을 부여 하는 방법을 설명 합니다.  
  
데이터 쿼리를 위한 사용 권한을 부여 하는 데 사용 되는 문은 원하는 액세스 범위에 따라 다릅니다. 다음 SQL 문은 어플라이언스에 액세스할 수 있는 KimAbercrombie 라는 로그인을 만들고, **AdventureWorksPDW2012** 데이터베이스에 KimAbercrombie 라는 데이터베이스 사용자를 만들고, pdwquerydata 라는 데이터베이스 역할을 만들고, use KimAbercrombie를 pdwquerydata 역할에 추가 하 고, 개체 또는 데이터베이스 수준에 대 한 액세스 권한이 부여 되었는지 여부에 따라 쿼리 액세스를 부여 하는 옵션을 표시 합니다.  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>관리 콘솔을 사용할 수 있는 권한 부여
이 섹션에서는 관리 콘솔을 사용 하기 위해 로그인에 사용 권한을 부여 하는 방법을 설명 합니다.  
  
**관리 콘솔 사용**  
  
관리 콘솔을 사용 하려면 로그인에 서버 수준 **VIEW SERVER STATE** 권한이 필요 합니다. 다음 SQL 문은 Kim에서 관리 콘솔을 사용 하 여 SQL Server PDW 어플라이언스를 모니터링할 수 있도록 로그인에 **VIEW SERVER STATE** 권한을 부여 합니다 `KimAbercrombie` .  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**세션 중지**  
  
세션을 중지 하는 권한을 로그인에 부여 하려면 다음과 같이 **ALTER ANY CONNECTION** 권한을 부여 합니다.  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>데이터를 로드할 수 있는 권한 부여
이 섹션에서는 데이터베이스 역할 및 데이터베이스 사용자에 게 데이터를 SQL Server PDWappliance로 로드 하는 권한을 부여 하는 방법을 설명 합니다.  
  
다음 스크립트는 각 로드 옵션에 필요한 사용 권한을 보여 줍니다. 특정 요구 사항에 맞게 수정할 수 있습니다.  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>어플라이언스를 데이터 복사에 대 한 사용 권한 부여
이 섹션에서는 사용자 또는 데이터베이스 역할에 SQL Server PDW 어플라이언스에서 데이터를 복사 하는 권한을 부여 하는 방법을 설명 합니다.  
  
데이터를 다른 위치로 이동 하려면 이동할 데이터를 포함 하는 테이블에 대 한 **SELECT** 권한이 있어야 합니다.  
  
데이터의 대상이 다른 SQL Server PDW 경우에는 사용자에 게 대상에 대 한 **CREATE TABLE** 권한과 테이블이 포함 될 스키마에 대 한 **ALTER schema** 권한이 있어야 합니다.  
  
## <a name="grant-permissions-to-manage-databases"></a>데이터베이스를 관리할 수 있는 권한 부여
이 섹션에서는 SQL Server PDW 어플라이언스에서 데이터베이스를 관리 하기 위해 데이터베이스 사용자에 게 권한을 부여 하는 방법을 설명 합니다.  
  
경우에 따라 회사는 데이터베이스에 대 한 관리자를 할당 합니다. 관리자는 데이터베이스에 대 한 다른 로그인 및 데이터베이스의 데이터 및 개체에 대 한 액세스를 제어 합니다. 데이터베이스의 모든 개체, 역할 및 사용자를 관리 하기 위해 사용자에 게 데이터베이스에 대 한 **CONTROL** 권한을 부여 합니다. 다음 문은 사용자에 게 **AdventureWorksPDW2012** 데이터베이스에 대 한 **CONTROL** 권한을 부여 합니다 `KimAbercrombie` .  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
사용자에 게 어플라이언스의 모든 데이터베이스를 제어할 수 있는 권한을 부여 하려면 master 데이터베이스에서 **ALTER ANY database** 권한을 부여 합니다.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>로그인, 사용자 및 데이터베이스 역할을 관리 하는 권한 부여
이 섹션에서는 로그인, 데이터베이스 사용자 및 데이터베이스 역할을 관리 하는 권한을 부여 하는 방법을 설명 합니다.  
  
### <a name="grant-permissions-to-manage-logins"></a><a name="PermsAdminConsole"></a>로그인을 관리할 수 있는 권한 부여  
**로그인 추가 또는 관리**  
  
다음 SQL 문은 [CREATE login](../t-sql/statements/create-login-transact-sql.md) 문을 사용 하 여 새 로그인을 만들고 [alter login](../t-sql/statements/alter-login-transact-sql.md) 문을 사용 하 여 기존 로그인을 변경할 수 있는 KimAbercrombie 이라는 로그인을 만듭니다.  
  
**ALTER ANY LOGIN** 권한은 새 로그인을 만들고 기존에 삭제할 수 있는 기능을 부여 합니다. 로그인이 있으면 **ALTER ANY login** 권한 또는 해당 로그인에 대 한 **alter** 권한이 있는 로그인으로 로그인을 관리할 수 있습니다. 로그인은 자체 로그인에 대 한 암호 및 기본 데이터베이스를 변경할 수 있습니다.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>로그인 세션을 관리 하는 권한 부여  
서버에서 모든 세션을 볼 수 있도록 하려면 **VIEW SERVER STATE** 권한이 필요 합니다. 다른 로그인의 세션을 종료 하는 기능에는 **ALTER ANY CONNECTION** 권한이 필요 합니다. 다음 예에서는 앞에서 `KimAbercrombie` 만든 로그인을 사용 합니다.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>데이터베이스 사용자를 관리할 수 있는 권한 부여  
데이터베이스 사용자를 만들고 삭제 하려면 **ALTER ANY USER** 권한이 필요 합니다. 기존 사용자를 관리 하려면 **ALTER ANY user** 권한 또는 해당 사용자에 대 한 **alter** 권한이 필요 합니다. 다음 예에서는 앞에서 `KimAbercrombie` 만든 로그인을 사용 합니다.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>권한이에 데이터베이스 역할 관리 권한 부여  
사용자 정의 데이터베이스 역할을 만들고 삭제 하려면 **ALTER ANY ROLE** 권한이 필요 합니다. 다음 예에서는 이전에 `KimAbercrombie` 만든 로그인 및 사용을 사용 합니다.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>로그인, 사용자 및 역할 권한 차트  
다음 차트는 혼란 스 러 울 수 있지만 제어와 같은 더 높은 수의 추가 권한 (예: 변경)을 별도로 부여할 수 있는 보다 세분화 된 사용 권한을 포함 하는 방법을 보여 줍니다. 사용자가 필요한 작업을 완료 하는 데는 항상 최소한의 권한을 부여 하는 것이 좋습니다. 이렇게 하려면 최상위 권한 대신 더 구체적인 사용 권한을 부여 합니다.  
  
**로그인 권한:**  
  
![APS 보안 로그인 권한](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**사용자 권한:**  
  
![APS 보안 사용자 권한](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**역할 권한:**  
  
![APS 보안 역할 권한](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>어플라이언스를 모니터링할 수 있는 권한 부여
관리 콘솔 또는 SQL Server PDW 시스템 뷰를 사용 하 여 SQL Server PDW 어플라이언스를 모니터링할 수 있습니다. 로그인 하려면 어플라이언스를 모니터링 하려면 서버 수준 **VIEW SERVER STATE** 권한이 필요 합니다. 로그인에는 관리 콘솔 이나 **KILL** 명령을 사용 하 여 연결을 종료 하는 **ALTER ANY CONNECTION** 권한이 필요 합니다. 관리 콘솔을 사용 하는 데 필요한 사용 권한에 대 한 자세한 내용은 [관리자 콘솔을 사용할 수 있는 권한 부여 &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)를 참조 하세요.  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views"></a><a name="PermsAdminConsole"></a>시스템 뷰를 사용 하 여 어플라이언스를 모니터링할 수 있는 권한 부여  
다음 SQL 문은 라는 로그인을 만들고 `monitor_login` 로그인에 **VIEW SERVER STATE** 권한을 부여 합니다 `monitor_login` .  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>시스템 뷰를 사용 하 여 어플라이언스를 모니터링 하 고 연결을 종료할 수 있는 권한 부여  
다음 SQL 문은 라는 로그인을 만들고이 로그인 `monitor_and_terminate_login` 에 **VIEW SERVER STATE** 및 **ALTER ANY CONNECTION** 권한을 부여 합니다 `monitor_and_terminate_login` .  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
관리자 로그인을 만들려면 [고정 서버 역할](pdw-permissions.md#fixed-server-roles)을 참조 하세요.  
  
## <a name="see-also"></a>참조
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[사용자 만들기](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[로드](load-overview.md)  
