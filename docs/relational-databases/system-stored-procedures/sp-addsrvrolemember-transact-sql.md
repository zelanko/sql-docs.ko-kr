---
title: sp_addsrvrolemember (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
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
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c8159218d405cbd09861938393fd054ab8aea6e9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spaddsrvrolemember-transact-sql"></a>sp_addsrvrolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  고정 서버 역할의 멤버로서 로그인을 추가합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>인수  
 [ @loginame  **=**  ] **'***로그인***'**  
 고정 서버 역할에 추가할 로그인의 이름입니다. *로그인* 은 **sysname**, 기본값은 없습니다. *로그인* 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 로그인 합니다. Windows 로그인에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한이 부여되어 있지 않으면 자동으로 부여됩니다.  
  
 [ @rolename  **=**  ] **'***역할***'**  
 로그인을 추가할 고정 서버 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 NULL 이며 다음 값 중 하나 여야 합니다.  
  
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
  
## <a name="remarks"></a>주의  
 로그인을 고정 서버 역할에 추가하면 이 역할과 연결된 사용 권한을 얻게 됩니다.  
  
 Sa 로그인 및 공용 역할 멤버 자격을 변경할 수 없습니다.  
  
 고정된 데이터베이스 또는 사용자 정의 역할에 구성원을 추가 하려면 sp_addrolemember를 사용 합니다.  
  
 sp_addsrvrolemember는 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 새 멤버를 추가할 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 Windows 로그인을 추가 `Corporate\HelenS` 에 `sysadmin` 고정된 서버 역할입니다.  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [서버 역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
