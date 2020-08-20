---
description: sp_password(Transact-SQL)
title: sp_password (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0675634050234b00cadccf63c0f44295a21e56a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481106"
---
# <a name="sp_password-transact-sql"></a>sp_password(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  로그인에 대 한 암호를 추가 하거나 변경 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 을 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @old = ] 'old_password'` 이전 암호입니다. *old_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @new = ] 'new_password'` 새 암호입니다. *new_password* 는 **sysname**이며 기본값은 없습니다. 명명 된 매개 변수가 사용 되지 않는 경우 *old_password* 를 지정 해야 합니다.  
  
> [!IMPORTANT]  
>  NULL 암호를 사용하지 마십시오. 강력한 암호를 사용하세요. 자세한 내용은 [Strong Passwords](../../relational-databases/security/strong-passwords.md)을 참조하세요.  
  
`[ @loginame = ] 'login'` 암호 변경의 영향을 받는 로그인의 이름입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *login* 은 이미 존재 해야 하며 **sysadmin** 또는 **securityadmin** 고정 서버 역할의 멤버만 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_password** 는 ALTER LOGIN을 호출 합니다. 이 문에서는 추가 옵션을 지정할 수 있습니다. 암호 변경에 대 한 자세한 내용은 [ALTER LOGIN &#40;transact-sql&#41;](../../t-sql/statements/alter-login-transact-sql.md)를 참조 하세요.  
  
 사용자 정의 트랜잭션 내에서는 **sp_password** 을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY LOGIN 권한이 필요합니다. 이전 암호를 제공하지 않고 암호를 다시 설정하려는 경우나 변경되고 있는 로그인에 CONTROL SERVER 권한이 있는 경우에는 CONTROL SERVER 권한도 필요합니다.  
  
 보안 주체는 자신의 암호를 변경할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>A. 이전 암호를 모른 채 로그인의 암호 변경  
 다음 예에서는 `ALTER LOGIN`을 사용하여 `Victoria` 로그인의 암호를 `B3r1000d#2-36`으로 변경하는 방법을 보여 줍니다. 이는 선호되는 방법입니다. 이 명령을 실행하고 있는 사용자는 CONTROL SERVER 권한을 가져야 합니다.  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>B. 암호 변경  
 다음 예에서는 `ALTER LOGIN`을 사용하여 `Victoria` 로그인의 암호를 `B3r1000d#2-36`에서 `V1cteAmanti55imE`로 변경하는 방법을 보여 줍니다. 이는 선호되는 방법입니다. `Victoria` 사용자는 추가 사용 권한 없이도 이 명령을 실행할 수 있습니다. 다른 사용자는 ALTER ANY LOGIN 권한을 가져야 합니다.  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;sp_revokelogin &#40;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
