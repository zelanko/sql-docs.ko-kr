---
title: sp_password (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_password
- sp_password_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_password
ms.assetid: 0ecbec81-e637-44a9-a61e-11bf060ef084
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b461f601e94756d1406da13f1da99f8b1df50198
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sppassword-transact-sql"></a>sp_password(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  추가 하거나 변경에 대 한 암호는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_password [ [ @old = ] 'old_password' , ]  
     { [ @new =] 'new_password' }  
     [ , [ @loginame = ] 'login' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@old=** ] **'***old_password***'**  
 이전 암호입니다. *old_password* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@new=** ] **'***new_password***'**  
 새 암호입니다. *new_password* 은 **sysname**, 기본값은 없습니다. *old_password* 명명 된 매개 변수를 사용 하지 지정 해야 합니다.  
  
> [!IMPORTANT]  
>  NULL 암호를 사용하지 마십시오. 강력한 암호를 사용하세요. 자세한 내용은 [Strong Passwords](../../relational-databases/security/strong-passwords.md)을 참조하세요.  
  
 [  **@loginame=** ] **'***로그인***'**  
 암호 변경의 영향을 받는 로그인의 이름입니다. *로그인* 은 **sysname**, 기본값은 NULL입니다. *로그인* 이미 존재 해야 하며의 멤버만 지정할 수는 **sysadmin** 또는 **securityadmin** 고정 서버 역할입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_password** ALTER LOGIN을 호출 합니다. 이 문에서는 추가 옵션을 지정할 수 있습니다. 암호를 변경 하는 방법에 대 한 정보를 참조 하세요. [ALTER login&#40; Transact SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_password** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 ALTER ANY LOGIN 권한이 필요합니다. 이전 암호를 제공하지 않고 암호를 다시 설정하려는 경우나 변경되고 있는 로그인에 CONTROL SERVER 권한이 있는 경우에는 CONTROL SERVER 권한도 필요합니다.  
  
 보안 주체는 자신의 암호를 변경할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-changing-the-password-of-a-login-without-knowing-the-old-password"></a>1. 이전 암호를 모른 채 로그인의 암호 변경  
 다음 예에서는 `ALTER LOGIN`을 사용하여 `Victoria` 로그인의 암호를 `B3r1000d#2-36`으로 변경하는 방법을 보여 줍니다. 이것은 기본적으로 사용되는 방법입니다. 이 명령을 실행하고 있는 사용자는 CONTROL SERVER 권한을 가져야 합니다.  
  
```  
ALTER LOGIN Victoria WITH PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
### <a name="b-changing-a-password"></a>2. 암호 변경  
 다음 예에서는 `ALTER LOGIN`을 사용하여 `Victoria` 로그인의 암호를 `B3r1000d#2-36`에서 `V1cteAmanti55imE`로 변경하는 방법을 보여 줍니다. 이것은 기본적으로 사용되는 방법입니다. `Victoria` 사용자는 추가 사용 권한 없이도 이 명령을 실행할 수 있습니다. 다른 사용자는 ALTER ANY LOGIN 권한을 가져야 합니다.  
  
```  
ALTER LOGIN Victoria WITH   
     PASSWORD = 'V1cteAmanti55imE'   
     OLD_PASSWORD = 'B3r1000d#2-36';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_addlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
