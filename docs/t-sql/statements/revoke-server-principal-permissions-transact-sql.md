---
title: REVOKE 서버 보안 주체 사용 권한
description: SQL Server 로그인의 사용 권한을 철회합니다.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, impersonation
- permissions [SQL Server], impersonation
- permissions [SQL Server], logins
- impersonate [SQL Server], revoking
- logins [SQL Server], revoking
- REVOKE statement, logins
ms.assetid: 75409024-f150-4326-af16-9d60e900df18
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 03dc120975d50edb743911b3c9973b94a15b3ceb
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485361"
---
# <a name="revoke-server-principal-permissions-transact-sql"></a>REVOKE 서버 보안 주체 사용 권한(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 부여되거나 거부된 사용 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey     
    | server_role  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *permission*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 취소할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 LOGIN **::** *SQL_Server_login*  
 사용 권한을 취소할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다. 범위 한정자( **::** )가 필요합니다.  
  
 SERVER ROLE **::** *server_role*  
 사용 권한을 취소할 서버 역할을 지정합니다. 범위 한정자( **::** )가 필요합니다.  
  
 { FROM | TO } \<server_principal> 사용 권한을 취소할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서버 역할을 지정합니다.  
  
 *SQL_Server_login*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_Windows_login*  
 Windows 로그인에서 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_certificate*  
 인증서로 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *SQL_Server_login_from_AsymKey*  
 비대칭 키에 매핑된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름을 지정합니다.  
  
 *server_role*  
 사용자 정의 서버 역할의 이름을 지정합니다.  
  
 GRANT OPTION  
 지정한 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한이 취소됨을 나타냅니다. 사용 권한 자체는 취소되지 않습니다.  
  
> [!IMPORTANT]  
>  보안 주체에 GRANT 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
 CASCADE  
 사용 권한이 취소된 보안 주체에게 사용 권한을 부여 받거나 거부당한 다른 보안 주체의 사용 권한도 취소됨을 나타냅니다.  
  
> [!CAUTION]  
>  WITH GRANT OPTION을 부여 받은 사용 권한이 연계되어 취소되면 해당 사용 권한의 GRANT 및 DENY가 모두 취소됩니다.  
  
 AS *SQL_Server_login*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 취소하는 권한을 부여할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 서버 역할은 서버 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서버 역할에 대해 취소할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|SQL Server 로그인 또는 서버 역할 사용 권한|SQL Server 로그인 또는 서버 역할 사용 권한에 포함된 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>사용 권한  
 로그인의 경우 로그인에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
 서버 역할의 경우 서버 역할에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY SERVER ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-revoking-impersonate-permission-on-a-login"></a>A. 로그인에 대한 IMPERSONATE 권한 취소  
 다음 예에서는 사용자 `AdvWorks\YoonM`에서 생성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `WanidaBenshoof`에 대한 `IMPERSONATE` 권한을 취소합니다.  
  
```  
USE master;  
REVOKE IMPERSONATE ON LOGIN::WanidaBenshoof FROM [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-with-cascade"></a>B. CASCADE를 지정하여 VIEW DEFINITION 권한 취소  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `VIEW DEFINITION`으로부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `EricKurjan`에 대한 `RMeyyappan` 권한을 취소합니다. `CASCADE` 옵션은 `VIEW DEFINITION`에 대한 `EricKurjan` 권한도 `RMeyyappan`이 이 사용 권한을 부여한 보안 주체로부터 취소됨을 나타냅니다.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON LOGIN::EricKurjan FROM RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-revoking-view-definition-permission-on-a-server-role"></a>C. 서버 역할에 대한 VIEW DEFINITION 권한 취소  
 다음 예에서는 `VIEW DEFINITION` 서버 역할에 대한 `Sales`을 `Auditors` 서버 역할에서 취소합니다.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [DENY 서버 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

