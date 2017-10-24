---
title: "GRANT 서버 보안 주체 사용 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- impersonate [SQL Server], granting
- granting permissions [SQL Server], logins
- permissions [SQL Server], impersonate
- permissions [SQL Server], logins
- GRANT statement, impersonation
- GRANT statement, logins
- logins [SQL Server], granting access
- granting permissions [SQL Server], impersonation
ms.assetid: 4cbed281-5e1e-4d8b-b410-4c18a6cd0205
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee77fb0aa9ddcb274b1ac3ff88690d9675d2d192
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="grant-server-principal-permissions-transact-sql"></a>GRANT 서버 보안 주체 사용 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대한 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>인수  
 *사용 권한*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 부여할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 로그인 **::** *SQL_Server_login*  
 사용 권한을 부여할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다. 범위 한정자 (**::**)가 필요 합니다.  
  
 서버 역할 **::** *server_role*  
 사용 권한을 부여할 사용자 정의 서버 역할을 지정합니다. 범위 한정자 (**::**)가 필요 합니다.  
  
 \<server_principal > 지정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 권한이 부여 되 고 있는 로그인 또는 서버 역할입니다.  
  
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
  
 WITH GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 AS *SQL_Server_login*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정합니다.  
  
## <a name="remarks"></a>주의  
 현재 데이터베이스가 master인 경우에만 서버 범위의 사용 권한을 부여할 수 있습니다.  
  
 서버 사용 권한에 대 한 정보는 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰에 있습니다. 서버 보안 주체에 대 한 정보에 표시 되는 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰에 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 서버 역할은 서버 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 서버 역할에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|SQL Server 로그인 또는 서버 역할 사용 권한|SQL Server 로그인 또는 서버 역할 사용 권한에 포함된 사용 권한|서버 사용 권한에 포함된 사용 권한|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissions  
 로그인의 경우 로그인에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
 서버 역할의 경우 서버 역할에 대한 CONTROL 권한 또는 서버에 대한 ALTER ANY SERVER ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-impersonate-permission-on-a-login"></a>1. 로그인에 IMPERSONATE 권한 부여  
 다음 예제에서는 부여 `IMPERSONATE` 에 대 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `WanidaBenshoof` 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 사용자에서 만든 로그인 `AdvWorks\YoonM`합니다.  
  
```  
USE master;  
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-granting-view-definition-permission-with-grant-option"></a>2. GRANT OPTION을 지정하여 VIEW DEFINITION 권한 부여  
 다음 예에서는 `VIEW DEFINITION`으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `EricKurjan`에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `RMeyyappan`에 대한 `GRANT OPTION`을 부여합니다.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    WITH GRANT OPTION;  
GO   
```  
  
### <a name="c-granting-view-definition-permission-on-a-server-role"></a>3. 서버 역할에 대한 VIEW DEFINITION 권한 부여  
 다음 예에서는 `VIEW DEFINITION` 서버 역할에 대한 `Sales`을 `Auditors` 서버 역할에 부여합니다.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  


