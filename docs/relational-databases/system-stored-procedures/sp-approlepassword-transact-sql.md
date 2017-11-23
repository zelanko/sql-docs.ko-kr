---
title: sp_approlepassword (Transact SQL) | Microsoft Docs
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
- sp_approlepassword
- sp_approlepassword_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_approlepassword
ms.assetid: 7967dc0b-bee2-4c63-b8e9-1c3ce2f5db2a
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 960d3f4d2803d13f04c07a5034077498dc7d0e4e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spapprolepassword-transact-sql"></a>sp_approlepassword (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에 있는 응용 프로그램 역할의 암호를 변경합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [ALTER APPLICATION ROLE](../../t-sql/statements/alter-application-role-transact-sql.md) 대신 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_approlepassword [ @rolename= ] 'role' , [ @newpwd = ] 'password'   
```  
  
## <a name="arguments"></a>인수  
 [  **@rolename =** ] **'***역할***'**  
 응용 프로그램 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 없습니다. *역할* 현재 데이터베이스에 존재 해야 합니다.  
  
 [  **@newpwd =** ] **'***암호***'**  
 응용 프로그램 역할의 새 암호입니다. *암호* 은 **sysname**, 기본값은 없습니다. *암호* NULL 일 수 없습니다.  
  
> [!IMPORTANT]  
>  NULL 암호를 사용하지 마십시오. 강력한 암호를 사용하세요. 자세한 내용은 [Strong Passwords](../../relational-databases/security/strong-passwords.md)을 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_approlepassword** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예는 `PayrollAppRole` 응용 프로그램 역할의 암호를 `B3r12-36`으로 설정합니다.  
  
```  
EXEC sp_approlepassword 'PayrollAppRole', '''B3r12-36';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [응용 프로그램 역할](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_addapprole&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_setapprole&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
