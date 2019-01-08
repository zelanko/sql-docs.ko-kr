---
title: sp_unregistercustomresolver (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46de29c32442bb2c7672eb7043d10c185327963b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783265"
---
# <a name="spunregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이전에 등록된 비즈니스 논리 모듈을 등록 취소합니다. 비즈니스 논리는 COM 구성 요소 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 어셈블리 형식일 수 있습니다. 이 저장 프로시저는 사용자 지정 비즈니스 논리가 등록된 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>인수  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 등록을 취소할 사용자 지정 비즈니스 논리의 이름을 지정합니다. *article_resolver* 됩니다 **nvarchar(255)**, 기본값은 없습니다. 제거될 비즈니스 논리가 COM 구성 요소인 경우 이 매개 변수는 해당 구성 요소의 이름입니다. 비즈니스 논리가 .NET Framework 어셈블리인 경우 이 매개 변수는 해당 어셈블리의 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_unregistercustomresolver** 병합 복제에 사용 됩니다.  
  
 사용 하 여 [sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 모든 서버에서 복제 토폴로지를 토폴로지에 등록 된 사용자 지정 비즈니스 논리 모듈 또는 사용 가능한 COM 해결 프로그램의 목록을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_unregistercustomresolver**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_registercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
