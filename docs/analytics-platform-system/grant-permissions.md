---
title: 사용 권한 부여
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: 35542a9ea2544f0bdd357d3609937e1596e00a3f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="grant-permissions"></a>사용 권한 부여

## <a name="grant-permissions-to-submit-database-queries"></a>데이터베이스 쿼리를 전송 하는 권한 부여
이 섹션에서는 사용자가 SQL Server PDW 어플라이언스에에서 데이터를 쿼리할 수 및 데이터베이스 역할에 권한을 부여 하는 방법을 설명 합니다.  
  
문은 쿼리 데이터에 대 한 사용 권한을 부여 하는 데 필요한 액세스 범위에 따라 다릅니다. 다음 SQL 문을 어플라이언스에 액세스에서 KimAbercrombie 라는 데이터베이스 사용자를 만들 수 있는 KimAbercrombie 이라는 로그인을 만듭니다는 **AdventureWorksPDW2012** PDWQueryData 라는 데이터베이스 역할을 만들고, 추가, 데이터베이스 사용 하 여 KimAbercrombie PDWQueryData 역할 및 다음 쿼리 액세스 권한 부여에 대 한 표시 옵션에 개체 또는 데이터베이스 수준에서에 액세스 권한이 부여 되는 여부에 따라.  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>관리 콘솔을 사용 하는 권한 부여
이 섹션에서는 관리 콘솔을 사용 하려면 로그인에 사용 권한을 부여 하는 방법을 설명 합니다.  
  
**관리 콘솔을 사용 하 여**  
  
로그인 필요한 서버 수준 관리 콘솔을 사용 하려면 **VIEW SERVER STATE** 권한. 다음 SQL 문은 부여는 **VIEW SERVER STATE** 로그인에 권한을 `KimAbercrombie` Kim SQL Server PDW 어플라이언스를 모니터링 하는 관리 콘솔을 사용할 수 있도록 합니다.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**세션을 중지 합니다.**  
  
로그인 세션을 해제 하는 권한을 부여 하려면 부여는 **ALTER ANY CONNECTION** 다음과 같이 사용 권한:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>데이터를 로드 하는 권한 부여
이 섹션에서는 SQL Server PDWappliance에 데이터를 로드 하려면 데이터베이스 역할 및 데이터베이스 사용자 권한을 부여 하는 방법에 설명 합니다.  
  
다음 스크립트는 어떠한 권한이 필요한 각 로드 옵션에 대 한 지 보여 줍니다. 이 특정 요구를 충족 하도록 수정할 수 있습니다.  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>기기에서 데이터를 복사 하는 권한 부여
이 섹션에서는 SQL Server PDW 어플라이언스에 데이터를 복사 하 여 사용자 또는 데이터베이스 역할에 권한을 부여 하는 방법을 설명 합니다.  
  
데이터를 다른 위치로 이동 하려면 필요 **선택** 데이터가 포함 된 테이블에 대 한를 이동 해야 합니다.  
  
사용자 데이터에 대 한 대상이 다른 SQL Server PDW 있으면 있어야 **CREATE TABLE** 대상에 대 한 사용 권한 및 **ALTER SCHEMA** 테이블을 포함할 스키마에 대 한 권한이 있습니다.  
  
## <a name="grant-permissions-to-manage-databases"></a>데이터베이스를 관리 하는 권한 부여
이 섹션에서는 SQL Server PDW 어플라이언스에 데이터베이스를 관리 하는 데이터베이스 사용자에 게 권한을 부여 하는 방법을 설명 합니다.  
  
경우에 따라 회사 데이터베이스에 대 한 관리자를 할당합니다. 관리자는 다른 로그인을 데이터베이스 뿐만 아니라 데이터 및 데이터베이스의 개체에 대 한 액세스를 제어 합니다. 모든 관리 개체, 역할 및 사용자에 게 부여 된 데이터베이스의 사용자는 **제어** 데이터베이스에 대 한 권한이 있습니다. 다음 문은 부여는 **제어** 에 대 한 권한이 **AdventureWorksPDW2012** 데이터베이스 사용자에 게 `KimAbercrombie`합니다.  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
에 게 부여 하려면 사용자 기기에 있는 모든 데이터베이스를 제어할 수 있는 권한 부여는 **ALTER ANY DATABASE** master 데이터베이스에 대 한 사용 권한입니다.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>로그인, 사용자를 관리 하 고 데이터베이스 역할에 권한 부여
이 섹션에서는 로그인, 데이터베이스 사용자 및 데이터베이스 역할을 관리할 수 있는 권한을 부여 하는 방법을 설명 합니다.  
  
### <a name="PermsAdminConsole"></a>로그인을 관리 하는 권한 부여  
**추가 하거나 로그인 관리**  
  
다음 SQL 문을 사용 하 여 새 로그인을 만들 수 있는 KimAbercrombie 이라는 로그인을 만듭니다는 [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) 문을 사용 하 여 기존 로그인을 변경 하 고는 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) 문.  
  
**ALTER ANY LOGIN** 사용 새 로그인을 만들고 기존을 삭제할 수 있는 권한을 부여 합니다. 로그인이 있는 되 면 로그인을 사용 하 여 로그인 하 여 관리할 수 있습니다는 **ALTER ANY LOGIN** 권한 또는 **ALTER** 해당 로그인에 대 한 권한이 있습니다. 로그인 자체 로그인에 대 한 암호 및 기본 데이터베이스를 변경할 수 있습니다.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>로그인 세션을 관리 하는 권한 부여  
서버에서 모든 세션을 볼 수 있도록 하려면 필요는 **VIEW SERVER STATE** 권한. 다른 로그인 세션을 종료 하는 기능 요구는 **ALTER ANY CONNECTION** 권한. 다음 예제에서는 `KimAbercrombie` 앞에서 만든 로그인입니다.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>데이터베이스 사용자를 관리 하는 권한 부여  
만들기 및 데이터베이스 사용자를 삭제 해야는 **ALTER ANY USER** 권한. 기존 사용자를 관리 하려면 필요는 **ALTER ANY USER** 권한 또는 **ALTER** 해당 사용자에 대 한 권한이 있습니다. 다음 예제에서는 `KimAbercrombie` 앞에서 만든 로그인입니다.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>데이터베이스 역할 관리에 대 한 권한을 부여합니다  
만들기 및 사용자 정의 데이터베이스 역할을 삭제 해야는 **ALTER ANY ROLE** 권한. 다음 예제에서는 `KimAbercrombie` 로그인 및 사용 하 여 이전에 만든 합니다.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>로그인, 사용자 및 역할 사용 권한 차트  
다음 차트는 혼동 될 수 있지만 방법을 더 높은 수준 권한 (예: 제어)를 보여 줍니다 별도로 (예: ALTER) 부여할 수 있는 보다 세부적인 권한을 포함 합니다. 항상 최소한의 다른 사용자에 게 필요한 작업을 완료할에 대 한 권한 부여 하는 것이 좋습니다. 이렇게 하려면 최상위 수준 권한 대신 보다 구체적인 사용 권한을 부여 합니다.  
  
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
관리 콘솔 또는 SQL Server PDW 시스템 뷰를 사용 하 여 SQL Server PDW 어플라이언스를 모니터링할 수 있습니다. 로그인은 서버 수준 필요 **VIEW SERVER STATE** 기기를 모니터링할 수 있는 합니다. 로그인 필요는 **ALTER ANY CONNECTION** 관리 콘솔을 사용 하 여 연결을 끊을 수 있는 권한을 또는 **KILL** 명령입니다. 관리 콘솔을 사용 하는 데 필요한 사용 권한에 대 한 자세한 내용은 참조 하십시오. [관리 콘솔을 사용할 수 있는 권한을 부여 &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)합니다.  
  
### <a name="PermsAdminConsole"></a>시스템 뷰를 사용 하 여 어플라이언스에 모니터링 하는 권한 부여  
다음 SQL 문은 이라는 로그인을 만듭니다 `monitor_login` 하 고 권한을 부여는 **VIEW SERVER STATE** 권한을 `monitor_login` 로그인 합니다.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>시스템 뷰를 사용 하 여 어플라이언스에 모니터링 하 고 연결을 종료 하는 권한 부여  
다음 SQL 문은 이라는 로그인을 만듭니다 `monitor_and_terminate_login` 부여는 **VIEW SERVER STATE** 및 **ALTER ANY CONNECTION** 권한을 `monitor_and_terminate_login` 로그인 합니다.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
참조 관리자 로그인을 만들려는 [고정 서버 역할](pdw-permissions.md#fixed-server-roles)합니다.  
  
## <a name="see-also"></a>참고 항목
[로그인 만들기](../t-sql/statements/create-login-transact-sql.md)  
[사용자 만들기](../t-sql/statements/create-user-transact-sql.md)  
[역할 만들기](../t-sql/statements/create-role-transact-sql.md)  
[부하](load-overview.md)  
