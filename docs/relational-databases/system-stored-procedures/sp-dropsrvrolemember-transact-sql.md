---
title: sp_dropsrvrolemember (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc66cffd56d8eebf31f50ce784be407292261b89
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  고정 서버 역할에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이나 Windows 사용자 또는 그룹을 제거합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]사용 하 여 [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) 대신 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>인수  
 [ @loginame  **=**  ] **'***로그인***'**  
 고정 서버 역할에서 제거할 로그인의 이름입니다. *로그인* 은 **sysname**, 기본값은 없습니다. *로그인* 존재 해야 합니다.  
  
 [ @rolename  **=**  ] **'***역할***'**  
 서버 역할의 이름입니다. *역할* 은 **sysname**, 기본값은 NULL입니다. *역할* 다음 값 중 하나 여야 합니다.  
  
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
 Sp_dropsrvrolemember만 고정된 서버 역할에서 로그인을 제거 합니다. 데 사용할 수 있습니다. Sp_droprolemember를 사용 하 여 데이터베이스 역할에서 구성원을 제거 합니다.  
  
 어떠한 고정된 서버 역할에서 sa 로그인을 제거할 수 없습니다.  
  
 sp_dropsrvrolemember는 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 또는 ALTER ANY LOGIN 권한이 둘 다 서버 및 멤버를 삭제 하 고 역할의 멤버 자격의에서 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예는 `JackO` 고정 서버 역할에서 `sysadmin` 로그인을 제거합니다.  
  
```  
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [서버 역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER role&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [보안 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
