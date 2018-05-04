---
title: sp_addlogin (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3120366e65e33341dfb4ab17e9e2c5436a47d4c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있도록 하는 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 대신 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
 [ @loginame=] '*로그인*'  
 로그인 이름입니다. *로그인* 은 **sysname**, 기본값은 없습니다.  
  
 [ @passwd=] '*암호*'  
 로그인 암호입니다. *암호* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*데이터베이스*'  
 로그인의 기본 데이터베이스(로그인한 다음 처음 연결되는 데이터베이스)입니다. *데이터베이스* 은 **sysname**, 기본값은 **마스터**합니다.  
  
 [ @deflanguage=] '*언어*'  
 로그인의 기본 언어입니다. *언어* 은 **sysname**, 기본값은 NULL입니다. 경우 *언어* 를 지정 하지 않으면 기본 *언어* 새 로그인의 서버의 현재 기본 언어로 설정 합니다.  
  
 [ @sid=] '*sid*'  
 로그인의 SID(보안 ID)입니다. *sid* 은 **varbinary (16)**, 기본값은 NULL입니다. 경우 *sid* 가 NULL 인 시스템에서 새 로그인에 대 한 SID를 생성 합니다. 이 사용 되지만 **varbinary** 데이터 형식, NULL이 아닌 값 정확히 16 바이트 길이가 하며 이미 존재 하지 않아야 합니다. 지정 *sid* 유용, 예를 들어 스크립팅 또는 이동할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 다른 서버 간에 로그인 하려면 서로 다른 서버에 동일한 SID를 로그인 합니다.  
  
 [ @encryptopt=] '*encryption_option*'  
 암호를 일반 텍스트로 전달할지 아니면 일반 텍스트 암호의 해시로 전달할지 지정합니다. 암호화되지는 않습니다. 이 설명에서 "암호화"라는 단어는 이전 버전과의 호환성을 위해 사용합니다. 일반 텍스트 암호가 전달되면 전달된 암호는 해시됩니다. 해시된 암호는 저장됩니다. *encryption_option* 은 **varchar (20)**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|NULL|암호를 일반 텍스트로 전달합니다. 기본값입니다.|  
|**skip_encryption**|암호가 이미 해시되어 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 다시 해시하지 않고 값을 저장합니다.|  
|**skip_encryption_old**|제공된 암호가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 해시되었습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 다시 해시하지 않고 값을 저장합니다. 이 옵션은 업그레이드 목적으로만 제공됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 문자, 기호 및 숫자를 포함하여 1자에서 128자까지의 문자를 포함할 수 있습니다. 로그인은 백슬래시를 포함할 수 없습니다 (\\); sa, public, 예약 된 로그인 이름으로 이미 존재 또는 NULL 또는 빈 문자열일 수 (`''`).  
  
 기본 데이터베이스의 이름이 제공되는 경우에는 USE 문을 실행하지 않고도 지정된 데이터베이스에 연결할 수 있습니다. 그러나 데이터베이스 소유자가 해당 데이터베이스에 액세스 부여 될 때까지 기본 데이터베이스를 사용할 수 없습니다 (사용 하 여 [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) 또는 [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) 또는 [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 SID는 서버에서 로그인을 고유하게 식별하는 GUID입니다.  
  
 서버의 기본 언어를 변경해도 기존 로그인의 기본 언어는 변경되지 않습니다. 서버의 기본 언어를 변경 하려면 사용 하 여 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
 사용 하 여 **skip_encryption** 암호를 표시 하지 않으려면 해시는 로그인에 추가 되는 암호가 이미 해시 하는 경우에 유용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이전 버전의에서 암호 해시 된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용 하 여 **skip_encryption_old**합니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_addlogin을 실행할 수 없습니다.  
  
 다음 표에서는 sp_addlogin과 함께 사용하는 몇 가지 저장 프로시저를 보여 줍니다.  
  
|저장 프로시저|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Windows 사용자 또는 그룹을 추가합니다.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|사용자의 암호를 변경합니다.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|사용자의 기본 데이터베이스를 변경합니다.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|사용자의 기본 언어를 변경합니다.|  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-sql-server-login"></a>1. SQL Server 로그인 만들기  
 다음 예에서는 `Victoria`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B1r12-36`이며 기본 데이터베이스는 지정하지 않습니다.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>2. 기본 데이터베이스가 있는 SQL Server 로그인 만들기  
 다음 예에서는 `Albert`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B5432-3M6`이며 기본 데이터베이스는 `corporate`입니다.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>3. 기본 언어가 다른 SQL Server 로그인 만들기  
 다음 예에서는 `TzTodorov`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `709hLKH7chjfwv`이고 기본 데이터베이스는 `AdventureWorks2012`이며 기본 언어는 `Bulgarian`입니다.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>4. 특정 SID를 가진 SQL Server 로그인 만들기  
 다음 예에서는 `Michael`이라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B548bmM%f6`이고 기본 데이터베이스는 `AdventureWorks2012`이며 기본 언어는 `us_english`입니다. 그리고 SID는 `0x0123456789ABCDEF0123456789ABCDEF`입니다.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
