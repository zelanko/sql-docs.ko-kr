---
title: GRANT Server Permissions(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- GRANT statement, servers
- permissions [SQL Server], servers
- servers [SQL Server], permissions
- granting permissions [SQL Server], servers
ms.assetid: 7e880a5a-3bdc-491f-a167-7a9ed338be7f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 424bb9cf8db72c399a733d1e4ffe3eb55bd14427
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="grant-server-permissions-transact-sql"></a>GRANT 서버 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에 대한 사용 권한을 부여합니다. 
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ] [ WITH GRANT OPTION ]  
    [ AS <grantor_principal> ]  
  
<grantee_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
  
<grantor_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 서버에 대해 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 \<grantee_principal>에 대해 사용 권한을 부여할 보안 주체를 지정합니다.  
  
 \<grantor_principal>로서 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 보안 주체를 지정합니다.  
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login_mapped_to_Windows_login*  
 Windows 로그인으로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login_mapped_to_Windows_group*  
 Windows 그룹으로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login_mapped_to_certificate*  
 인증서로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login_mapped_to_asymmetric_key*  
 비대칭 키로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *server_role*  
 사용자 정의 서버 역할을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 현재 데이터베이스가 master인 경우에만 서버 범위의 사용 권한을 부여할 수 있습니다.  
  
 서버 사용 권한에 대한 정보는 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰에 표시되고 서버 보안 주체에 대한 정보는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰에 표시됩니다. 서버 역할의 멤버 자격에 대한 정보는 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 서버는 사용 권한 계층에서 가장 높은 수준입니다. 다음 표에는 서버에서 부여될 수 있는 가장 제한적인 특정 사용 권한이 나열되어 있습니다.  
  
|서버 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|CREATE AVAILABILITY GROUP<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="remarks"></a>Remarks  
 다음 세 가지 서버 사용 권한이 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 추가되었습니다.  
  
 **CONNECT ANY DATABASE** 권한  
 현재 있는 모든 데이터베이스와 향후 만들 수 있는 새로운 데이터베이스에 연결해야 하는 로그인에 **CONNECT ANY DATABASE** 를 부여합니다. 연결을 벗어나는 데이터베이스에서는 사용 권한을 부여하지 않습니다. **SELECT ALL USER SECURABLES** 또는 **VIEW SERVER STATE**와 결합하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 모든 데이터 또는 모든 데이터베이스 상태를 보기 위한 감사 프로세스를 허용합니다.  
  
 **IMPERSONATE ANY LOGIN** 권한  
 허용하면 데이터베이스에 연결할 때 중간 계층 프로세스가 클라이언트 계정을 가장하여 연결할 수 있습니다. 거부하면 높은 권한 로그인이 다른 로그인을 가장하지 못하도록 차단할 수 있습니다. 예를 들어, **CONTROL SERVER** 권한이 있는 로그인이 다른 로그인을 가장하지 못하도록 차단할 수 있습니다.  
  
 **SELECT ALL USER SECURABLES** 권한  
 허용하면 감사자 등으로 로그인하여 사용자 연결이 가능한 모든 데이터베이스에서 데이터를 볼 수 있습니다. 거부하면 개체가 **sys** 스키마에 있지 않는 한 개체에 대한 액세스를 차단합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다. sysadmin 고정 서버 역할의 멤버는 모든 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-a-permission-to-a-login"></a>1. 로그인에 사용 권한 부여  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `CONTROL SERVER`에 대해 `TerryEminhizer` 권한을 부여합니다.  
  
```  
USE master;  
GRANT CONTROL SERVER TO TerryEminhizer;  
GO  
```  
  
### <a name="b-granting-a-permission-that-has-grant-permission"></a>2. GRANT 권한이 있는 사용 권한 부여  
 다음 예에서는 다른 로그인에 사용 권한을 부여할 수 있는 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `ALTER ANY EVENT NOTIFICATION`에 대해 `JanethEsteves`을 부여합니다.  
  
```  
USE master;  
GRANT ALTER ANY EVENT NOTIFICATION TO JanethEsteves WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-a-permission-to-a-server-role"></a>3. 서버 역할에 사용 권한 부여  
 다음 예에서는 `ITDevAdmin` 및 `ITDevelopers`라는 두 개의 서버 역할을 만듭니다. `ALTER ANY DATABASE` 서버 역할이 `ITDevAdmin` 권한을 다시 할당할 수 있도록 `WITH GRANT` 옵션을 포함하여 `ITDevAdmin` 사용자 정의 서버 역할에 `ALTER ANY DATABASE` 권한을 부여합니다. 그럼 다음 예에서 `ITDevelopers` 서버 역할의 `ALTER ANY DATABASE` 권한을 사용할 사용 권한을 `ITDevAdmin`에 부여합니다.  
  
```  
USE master;  
CREATE SERVER ROLE ITDevAdmin ;  
CREATE SERVER ROLE ITDevelopers ;  
GRANT ALTER ANY DATABASE TO ITDevAdmin WITH GRANT OPTION ;  
GRANT ALTER ANY DATABASE TO ITDevelopers AS ITDevAdmin ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [DENY 서버 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [REVOKE 서버 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

