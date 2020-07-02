---
title: sp_add_targetservergroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_targetservergroup
- sp_add_targetservergroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_targetservergroup
ms.assetid: acb69343-d766-46ff-b771-0c7655c5231a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 72a125d48251d1f4a4ff95aad2fbd0113e5cd7f3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646408"
---
# <a name="sp_add_targetservergroup-transact-sql"></a>sp_add_targetservergroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정된 서버 그룹을 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_targetservergroup [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'`만들 서버 그룹의 이름입니다. *name* 은 **sysname**이며 기본값은 없습니다. *이름* 에는 쉼표를 사용할 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 대상 서버 그룹은 대상 서버 컬렉션에서 작업을 대상화하는 간편한 방법을 제공합니다. 자세한 내용은 [sp_apply_job_to_targets](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Servers Processing Customer Orders`라는 대상 서버 그룹을 만듭니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_targetservergroup  
    'Servers Processing Customer Orders' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_apply_job_to_targets &#40;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_help_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_update_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
