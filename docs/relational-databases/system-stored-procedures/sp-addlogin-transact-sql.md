---
title: sp_addlogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5868120af1e98c4b2f3be78f2cf7927df53b42d1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68072659"
---
# <a name="sp_addlogin-transact-sql"></a>sp_addlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있도록 하는 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 을 사용 해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @loginame= ] '*로그인*'  
 로그인 이름입니다. *login* 은 **sysname**이며 기본값은 없습니다.  
  
 [ @passwd= ] '*암호*'  
 로그인 암호입니다. *password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb= ] '*데이터베이스*'  
 로그인의 기본 데이터베이스(로그인한 다음 처음 연결되는 데이터베이스)입니다. *데이터베이스* 는 **sysname**이며 기본값은 **master**입니다.  
  
 [ @deflanguage= ] '*언어*'  
 로그인의 기본 언어입니다. *language* 는 **sysname**이며 기본값은 NULL입니다. *Language* 를 지정 하지 않으면 새 로그인의 기본 *언어가* 서버의 현재 기본 언어로 설정 됩니다.  
  
 [ @sid= ] '*sid*'  
 로그인의 SID(보안 ID)입니다. *sid* 는 **varbinary (16)** 이며 기본값은 NULL입니다. *Sid* 가 NULL 인 경우 시스템은 새 로그인에 대 한 sid를 생성 합니다. **Varbinary** 데이터 형식을 사용 하는 경우에도 NULL이 아닌 값은 정확히 16 바이트 여야 하며, 아직 존재 하지 않아야 합니다. 예 *sid* 를 들어, 서버 간에 로그인을 스크립팅 하거나 이동 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 경우와 로그인이 다른 서버에서 동일한 sid를 갖도록 하려면 sid를 지정 하는 것이 유용 합니다.  
  
 [ @encryptopt= ] '*encryption_option*'  
 암호를 일반 텍스트로 전달할지 아니면 일반 텍스트 암호의 해시로 전달할지 지정합니다. 암호화되지는 않습니다. 이 설명에서 "암호화"라는 단어는 이전 버전과의 호환성을 위해 사용합니다. 일반 텍스트 암호가 전달되면 전달된 암호는 해시됩니다. 해시된 암호는 저장됩니다. *encryption_option* 는 **varchar (20)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|NULL|암호를 일반 텍스트로 전달합니다. 이것이 기본값입니다.|  
|**skip_encryption**|암호가 이미 해시되어 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 다시 해시하지 않고 값을 저장합니다.|  
|**skip_encryption_old**|제공된 암호가 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 해시되었습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 다시 해시하지 않고 값을 저장합니다. 이 옵션은 업그레이드 목적으로만 제공됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 문자, 기호 및 숫자를 포함하여 1자에서 128자까지의 문자를 포함할 수 있습니다. 로그인에는 백슬래시 (\\)를 사용할 수 없습니다. sa 또는 public과 같은 예약 된 로그인 이름 이거나 이미 존재 합니다. 또는가 NULL 이거나 빈 문자열 (`''`) 인 경우  
  
 기본 데이터베이스의 이름이 제공되는 경우에는 USE 문을 실행하지 않고도 지정된 데이터베이스에 연결할 수 있습니다. 그러나 데이터베이스 소유자가 [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) 또는 [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) 또는 [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)를 사용 하 여 해당 데이터베이스에 대 한 액세스 권한을 부여할 때까지 기본 데이터베이스를 사용할 수 없습니다.  
  
 SID는 서버에서 로그인을 고유하게 식별하는 GUID입니다.  
  
 서버의 기본 언어를 변경해도 기존 로그인의 기본 언어는 변경되지 않습니다. 서버의 기본 언어를 변경 하려면 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)을 사용 합니다.  
  
 암호 해시를 표시 하지 않기 위해 **skip_encryption** 를 사용 하는 것은 로그인이에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]추가 될 때 암호가 이미 해시 된 경우에 유용 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 암호를 해시 한 경우 **skip_encryption_old**를 사용 합니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_addlogin을 실행할 수 없습니다.  
  
 다음 표에서는 sp_addlogin과 함께 사용하는 몇 가지 저장 프로시저를 보여 줍니다.  
  
|저장 프로시저|설명|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Windows 사용자 또는 그룹을 추가합니다.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|사용자의 암호를 변경합니다.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|사용자의 기본 데이터베이스를 변경합니다.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|사용자의 기본 언어를 변경합니다.|  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-sql-server-login"></a>A. SQL Server 로그인 만들기  
 다음 예에서는 `Victoria`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B1r12-36`이며 기본 데이터베이스는 지정하지 않습니다.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 기본 데이터베이스가 있는 SQL Server 로그인 만들기  
 다음 예에서는 `Albert`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B5432-3M6`이며 기본 데이터베이스는 `corporate`입니다.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 기본 언어가 다른 SQL Server 로그인 만들기  
 다음 예에서는 `TzTodorov`라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `709hLKH7chjfwv`이고 기본 데이터베이스는 `AdventureWorks2012`이며 기본 언어는 `Bulgarian`입니다.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 특정 SID를 가진 SQL Server 로그인 만들기  
 다음 예에서는 `Michael`이라는 사용자에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다. 암호는 `B548bmM%f6`이고 기본 데이터베이스는 `AdventureWorks2012`이며 기본 언어는 `us_english`입니다. 그리고 SID는 `0x0123456789ABCDEF0123456789ABCDEF`입니다.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;로그인 &#40;만들기](../../t-sql/statements/create-login-transact-sql.md)   
 [Transact-sql&#41;sp_droplogin &#40;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [Transact-sql&#41;sp_helpuser &#40;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Transact-sql&#41;sp_revokelogin &#40;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Transact-sql&#41;xp_logininfo &#40;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
