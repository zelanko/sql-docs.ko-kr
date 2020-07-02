---
title: sp_delete_jobserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobserver
- sp_delete_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobserver
ms.assetid: 6d63ed32-68cf-4d8f-aa40-05a3826e05b8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 87597bbf7685f525eb2dab5c9dfed623b1577359
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750627"
---
# <a name="sp_delete_jobserver-transact-sql"></a>sp_delete_jobserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정된 대상 서버를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_jobserver { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>인수  
`[ @job_id = ] job_id`지정 된 대상 서버를 제거할 작업의 id입니다. *job_id* 은 **uniqueidentifier**이며 기본값은 NULL입니다.  
  
`[ @job_name = ] 'job_name'`지정 된 대상 서버를 제거할 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Job_id* 또는 *job_name* 를 지정 해야 합니다. 둘 다 지정할 수 없습니다.  
  
`[ @server_name = ] 'server'`지정 된 작업에서 제거할 대상 서버의 이름입니다. *서버* 는 **nvarchar (30)** 이며 기본값은 없습니다. *서버* 는 **(LOCAL)** 또는 원격 대상 서버의 이름일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자가 **sysadmin** 고정 서버 역할의 멤버 여야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 작업 처리에서 서버를 제거 합니다 `SEATTLE2` `Weekly Sales Backups` .  
  
> [!NOTE]  
>  이 예에서는 `Weekly Sales Backups` 작업이 이전에 생성된 것으로 가정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [Transact-sql&#41;sp_help_jobserver &#40;](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
