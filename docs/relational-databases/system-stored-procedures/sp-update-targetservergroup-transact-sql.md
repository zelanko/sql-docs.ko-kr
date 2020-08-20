---
description: sp_update_targetservergroup(Transact-SQL)
title: sp_update_targetservergroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_targetservergroup_TSQL
- sp_update_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_targetservergroup
ms.assetid: 4ac65ed6-e07e-40e4-a282-13bfd92dfa41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6aa33876376560cfc90cbf7ab03a69fcf94fa6a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473549"
---
# <a name="sp_update_targetservergroup-transact-sql"></a>sp_update_targetservergroup(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정한 대상 서버 그룹의 이름을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_targetservergroup  
     [@name =] 'current_name' ,  
     [@new_name =] 'new_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'current_name'` 대상 서버 그룹의 이름입니다. *current_name* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @new_name = ] 'new_name'` 대상 서버 그룹의 새 이름입니다. *new_name* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행 하려면 사용자에 게 **sysadmin** 고정 서버 역할을 부여 해야 합니다.  
  
## <a name="remarks"></a>설명  
 **sp_update_targetservergroup** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 대상 서버 그룹 `Servers Processing Customer Orders`를 `Local Servers Processing Customer Orders`로 변경합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_targetservergroup  
    @name = N'Servers Processing Customer Orders',  
    @new_name = N'Local Servers Processing Customer Orders' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_help_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
