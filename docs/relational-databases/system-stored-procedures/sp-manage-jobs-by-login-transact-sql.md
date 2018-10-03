---
title: sp_manage_jobs_by_login (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: dc6538cbc62be98414b180d44725d987e660ff99
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742441"
---
# <a name="spmanagejobsbylogin-transact-sql"></a>sp_manage_jobs_by_login(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 로그인에 속하는 작업을 삭제하거나 다시 할당합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_manage_jobs_by_login  
     [ @action = ] 'action'  
     [, [@current_owner_login_name = ] 'current_owner_login_name']  
     [, [@new_owner_login_name = ] 'new_owner_login_name']  
```  
  
## <a name="arguments"></a>인수  
 [  **@action=** ] **'***동작***'**  
 지정된 로그인에 대해 수행할 동작입니다. *동작* 됩니다 **varchar(10)**, 기본값은 없습니다. 때 *동작*됩니다 **삭제**, **sp_manage_jobs_by_login** 소유 하는 모든 작업을 삭제 *current_owner_login_name*합니다. 때 *동작* 됩니다 **재할당**, 모든 작업에 할당 된 *new_owner_login_name*합니다.  
  
 [ **@current_owner_login_name=** ] **'***current_owner_login_name***'**  
 현재 작업 소유자의 로그인 이름입니다. *current_owner_login_name* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@new_owner_login_name=** ] **'***new_owner_login_name***'**  
 새 작업 소유자의 로그인 이름입니다. 경우에만이 매개 변수를 사용 하 여 *동작* 됩니다 **재할당**합니다. *new_owner_login_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 이 저장된 프로시저를 실행 하려면 사용자에 부여 해야 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_delete_job &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
