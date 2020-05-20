---
title: sp_help_targetservergroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetservergroup_TSQL
- sp_help_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetservergroup
ms.assetid: ec3a4a68-b591-431c-9518-053ede522d0c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3329efc6ecb0ed19788138987a0f88210abeaaa3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820433"
---
# <a name="sp_help_targetservergroup-transact-sql"></a>sp_help_targetservergroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 그룹의 모든 대상 서버를 나열합니다. 그룹을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 모든 대상 서버 그룹에 관한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_targetservergroup  
    [ [ @name = ] 'name' ]  
```  
  
## <a name="argument"></a>인수  
`[ @name = ] 'name'`정보를 반환할 대상 서버 그룹의 이름입니다. *name* 은 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**servergroup_id**|**int**|서버 그룹의 ID 번호입니다.|  
|**name**|**sysname**|서버 그룹의 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 **sysadmin** 고정 서버 역할에 대 한 것입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-information-for-all-target-server-groups"></a>A. 모든 대상 서버 그룹에 대한 정보 나열  
 다음 예에서는 모든 대상 서버 그룹에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetservergroup ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server-group"></a>B. 특정 대상 서버 그룹에 대한 정보 나열  
 다음 예에서는 `Servers Maintaining Customer Information` 대상 서버 그룹에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetservergroup   
    N'Servers Maintaining Customer Information' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_add_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_delete_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [Transact-sql&#41;sp_update_targetservergroup &#40;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
