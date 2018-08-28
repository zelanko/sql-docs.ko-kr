---
title: ALTER SERVER ROLE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8563fae692fbb904b4f1746b9500362c04545fa
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099444"
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

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
  
ADD MEMBER *server_principal*  
서버 역할에 지정한 서버 보안 주체를 추가합니다. *server_principal*은 로그인 또는 사용자 정의 서버 역할일 수 있습니다. *server_principal*은 고정 서버 역할, 데이터베이스 역할 또는 sa가 될 수 없습니다.  
  
DROP MEMBER *server_principal*  
서버 역할에서 지정한 서버 보안 주체를 제거합니다. *server_principal*은 로그인 또는 사용자 정의 서버 역할일 수 있습니다. *server_principal*은 고정 서버 역할, 데이터베이스 역할 또는 sa가 될 수 없습니다.  
  
WITH NAME **=***new_server_role_name*  
사용자 정의 서버 역할의 새로운 이름을 지정합니다. 이 이름은 아직 서버에 없는 이름이어야 합니다.  
  
## <a name="remarks"></a>Remarks  
사용자 정의 서버 역할의 이름을 변경하더라도 역할의 ID 번호, 소유자 또는 사용 권한은 변경되지 않습니다.  
  
역할 멤버쉽을 변경하는 경우 `ALTER SERVER ROLE`은 sp_addsrvrolemember 및 sp_dropsrvrolemember를 대체합니다. 이러한 저장 프로시저는 더 이상 사용되지 않습니다.  
  
`sys.server_role_members` 및 `sys.server_principals` 카탈로그 뷰를 쿼리하여 서버 역할을 볼 수 있습니다.  
  
사용자 정의 서버 역할의 소유자를 변경하려면 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 사용하세요.  
  
## <a name="permissions"></a>Permissions  
사용자 정의 서버 역할의 이름을 변경하려면 서버에 대한 `ALTER ANY SERVER ROLE` 권한이 필요합니다.  
  
**고정 서버 역할**  
  
고정 서버 역할에 멤버를 추가하려면 고정 서버 역할의 멤버이거나 `sysadmin` 고정 서버 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  `CONTROL SERVER` 및 `ALTER ANY SERVER ROLE` 권한은 고정 서버 역할에 대해 `ALTER SERVER ROLE`을 실행하기에는 부족하며 고정 서버 역할에는 `ALTER` 권한을 부여할 수 없습니다.  
  
**사용자 정의 서버 역할**  
  
사용자 정의 서버 역할에 멤버를 추가하려면 `sysadmin` 고정 서버 역할의 멤버이거나 `CONTROL SERVER` 또는 `ALTER ANY SERVER ROLE` 권한이 있어야 합니다. 또는 해당 역할에 대한 `ALTER` 권한이 있어야 합니다.  
  
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
다음 예에서는 `adventure-works\roberto0`이라는 도메인 계정을 `Production`이라는 사용자 정의 서버 역할에 추가합니다.  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>3. 서버 역할에 SQL Server 로그인 추가  
다음 예에서는 `Ted`라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 `diskadmin` 고정 서버 역할에 추가합니다.  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>4. 서버 역할에서 도메인 계정 제거  
다음 예에서는 `adventure-works\roberto0`이라는 도메인 계정을 `Production`이라는 사용자 정의 서버 역할에서 제거합니다.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>5. 서버 역할에서 SQL Server 로그인 제거  
다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `Ted`를 `diskadmin` 고정 서버 역할에서 제거합니다.  
  
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
역할 멤버 자격을 보려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **서버 역할(멤버)** 페이지를 사용하거나 다음 쿼리를 실행합니다.  
  
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
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]   
  
### <a name="h-basic-syntax"></a>8. 기본 구문  
다음 예는 Windows 로그인 `Anna`을 `LargeRC` 서버 역할에 추가합니다.  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>9. 리소스 클래스에서 로그인을 제거합니다.  
다음 예에서는 `LargeRC` 서버 역할에서 안나의 멤버 자격을 삭제합니다.  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>참고 항목  
[CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
