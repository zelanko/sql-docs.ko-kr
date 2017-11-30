---
title: sp_update_category (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_category
- sp_update_category_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_update_category
ms.assetid: 098b926a-b078-4122-a5e1-3ef54b979dd4
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fad21c3db995f5eaa57d3f31c6ed057b7c9790b8
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="spupdatecategory-transact-sql"></a>sp_update_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  범주의 이름을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_category  
     [@class =] 'class' ,   
     [@name =] 'old_name' ,  
     [@new_name =] 'new_name'  
```  
  
## <a name="arguments"></a>인수  
 [  **@class =**] **'***클래스***'**  
 업데이트할 범주의 클래스입니다. *클래스*은 **varchar(8)**, 기본값은 없고 수와 이러한 값 중 하나 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**경으십시오**|경고 범주를 업데이트합니다.|  
|**작업**|작업 범주를 업데이트합니다.|  
|**연산자**|연산자 범주를 업데이트합니다.|  
  
 [  **@name =**] **'***old_name***'**  
 범주의 현재 이름입니다. *old_name*은 **sysname**, 기본값은 없습니다.  
  
 [  **@new_name =**] **'***new_name***'**  
 범주의 새 이름입니다. *new_name*은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_update_category** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장된 프로시저를 실행 하려면 사용자에 게 부여 해야 합니다는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 작업 범주의 이름을 `AdminJobs`에서 `Administrative Jobs`로 바꿉니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_category  
  @class = N'JOB',  
  @name = N'AdminJobs',  
  @new_name = N'Administrative Jobs' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
