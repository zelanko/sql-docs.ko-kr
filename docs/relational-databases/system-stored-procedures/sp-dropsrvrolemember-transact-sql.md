---
title: sp_dropsrvrolemember (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 2624ed4800a247b0847adc5839346758aa50f140
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67463569"
---
# <a name="sp_dropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember(Transact-SQL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

고정 서버 역할에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이나 Windows 사용자 또는 그룹을 제거합니다.

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 을 사용 하십시오.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>인수

**[ @loginame = ]** '_로그인_'  
고정 서버 역할에서 제거할 로그인의 이름입니다. *login* 은 **sysname**이며 기본값은 없습니다. *로그인* 이 있어야 합니다.  

**[ @rolename = ]** '_role_'  
서버 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. *role* 은 다음 값 중 하나 여야 합니다.  

-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 고정 서버 역할에서 로그인을 제거하는데 사용할 수 있는 것은 sp_dropsrvrolemember뿐입니다. 데이터베이스 역할에서 멤버를 제거하려면 sp_droprolemember를 사용하십시오.  
  
 어떠한 고정 서버 역할에서도 sa 로그인을 제거할 수 없습니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_dropsrvrolemember를 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할의 멤버 자격 또는 서버에 대한 ALTER ANY LOGIN 권한 및 멤버를 삭제할 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예는 `JackO` 고정 서버 역할에서 `sysadmin` 로그인을 제거합니다.  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;서버 역할 만들기](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-sql&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addsrvrolemember &#40;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_droprolemember &#40;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
