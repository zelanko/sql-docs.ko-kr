---
title: sp_change_users_login (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: b0c847215d31bd2064467c3edbce42ba957c2e78
ms.sourcegitcommit: f7af758b353b53ac3b596d79fd6e32ad7e1e61cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/17/2020
ms.locfileid: "79448335"
---
# <a name="sp_change_users_login-transact-sql"></a>sp_change_users_login(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  기존 데이터베이스 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 매핑합니다. 
  
 > [!IMPORTANT]
 > [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) 를 사용 해야 합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 프로시저로 수행할 동작에 대해 설명합니다. *action* 은 **varchar (10)** 입니다. *작업* 은 다음 값 중 하나를 가질 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Auto_Fix**|현재 데이터베이스의 sys.database_principals 시스템 카탈로그 뷰에 있는 사용자 항목을 동일한 이름의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 연결합니다. 동일한 이름의 로그인이 없으면 자동으로 생성됩니다. **Auto_Fix** 문의 결과를 검토 하 여 올바른 링크가 실제로 생성 되었는지 확인 합니다. 보안이 중요 한 상황에서는 **Auto_Fix** 사용 하지 마십시오.<br /><br /> **Auto_Fix**사용 하는 경우 로그인이 아직 없는 경우 *사용자* 와 *암호* 를 지정 해야 합니다. 그렇지 않으면 *사용자* 를 지정 해야 하지만 *암호* 는 무시 됩니다. *로그인* 은 NULL 이어야 합니다. *사용자* 는 현재 데이터베이스에서 유효한 사용자 여야 합니다. 로그인에는 다른 사용자가 매핑될 수 없습니다.|  
|**Report**|현재 데이터베이스에서 어떠한 로그인에도 연결되지 않은 사용자와 해당 SID(보안 식별자)를 나열합니다. *사용자*, *로그인*및 *암호* 는 NULL 이거나 지정 하지 않아야 합니다.<br /><br /> 시스템 테이블을 사용 하 여 보고서 옵션을 쿼리로 바꾸려면 **sys. server_prinicpals** 의 항목을 **database_principals**의 항목과 비교 합니다.|  
|**Update_One**|현재 데이터베이스의 지정 된 *사용자* 를 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *로그인*에 연결 합니다. *사용자* 및 *로그인* 을 지정 해야 합니다. *암호* 는 NULL 이거나 지정 하지 않아야 합니다.|  
  
 [ @UserNamePattern= ] '*user*'  
 현재 데이터베이스에 있는 사용자의 이름입니다. *사용자* 는 **sysname**이며 기본값은 NULL입니다.  
  
 [ @LoginName= ] '*로그인*'  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. *login* 은 **sysname**이며 기본값은 NULL입니다.  
  
 [ @Password= ] '*암호*'  
 Auto_Fix를 지정 하 여 만든 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 할당 된 암호입니다 **Auto_Fix**. 일치 하는 로그인이 이미 있는 경우 사용자와 로그인이 매핑되고 *암호* 는 무시 됩니다. 일치 하는 로그인이 없으면 sp_change_users_login 새 로그인을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *암호* 를 새 로그인의 암호로 할당 합니다. *password* 는 **sysname**이며 NULL이 아니어야 합니다.  
  
> **중요!!** 항상 [강력한 암호를 사용 하세요.](../../relational-databases/security/strong-passwords.md)
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|UserName|**sysname**|데이터베이스 사용자 이름입니다.|  
|UserSID|**varbinary (85)**|사용자의 보안 식별자입니다.|  
  
## <a name="remarks"></a>설명  
 sp_change_users_login을 사용하여 현재 데이터베이스의 데이터베이스 사용자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 연결할 수 있습니다. 사용자에 대한 로그인이 변경된 경우 sp_change_users_login을 통해 사용자 권한을 그대로 유지한 채 새 로그인에 사용자를 연결할 수 있습니다. 새 *로그인* 은 sa가 될 수 없으며 *사용자* 는 dbo, guest 또는 INFORMATION_SCHEMA 사용자가 될 수 없습니다.  
  
 sp_change_users_login은 데이터베이스 사용자를 Windows 수준 보안 주체, 인증서 또는 비대칭 키에 매핑하는 데 사용할 수 없습니다.  
  
 Windows 보안 주체에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 CREATE USER WITHOUT LOGIN을 사용하여 만든 사용자에 sp_change_users_login을 사용할 수 없습니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_change_users_login을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 db_owner 고정 데이터베이스 역할의 멤버 자격이 필요합니다. Sysadmin 고정 서버 역할의 멤버만 **Auto_Fix** 옵션을 지정할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-showing-a-report-of-the-current-user-to-login-mappings"></a>A. 현재 사용자와 로그인 간의 매핑에 대한 보고서 표시  
 다음 예에서는 현재 데이터베이스의 사용자 및 해당 사용자의 SID(보안 식별자)에 대한 보고서를 생성합니다.  
  
```  
EXEC sp_change_users_login 'Report';  
```  
  
### <a name="b-mapping-a-database-user-to-a-new-sql-server-login"></a>B. 데이터베이스 사용자를 새 SQL Server 로그인에 매핑  
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
  
### <a name="c-automatically-mapping-a-user-to-a-login-creating-a-new-login-if-it-is-required"></a>C. 사용자를 로그인에 자동으로 매핑하고 필요한 경우 새 로그인 만들기  
 다음 예에서는 `Auto_Fix`를 사용하여 기존 사용자를 동일한 이름의 로그인에 매핑하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 없는 경우 암호가 `Mary`인 `B3r12-3x$098f6` 로그인 `Mary`를 만드는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_change_users_login 'Auto_Fix', 'Mary', NULL, 'B3r12-3x$098f6';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Transact-sql&#41;sp_adduser &#40;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [Transact-sql&#41;sp_helplogins &#40;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
