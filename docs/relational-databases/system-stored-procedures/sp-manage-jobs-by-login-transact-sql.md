---
title: sp_manage_jobs_by_login (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_manage_jobs_by_login
- sp_manage_jobs_by_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_manage_jobs_by_login
ms.assetid: 832ec15a-6e92-4eb5-8c4a-af4dba79fbaa
author: stevestein
ms.author: sstein
ms.openlocfilehash: ebc71c304939a977ac34cc2fad819edd463614fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67894990"
---
# <a name="sp_manage_jobs_by_login-transact-sql"></a>sp_manage_jobs_by_login(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 로그인에 속하는 작업을 삭제하거나 다시 할당합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_manage_jobs_by_login  
     [ @action = ] 'action'  
     [, [@current_owner_login_name = ] 'current_owner_login_name']  
     [, [@new_owner_login_name = ] 'new_owner_login_name']  
```  
  
## <a name="arguments"></a>인수  
`[ @action = ] 'action'`지정 된 로그인에 대해 수행할 동작입니다. *action* 은 **varchar (10)** 이며 기본값은 없습니다. *작업이* **DELETE**인 경우 **sp_manage_jobs_by_login** 는 *current_owner_login_name*소유의 모든 작업을 삭제 합니다. *작업이* **재할당**되 면 모든 작업이 *new_owner_login_name*에 할당 됩니다.  
  
`[ @current_owner_login_name = ] 'current_owner_login_name'`현재 작업 소유자의 로그인 이름입니다. *current_owner_login_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @new_owner_login_name = ] 'new_owner_login_name'`새 작업 소유자의 로그인 이름입니다. *작업* 을 **다시 할당**하는 경우에만이 매개 변수를 사용 합니다. *new_owner_login_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `danw` 의 모든 작업을 `françoisa`에 다시 할당합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_manage_jobs_by_login  
    @action = N'REASSIGN',  
    @current_owner_login_name = N'danw',  
    @new_owner_login_name = N'françoisa' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_job &#40;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
