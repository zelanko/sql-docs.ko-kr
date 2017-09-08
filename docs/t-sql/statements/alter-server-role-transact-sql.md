---
title: ALTER SERVER ROLE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f88c9aaf3e541d4213a3adeb77a0e457deb7c06
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

서버 역할의 멤버 자격을 변경하거나 사용자 정의 서버 역할의 이름을 변경합니다. 고정 서버 역할은 이름을 바꿀 수 없습니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>인수  
*server_role_name*  
변경할 서버 역할의 이름입니다.  
  
멤버 추가 *server_principal*  
서버 역할에 지정한 서버 보안 주체를 추가합니다. *server_principal* 은 로그인 또는 사용자 정의 서버 역할 일 수 있습니다. *server_principal* 고정된 서버 역할, 데이터베이스 역할 또는 sa 일 수 없습니다.  
  
DROP MEMBER *server_principal*  
서버 역할에서 지정한 서버 보안 주체를 제거합니다. *server_principal* 은 로그인 또는 사용자 정의 서버 역할 일 수 있습니다. *server_principal* 고정된 서버 역할, 데이터베이스 역할 또는 sa 일 수 없습니다.  
  
이름의  **=**  *new_server_role_name*  
사용자 정의 서버 역할의 새로운 이름을 지정합니다. 이 이름은 아직 서버에 없는 이름이어야 합니다.  
  
## <a name="remarks"></a>주의  
사용자 정의 서버 역할의 이름을 변경하더라도 역할의 ID 번호, 소유자 또는 사용 권한은 변경되지 않습니다.  
  
역할 멤버 자격을 변경 하는 데 `ALTER SERVER ROLE` sp_addsrvrolemember 및 sp_dropsrvrolemember를 대체 합니다. 이러한 저장 프로시저는 더 이상 사용되지 않습니다.  
  
`sys.server_role_members` 및 `sys.server_principals` 카탈로그 뷰를 쿼리하여 서버 역할을 볼 수 있습니다.  
  
사용자 정의 서버 역할의 소유자를 변경 하려면 사용 하 여 [ALTER authorization&#40; Transact SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
필요한 `ALTER ANY SERVER ROLE` 사용자 정의 서버 역할의 이름을 변경 하려면 서버에 대 한 권한이 있습니다.  
  
**고정된 서버 역할**  
  
고정 서버 역할에 멤버를 추가하려면 고정 서버 역할의 멤버이거나 `sysadmin` 고정 서버 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  `CONTROL SERVER` 및 `ALTER ANY SERVER ROLE` 를 실행할 권한이 없는 `ALTER SERVER ROLE` 고정된 서버 역할에 대 한 및 `ALTER` 고정된 서버 역할에 권한을 부여할 수 없습니다.  
  
**사용자 정의 서버 역할**  
  
사용자 정의 서버 역할에 구성원을 추가할의 구성원 이어야는 `sysadmin` 고정 서버 역할 또는 `CONTROL SERVER` 또는 `ALTER ANY SERVER ROLE` 권한. 그렇지 않으면 있어야 `ALTER` 해당 역할에 대 한 권한이 있습니다.  
  
> [!NOTE]  
>  고정 서버 역할과 달리 사용자 정의 서버 역할의 멤버는 기본적으로 동일한 역할에 멤버를 추가할 수 있는 사용 권한이 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-name-of-a-server-role"></a>1. 서버 역할의 이름 변경  
다음 예에서는 `Product`라는 서버 역할을 만든 다음 서버 역할 이름을 `Production`으로 변경합니다.  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>2. 서버 역할에 도메인 계정 추가  
다음 예에서는 라는 도메인 계정을 추가 `adventure-works\roberto0` 사용자 정의 서버 역할에 `Production`합니다.  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>3. 서버 역할에 SQL Server 로그인 추가  
다음 예제에서는 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라는 로그인 `Ted` 에 `diskadmin` 고정된 서버 역할입니다.  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>4. 서버 역할에서 도메인 계정 제거  
다음 예에서는 라는 도메인 계정을 제거 `adventure-works\roberto0` 이라는 사용자 정의 서버 역할에서 `Production`합니다.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>5. 서버 역할에서 SQL Server 로그인 제거  
다음 예제에서는 제거 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `Ted` 에서 `diskadmin` 고정된 서버 역할입니다.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>6. 로그인에 사용 권한을 부여하여 사용자 정의 서버 역할에 로그인 추가  
다음 예에서는 `Ted`가 `Production` 사용자 정의 서버 역할에 다른 로그인을 추가할 수 있도록 허용합니다.  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>7. 역할 멤버 자격 보기  
역할 멤버 자격을 보려면 사용 하 여는 **서버 역할 (멤버)** 페이지에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 하거나 다음 쿼리를 실행 합니다.  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>8. 기본 구문  
다음 예제에서는 추가 로그인 `Anna` 에 `LargeRC` 서버 역할입니다.  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>9. 리소스 클래스에서 로그인을 제거 합니다.  
다음 예제에서는의 Anna의 멤버 자격 삭제는 `LargeRC` 서버 역할입니다.  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>관련 항목:  
[서버 역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER role&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP role&#40; Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.server_role_members&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  

