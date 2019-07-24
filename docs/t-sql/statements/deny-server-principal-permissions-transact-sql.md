---
title: DENY Server Principal Permissions(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2fc90354abf3c18a5eba7a92b7a5ffa54a84ce3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984506"
---
# <a name="deny-server-principal-permissions-transact-sql"></a>DENY 서버 보안 주체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 부여된 사용 권한을 거부합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 LOGIN **::** *SQL_Server_login*  
 사용 권한을 거부할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다. 범위 한정자( **::** )가 필요합니다.  
  
 SERVER ROLE **::** *server_role*  
 사용 권한을 거부할 서버 역할을 지정합니다. 범위 한정자( **::** )가 필요합니다.  
  
 TO \<server_principal>  
 사용 권한을 부여할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서버 역할을 지정합니다.  
  
 TO *SQL_Server_login*  
 사용 권한을 거부할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_Windows_login*  
 Windows 로그인에서 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_certificate*  
 인증서로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_AsymKey*  
 비대칭 키에 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *server_role*  
 서버 역할의 이름을 지정합니다.  
  
 CASCADE  
 사용 권한이 거부된 보안 주체에게 사용 권한을 부여 받은 다른 보안 주체의 사용 권한도 거부됨을 나타냅니다.  
  
 AS *SQL_Server_login*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 거부하는 권한을 부여할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 현재 데이터베이스가 master인 경우에만 서버 범위의 사용 권한을 거부할 수 있습니다.  
  
 서버 사용 권한 정보는 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰에 표시됩니다. 서버 보안 주체 정보는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰에 표시됩니다.  
  
 GRANT OPTION을 지정하여 사용 권한이 부여된 보안 주체의 사용 권한을 거부할 경우 CASCADE를 지정하지 않으면 DENY 문이 실패합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 서버 역할은 서버 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서버 역할에 대해 거부할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|SQL Server 로그인 또는 서버 역할 사용 권한|SQL Server 로그인 또는 서버 역할 사용 권한에 포함된 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>사용 권한  
 로그인의 경우 로그인에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
 서버 역할의 경우 서버 역할에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY SERVER ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>1\. 로그인에 IMPERSONATE 권한 거부  
 다음 예에서는 `IMPERSONATE`Windows 사용자 에서 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그인`WanidaBenshoof`에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로그인에 대한 권한을 거부합니다`AdvWorks\YoonM`.  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>2\. CASCADE를 지정하여 VIEW DEFINITION 권한 거부  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `VIEW DEFINITION`에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `EricKurjan`에 대한 `RMeyyappan` 권한을 거부합니다. `CASCADE` 옵션은 `VIEW DEFINITION`에 대한 `EricKurjan` 권한도 `RMeyyappan`이 이 사용 권한을 부여한 보안 주체에 대해 거부됨을 나타냅니다.  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. 서버 역할에 대한 VIEW DEFINITION 권한 거부  
 다음 예에서는 `VIEW DEFINITION` 서버 역할에 대한 `Sales`을 `Auditors` 서버 역할에 대해 거부합니다.  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
