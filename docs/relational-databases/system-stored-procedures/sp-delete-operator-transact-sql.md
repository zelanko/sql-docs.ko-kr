---
description: sp_delete_operator(Transact-SQL)
title: sp_delete_operator (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_operator
- sp_delete_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_operator
ms.assetid: ff6c2c4b-e9fe-4d0c-bbc2-a2ddcc1acb95
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d228dbfe5d349a69addded2fe4eeadca6656836c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541813"
---
# <a name="sp_delete_operator-transact-sql"></a>sp_delete_operator(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  운영자를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_operator [ @name = ] 'name'   
     [ , [ @reassign_to_operator = ] 'reassign_operator' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'` 삭제할 운영자의 이름입니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @reassign_to_operator = ] 'reassign_operator'` 지정 된 운영자의 경고를 재할당할 수 있는 운영자의 이름입니다. *reassign_operator* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 운영자가 제거되면 그 운영자와 연관된 알림도 모두 함께 제거됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버는 **sp_delete_operator**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 운영자 `François Ajenstat`를 삭제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_operator @name = 'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_operator &#40;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [Transact-sql&#41;sp_help_operator &#40;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Transact-sql&#41;sp_update_operator &#40;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
