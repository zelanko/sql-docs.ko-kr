---
title: 사용 권한 부여 T-SQL-병렬 데이터 웨어하우스 | Microsoft Docs
description: Parallel Data Warehouse에서 데이터베이스 작업에 대 한 권한 부여 T-SQL입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 15798edc4d6a9b1f00c8dd489dfed76a39e5f340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960942"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Parallel Data Warehouse에 대 한 권한 부여 T-SQL
Parallel Data Warehouse에서 데이터베이스 작업에 대 한 권한 부여 T-SQL입니다.

## <a name="grant-permissions-to-submit-database-queries"></a>데이터베이스 쿼리를 제출 하는 권한 부여
이 섹션에는 SQL Server PDW appliance에서 데이터를 쿼리 하는 사용자 및 데이터베이스 역할에 권한을 부여 하는 방법을 설명 합니다.  
  
문이 데이터를 쿼리 하는 권한을 부여 하는 데 필요한 액세스 범위에 따라 달라 집니다. 다음 SQL 문을 만들 어플라이언스에 액세스, KimAbercrombie에서 명명 된 데이터베이스 사용자를 만들 수 있는 KimAbercrombie 이라는 로그인을 **AdventureWorksPDW2012** 데이터베이스, PDWQueryData 라는 데이터베이스 역할 만들기, 추가 사용 하 여 KimAbercrombie PDWQueryData 역할 및 다음 쿼리 액세스 권한을 부여 하는 것에 대 한 표시 옵션 개체 또는 데이터베이스 수준에서의 액세스 권한을 부여 하는지 여부에 따라 합니다.  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>관리자 콘솔을 사용 하는 권한 부여
이 섹션에서는 관리 콘솔을 사용 하려면 로그인 권한을 부여 하는 방법을 설명 합니다.  
  
**관리 콘솔을 사용 하 여**  
  
관리 콘솔을 사용 하 여 로그인 하려면 서버 수준 **VIEW SERVER STATE** 권한. 다음 SQL 문은 권한을 부여 합니다 **VIEW SERVER STATE** 로그인에 권한을 `KimAbercrombie` Kim SQL Server PDW 어플라이언스를 모니터링 하는 관리 콘솔을 사용할 수 있도록 합니다.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**세션 중지**  
  
로그인 세션을 종료 하려면 권한을 부여 하려면 권한을 부여 합니다 **ALTER ANY CONNECTION** 다음과 같은 사용 권한:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>데이터를 로드 하는 권한 부여
이 섹션에서는 SQL Server PDWappliance에 데이터를 로드 하려면 데이터베이스 역할 및 데이터베이스 사용자에 게 권한을 부여 하는 방법을 설명 합니다.  
  
다음 스크립트는 각 로드 옵션에 대해 하는 데 필요한 권한은 보여 줍니다. 특정 요구 사항에 맞게이 수정할 수 있습니다.  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>어플라이언스 외부에 데이터를 복사 하는 권한 부여
이 섹션에는 SQL Server PDW 어플라이언스는 데이터를 복사 하는 사용자 또는 데이터베이스 역할에 권한을 부여 하는 방법을 설명 합니다.  
  
데이터를 다른 위치로 이동 하려면 **선택** 이동할 데이터가 포함 된 테이블에 대 한 권한이 있습니다.  
  
사용자 데이터에 대 한 대상이 다른 SQL Server PDW 있으면 있어야 **CREATE TABLE** 대상에 대 한 사용 권한 및 **ALTER SCHEMA** 테이블을 포함 하는 스키마에 대 한 권한.  
  
## <a name="grant-permissions-to-manage-databases"></a>데이터베이스를 관리 하는 권한 부여
이 섹션에는 SQL Server PDW appliance에서 데이터베이스를 관리 하는 데이터베이스 사용자에 권한을 부여 하는 방법을 설명 합니다.  
  
경우에 따라 회사 데이터베이스에 대 한 관리자를 할당합니다. 관리자는 다른 로그인 데이터베이스 뿐만 아니라 데이터 및 데이터베이스의 개체에 대 한 액세스를 제어 합니다. 모든 관리 개체, 역할 및 사용자 데이터베이스에서 사용자에 게 부여 합니다 **제어** 데이터베이스에 대 한 권한. 다음 문은 부여 합니다 **컨트롤** 에 대 한 권한이 **AdventureWorksPDW2012** 사용자에 게 데이터베이스 `KimAbercrombie`합니다.  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
기기에 있는 모든 데이터베이스를 제어할 수 있는 권한이 사용자에 게 부여 하려면 권한을 부여 합니다 **ALTER ANY DATABASE** master 데이터베이스에 대 한 사용 권한.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>로그인, 사용자 관리 및 데이터베이스 역할에 권한 부여
이 섹션에서는 로그인, 데이터베이스 사용자 및 데이터베이스 역할을 관리 하는 권한을 부여 하는 방법을 설명 합니다.  
  
### <a name="PermsAdminConsole"></a>로그인을 관리할 권한 부여  
**추가 하거나 로그인 관리**  
  
다음 SQL 문을 사용 하 여 새 로그인을 만들 수 있는 KimAbercrombie 라는 로그인을 만듭니다는 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문을 사용 하 여 기존 로그인을 변경 하 고는 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) 문입니다.  
  
합니다 **ALTER ANY LOGIN** 권한 부여를 새 로그인을 만들고 기존을 삭제할 수 있습니다. 로그인 되 면 로그인을 사용 하 여 로그인 하 여 관리할 수 있습니다 합니다 **ALTER ANY LOGIN** 권한 또는 **ALTER** 해당 로그인에 대 한 권한. 로그인 자체 로그인을 위한 암호 및 기본 데이터베이스를 변경할 수 있습니다.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>로그인 세션을 관리 하는 권한 부여  
서버의 모든 세션을 확인 하는 기능이 필요 합니다 **VIEW SERVER STATE** 권한. 다른 로그인의 세션을 종료 하는 기능이 필요 합니다 **ALTER ANY CONNECTION** 권한. 다음 예제에서는 `KimAbercrombie` 앞에서 만든 로그인입니다.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>데이터베이스 사용자를 관리할 수 있는 권한을 부여 합니다.  
만들기 및 데이터베이스 사용자를 삭제 해야 합니다 **ALTER ANY USER** 권한. 기존 사용자를 관리 하려면 필요 합니다 **ALTER ANY USER** 권한 또는 **ALTER** 해당 사용자에 대 한 권한이 있습니다. 다음 예제에서는 `KimAbercrombie` 앞에서 만든 로그인입니다.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>데이터베이스 역할 관리에 대 한 권한 부여  
만들기 및 사용자 정의 데이터베이스 역할을 삭제 해야 합니다 **ALTER ANY ROLE** 권한. 다음 예제에서는 `KimAbercrombie` 로그인 및 사용 하 여 이전에 생성 합니다.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>로그인, 사용자 및 역할 사용 권한 차트  
다음 차트는 혼동 될 수 있지만 어떻게 더 높은 수준 권한 (예: 컨트롤) 표시 개별적으로 (예: ALTER) 부여할 수 있는 보다 세부적인 사용 권한을 포함 합니다. 항상 최소한의 다른 사용자에 게 필요한 작업 완료에 대 한 권한 부여 하는 것이 좋습니다. 이렇게 하려면 최상위 수준 사용 권한이 아니라 보다 구체적인 사용 권한을 부여 합니다.  
  
**로그인 사용 권한:**  
  
![APS 보안 로그인 권한](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**사용자 권한:**  
  
![APS 보안 사용자 권한](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**역할 사용 권한:**  
  
![APS 보안 역할 권한](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>어플라이언스를 모니터링 하는 권한 부여
관리 콘솔 또는 SQL Server PDW 시스템 뷰를 사용 하 여 SQL Server PDW 어플라이언스에 모니터링할 수 있습니다. 로그인에 서버 수준 필요 **VIEW SERVER STATE** 기기를 모니터링할 수 있는 권한이 있습니다. 로그인 필요 합니다 **ALTER ANY CONNECTION** 관리 콘솔을 사용 하 여 연결을 종료 할 또는 **KILL** 명령입니다. 관리 콘솔을 사용 하는 데 필요한 권한에 대 한 자세한 내용은 [관리자 콘솔을 사용 하려면 권한 부여 &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)합니다.  
  
### <a name="PermsAdminConsole"></a>시스템 뷰를 사용 하 여 어플라이언스 모니터링 하는 권한 부여  
다음 SQL 문은 이라는 로그인을 만듭니다 `monitor_login` 권한을 부여 합니다 **VIEW SERVER STATE** 권한을 `monitor_login` 로그인 합니다.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>시스템 뷰를 사용 하 여 어플라이언스를 모니터링 하 고 연결을 종료 하는 권한 부여  
다음 SQL 문은 이라는 로그인을 만듭니다 `monitor_and_terminate_login` 권한을 부여 합니다 **VIEW SERVER STATE** 및 **ALTER ANY CONNECTION** 권한을 `monitor_and_terminate_login` 로그인 합니다.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
참조 관리자 로그인을 만들려면 [고정 서버 역할](pdw-permissions.md#fixed-server-roles)입니다.  
  
## <a name="see-also"></a>참조
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[사용자 만들기](../t-sql/statements/create-user-transact-sql.md)  
[역할 만들기](../t-sql/statements/create-role-transact-sql.md)  
[로드](load-overview.md)  
