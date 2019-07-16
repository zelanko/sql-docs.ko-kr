---
title: sp_change_users_login (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_users_login
- sp_change_users_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_users_login
ms.assetid: 1554b39f-274b-4ef8-898e-9e246b474333
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0594066f044288757e5e31f8e078fabb4c2f3775
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120226"
---
# <a name="spchangeuserslogin-transact-sql"></a>sp_change_users_login(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  기존 데이터베이스 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑합니다. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) 대신 합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_change_users_login [ @Action = ] 'action'   
    [ , [ @UserNamePattern = ] 'user' ]   
    [ , [ @LoginName = ] 'login' ]   
    [ , [ @Password = ] 'password' ]  
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @Action= ] '*action*'  
 프로시저로 수행할 동작에 대해 설명합니다. *동작* 됩니다 **varchar(10)** 합니다. *작업* 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**Auto_Fix**|현재 데이터베이스의 sys.database_principals 시스템 카탈로그 뷰에 있는 사용자 항목을 동일한 이름의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 연결합니다. 동일한 이름의 로그인이 없으면 자동으로 생성됩니다. 결과를 조사 합니다 **Auto_Fix** 문을 올바른 링크가 실제로 생성 되었는지 확인 합니다. 사용 하지 마세요 **Auto_Fix** 보안과 관련 된 경우에서.<br /><br /> 사용 하는 경우 **Auto_Fix**를 지정 해야 *사용자* 하 고 *암호* 로그인 아직 없는 경우 지정 해야 *사용자*있지만 *암호* 무시 됩니다. *로그인* NULL 이어야 합니다. *사용자* 현재 데이터베이스에서 유효한 사용자 여야 합니다. 로그인에는 다른 사용자가 매핑될 수 없습니다.|  
|**보고서**|현재 데이터베이스에서 어떠한 로그인에도 연결되지 않은 사용자와 해당 SID(보안 식별자)를 나열합니다. *사용자*, *로그인*, 및 *암호* NULL 이거나 지정 되지 않았습니다.<br /><br /> 시스템 테이블을 사용 하 여 쿼리를 사용 하 여 보고서 옵션을 바꾸려면의 항목과 비교 **sys.server_prinicpals** 의 항목과 **sys.database_principals**합니다.|  
|**Update_One**|지정 된 링크 *사용자* 현재 기존 데이터베이스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *로그인*합니다. *사용자* 하 고 *로그인* 지정 해야 합니다. *암호* NULL 이거나 지정 되지 않았습니다.|  
  
 [ @UserNamePattern= ] '*user*'  
 현재 데이터베이스에 있는 사용자의 이름입니다. *사용자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ @LoginName= ] '*login*'  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. *login*은 **sysname**이며 기본값은 NULL입니다.  
  
 [ @Password= ] '*password*'  
 새 할당 된 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 지정 하 여 만들어지는 **Auto_Fix**합니다. 사용자와 로그인이 매핑되고 있으면 일치 하는 로그인 하 고 *암호* 무시 됩니다. 일치 하는 로그인이 없으면 sp_change_users_login를 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 할당 *암호* 새 로그인에 대 한 합니다. *암호* 됩니다 **sysname**, NULL이 아니어야 합니다.  
  
> **중요!!** 항상 사용을 [강력한 암호!](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|데이터베이스 사용자 이름입니다.|  
|UserSID|**varbinary(85)**|사용자의 보안 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 sp_change_users_login을 사용하여 현재 데이터베이스의 데이터베이스 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 연결할 수 있습니다. 사용자에 대한 로그인이 변경된 경우 sp_change_users_login을 통해 사용자 권한을 그대로 유지한 채 새 로그인에 사용자를 연결할 수 있습니다. 새 *로그인* sa가 될 수 없습니다 하며 *사용자*dbo, guest 또는 INFORMATION_SCHEMA 사용자 일 수 없습니다.  
  
 sp_change_users_login은 데이터베이스 사용자를 Windows 수준 보안 주체, 인증서 또는 비대칭 키에 매핑하는 데 사용할 수 없습니다.  
  
 Windows 보안 주체에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 CREATE USER WITHOUT LOGIN을 사용하여 만든 사용자에 sp_change_users_login을 사용할 수 없습니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_change_users_login을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다. Sysadmin 고정된 서버 역할의 멤버만 지정할 수는 **Auto_Fix** 옵션입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 현재 사용자와 로그인 간의 매핑에 대한 보고서 표시  
 다음 예에서는 현재 데이터베이스의 사용자 및 해당 사용자의 SID(보안 식별자)에 대한 보고서를 생성합니다.  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>2\. 데이터베이스 사용자를 새 SQL Server 로그인에 매핑  
 다음 예에서는 데이터베이스 사용자가 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 연결됩니다. 데이터베이스 사용자 `MB-Sales`는 처음에 다른 로그인에 매핑되어 있다가 `MaryB` 로그인에 다시 매핑됩니다.  
  
```  
--Create the new login.  
CREATE LOGIN MaryB WITH PASSWORD = '982734snfdHHkjj3';  
GO  
--Map database user MB-Sales to login MaryB.  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Update_One', 'MB-Sales', 'MaryB';  
GO  
```  
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>3\. 사용자를 로그인에 자동으로 매핑하고 필요한 경우 새 로그인 만들기  
 다음 예에서는 `Auto_Fix`를 사용하여 기존 사용자를 동일한 이름의 로그인에 매핑하거나 `Mary` 로그인이 없는 경우 암호가 `B3r12-3x$098f6`인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 `Mary`를 만드는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_helplogins &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
