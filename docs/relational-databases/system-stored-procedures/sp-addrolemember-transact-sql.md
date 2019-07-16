---
title: sp_addrolemember (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrolemember_TSQL
- sp_addrolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrolemember
ms.assetid: a583c087-bdb3-46d2-b9e5-3921b3e6d10b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9e0d3152c6d60faff4c1c42410374287bd7d111
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030909"
---
# <a name="spaddrolemember-transact-sql"></a>sp_addrolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 데이터베이스의 데이터베이스 역할에 데이터베이스 사용자, 데이터베이스 역할, Windows 로그인 또는 Windows 그룹을 추가합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
sp_addrolemember [ @rolename = ] 'role', [ @membername = ] 'security_account'  

```    
  
## <a name="arguments"></a>인수  
 [ @rolename= ] '*role*'  
 현재 데이터베이스에 있는 데이터베이스 역할의 이름입니다. *역할* 되는 **sysname**, 기본값은 없습니다.  
  
 [ @membername= ] '*security_account*'  
 역할에 추가될 보안 계정입니다. *security_account* 되는 **sysname**, 기본값은 없습니다. *security_account* 데이터베이스 사용자, 데이터베이스 역할, Windows 로그인 또는 Windows 그룹 일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 sp_addrolemember를 사용하여 역할에 추가된 멤버는 해당 역할의 사용 권한을 상속합니다. 새 멤버가 해당 데이터베이스 사용자가 없는 Windows 수준의 보안 주체인 경우에는 데이터베이스 사용자가 생성되지만 로그인에 완전히 매핑되지 않을 수 있습니다. 로그인이 있고 데이터베이스에 액세스할 수 있는지 항상 확인하세요.  
  
 역할은 자신의 역할 자체를 멤버로 포함할 수 없습니다. 이와 같은 "순환" 정의는 하나 이상의 중간 멤버 자격을 통해 멤버 자격이 간접적으로 유추되는 경우에도 유효하지 않습니다.  
  
 sp_addrolemember는 역할에 고정된 데이터베이스 역할, 고정된 서버 역할 또는 dbo를 추가할 수 없습니다.
  
 데이터베이스 역할에 멤버를 추가할 경우에만 sp_addrolemember를 사용하십시오. 사용 하 여 서버 역할에 구성원을 추가할 [sp_addsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버를 유연한 데이터베이스 역할에 추가하려면 다음 항목 중 하나가 필요합니다.  
  
-   Db_owner 또는 db_securityadmin 고정된 데이터베이스 역할의 멤버 자격.  
  
-   역할을 소유하는 역할의 멤버 자격  
  
-   **ALTER ANY ROLE** 권한 또는 **ALTER** 역할에 대 한 권한이 있습니다.  
  
 고정 데이터베이스 역할에 멤버를 추가하려면 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-adding-a-windows-login"></a>A. Windows 로그인 추가  
 다음 예제에서는 Windows 로그인에 추가 `Contoso\Mary5` 에 `AdventureWorks2012` 사용자로 데이터베이스 `Mary5`합니다. 그런 다음 `Mary5` 사용자를 `Production` 역할에 추가합니다.  
  
> [!NOTE]  
>  `Contoso\Mary5`는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Mary5` 데이터베이스 사용자로 알려져 있기 때문에 `Mary5` 사용자 이름을 지정해야 합니다. `Contoso\Mary5`라는 로그인이 없으면 문이 실패합니다. 사용자 도메인의 로그인을 사용하여 테스트하세요.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER Mary5 FOR LOGIN [Contoso\Mary5] ;  
GO  
```  
  
### <a name="b-adding-a-database-user"></a>2\. 데이터베이스 사용자 추가  
 다음 예에서는 `Mary5` 데이터베이스 사용자를 현재 데이터베이스의 `Production` 데이터베이스 역할에 추가합니다.  
  
```  
EXEC sp_addrolemember 'Production', 'Mary5';  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-adding-a-windows-login"></a>3\. Windows 로그인 추가  
 다음 예에서는 로그인에 추가 합니다 `LoginMary` 에 `AdventureWorks2008R2` 사용자로 데이터베이스 `UserMary`합니다. 그런 다음 `UserMary` 사용자를 `Production` 역할에 추가합니다.  
  
> [!NOTE]  
>  때문에 로그인 `LoginMary` 데이터베이스 사용자로 알려져 `UserMary` 에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 사용자 이름을 `UserMary` 지정 해야 합니다. `Mary5`라는 로그인이 없으면 문이 실패합니다. 로그인 및 사용자 이름이 있습니다. 이 예제에서는 사용자 및 로그인에 영향을 주는 작업을 구분 하기 위해 다른 이름을 사용 합니다.  
  
```  
-- Uses AdventureWorks  
  
CREATE USER UserMary FOR LOGIN LoginMary ;  
GO  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
### <a name="d-adding-a-database-user"></a>4\. 데이터베이스 사용자 추가  
 다음 예에서는 `UserMary` 데이터베이스 사용자를 현재 데이터베이스의 `Production` 데이터베이스 역할에 추가합니다.  
  
```  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_grantdbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
