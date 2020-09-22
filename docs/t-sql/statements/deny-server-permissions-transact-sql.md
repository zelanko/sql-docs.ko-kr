---
description: DENY 서버 사용 권한(Transact-SQL)
title: DENY Server Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], servers
- denying permissions [SQL Server], servers
- servers [SQL Server], permissions
- DENY statement, servers
ms.assetid: 68d6b2a9-c36f-465a-9cd2-01d43a667e99
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 67833e662688b6de418fc6d7db169f1107866035
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688608"
---
# <a name="deny-server-permissions-transact-sql"></a>DENY 서버 사용 권한(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  서버에 대한 사용 권한을 거부합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DENY permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ]  
    [ CASCADE ]  
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *permission*  
 서버에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 CASCADE  
 지정된 보안 주체와 이 보안 주체가 사용 권한을 부여한 다른 모든 보안 주체에 대해 사용 권한이 거부됨을 나타냅니다. 보안 주체에 GRANT OPTION 권한이 있는 경우에 필요합니다. 
  
 TO \<server_principal>  
 사용 권한이 거부된 보안 주체를 지정합니다.  
  
 AS \<grantor_principal>  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 거부하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다.
권한의 거부자로서 기록된 보안 주체가 해당 문을 실행하는 사용자 이외의 다른 보안 주체여야 한다는 것을 표시하려면 AS 주절을 사용합니다. 예를 들어 Mary라는 사용자가 principal_id 12이고 Raul이라는 사용자는 principal 15라고 가정해 보겠습니다. Mary는 `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`을 실행합니다. 이제 sys.database_permissions 테이블은 해당 문을 실제로 사용자 13(Mary)가 실행했지만 거부 문의 grantor_prinicpal_id가 15(Raul)임을 표시합니다.
  
이 명령문에 AS를 사용한다고 해서 다른 사용자로 가장하는 기능을 의미하는 것은 아닙니다.    
  
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
 서버 역할을 지정합니다.  
  
## <a name="remarks"></a>설명  
 현재 데이터베이스가 master인 경우에만 서버 범위의 사용 권한을 거부할 수 있습니다.  
  
 서버 사용 권한에 대한 정보는 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰에 표시되고 서버 보안 주체에 대한 정보는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰에 표시됩니다. 서버 역할의 멤버 자격에 대한 정보는 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 서버는 사용 권한 계층에서 가장 높은 수준입니다. 다음 표에는 서버에서 거부될 수 있는 가장 제한적인 특정 사용 권한이 나열되어 있습니다.  
  
|서버 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|CREATE AVAILABILITY GROUP<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="remarks"></a>설명  
 다음 세 가지 서버 사용 권한이 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 추가되었습니다.  
  
 **CONNECT ANY DATABASE** 권한  
 현재 있는 모든 데이터베이스와 향후 만들 수 있는 새로운 데이터베이스에 연결해야 하는 로그인에 **CONNECT ANY DATABASE** 를 부여합니다. 연결을 벗어나는 데이터베이스에서는 사용 권한을 부여하지 않습니다. **SELECT ALL USER SECURABLES** 또는 **VIEW SERVER STATE**와 결합하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있는 모든 데이터 또는 모든 데이터베이스 상태를 보기 위한 감사 프로세스를 허용합니다.  
  
 **IMPERSONATE ANY LOGIN** 권한  
 허용하면 데이터베이스에 연결할 때 중간 계층 프로세스가 클라이언트 계정을 가장하여 연결할 수 있습니다. 거부하면 높은 권한 로그인이 다른 로그인을 가장하지 못하도록 차단할 수 있습니다. 예를 들어, **CONTROL SERVER** 권한이 있는 로그인이 다른 로그인을 가장하지 못하도록 차단할 수 있습니다.  
  
 **SELECT ALL USER SECURABLES** 권한  
 허용하면 감사자 등으로 로그인하여 사용자 연결이 가능한 모든 데이터베이스에서 데이터를 볼 수 있습니다. 거부하면 개체가 **sys** 스키마에 있지 않는 한 개체에 대한 액세스를 차단합니다.  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한 또는 보안 개체의 소유권이 필요합니다. AS 절을 사용하는 경우 지정된 보안 주체가 사용 권한을 거부할 보안 개체를 소유해야 합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-denying-connect-sql-permission-to-a-sql-server-login-and-principals-to-which-the-login-has-regranted-it"></a>A. SQL Server 로그인 및 이 로그인이 사용 권한을 다시 부여한 보안 주체에 대해 CONNECT SQL 권한 거부  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `CONNECT SQL` 및 이 사용자가 사용 권한을 부여한 보안 주체에 대해 `Annika` 권한을 거부합니다.  
  
```sql  
USE master;  
DENY CONNECT SQL TO Annika CASCADE;  
GO  
```  
  
### <a name="b-denying-create-endpoint-permission-to-a-sql-server-login-using-the-as-option"></a>B. AS 옵션을 사용하여 SQL Server 로그인에 대해 CREATE ENDPOINT 권한 거부  
 다음 예에서는 사용자 `CREATE ENDPOINT`에 대해 `ArifS` 권한을 거부합니다. 이 예에서는 `AS` 옵션을 사용하여 이를 위해 실행 보안 주체가 권한을 부여할 수 있는 보안 주체로 `MandarP`를 지정합니다.  
  
```sql  
USE master;  
DENY CREATE ENDPOINT TO ArifS AS MandarP;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [DENY 서버 사용 권한 (Transact-SQL)](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [REVOKE 서버 사용 권한 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
