---
title: sp_delete_category (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_category_TSQL
- sp_delete_category
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_category
ms.assetid: 63ea7d0d-a567-456e-a778-bee99e21d16c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9a6812e12366900dfc1c5808eaede727c05f958
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120045"
---
# <a name="spdeletecategory-transact-sql"></a>sp_delete_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 서버에서 지정된 범주의 작업, 경고 또는 연산자를 제거합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_category [ @class = ] 'class' , [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>인수  
`[ @class = ] 'class'` 범주의 클래스입니다. *클래스* 은 **varchar(8)** 해야 없고 기본적으로 사용 하 여 이러한 값 중 하나가 있어야 합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**JOB**|작업 범주를 제거합니다.|  
|**ALERT**|경고 범주를 제거합니다.|  
|**연산자**|연산자 범주를 제거합니다.|  
  
`[ @name = ] 'name'` 제거할 범주의 이름입니다. *이름을* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_delete_category** 에서 실행 해야 합니다 **msdb** 데이터베이스입니다.  
  
 범주를 제거하면 해당 범주의 모든 작업, 경고 또는 연산자를 해당 클래스의 기본 범주로 다시 범주화합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할에서이 프로시저를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdminJobs`라는 작업 범주를 삭제합니다.  
  
```  
USE msdb ;  
GO   
  
EXEC dbo.sp_delete_category  
    @name = N'AdminJobs',  
    @class = N'JOB' ;  
GO   
```  
  
## <a name="see-also"></a>참조  
 [sp_add_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_help_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
