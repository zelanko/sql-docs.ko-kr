---
title: sp_add_category (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_add_category
- sp_add_category_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a180b1719f11b19097d2599847f1167f15ce7424
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spaddcategory-transact-sql"></a>sp_add_category(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  작업, 경고 또는 운영자의 지정된 범주를 서버에 추가합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>인수  
 [  **@class =** ] **'***클래스***'**  
 추가할 범주의 클래스입니다. *클래스* 은 **varchar(8)** , 작업의 기본 값 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|JOB|작업 범주를 추가합니다.|  
|ALERT|경고 범주를 추가합니다.|  
|OPERATOR|운영자 범주를 추가합니다.|  
  
 [  **@type =** ] **'***형식***'**  
 추가할 범주의 유형입니다. *형식* 은 **varchar(12)**의 기본값은 **로컬**, 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|LOCAL|로컬 작업 범주|  
|다중 서버|다중 서버 작업 범주|  
|없음|JOB이 아닌 다른 클래스에 대 한 범주**합니다.**|  
  
 [  **@name =** ] **'***이름***'**  
 추가할 범주의 이름입니다. 이름은 지정한 클래스 내에서 고유해야 합니다. *이름* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 **sp_add_category** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_add_category**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdminJobs`라는 로컬 작업 범주를 만듭니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_delete_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sysjobs&#40; Transact SQL &#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40; Transact SQL &#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
