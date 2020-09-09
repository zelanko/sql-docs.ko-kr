---
description: sp_delete_targetservergroup(Transact-SQL)
title: sp_delete_targetservergroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetservergroup_TSQL
- sp_delete_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetservergroup
ms.assetid: d8dd838e-64aa-419f-9ccb-ff04908cf3e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1aebbb09f70f0a0cc3756c4cec53decc0cdbf94
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548123"
---
# <a name="sp_delete_targetservergroup-transact-sql"></a>sp_delete_targetservergroup(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  지정된 대상 서버 그룹을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_targetservergroup [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'` 제거할 대상 서버 그룹의 이름입니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 대상 서버 그룹 `Servers Processing Customer Orders`를 제거합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetservergroup  
    @name = N'Servers Processing Customer Orders';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_help_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_update_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
  
  
