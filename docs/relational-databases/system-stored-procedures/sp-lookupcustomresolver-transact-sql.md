---
title: sp_lookupcustomresolver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 274276a55a7b3e91ff85330a0810f01786a5a080
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937902"
---
# <a name="sp_lookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  비즈니스 논리 처리기 또는 배포자에 등록된 COM 기반 사용자 지정 해결 프로그램 구성 요소의 CLSID(클래스 식별자) 값에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @article_resolver = ] 'article_resolver'`등록을 취소할 사용자 지정 비즈니스 논리의 이름을 지정 합니다. *article_resolver* 은 **nvarchar (255)** 이며 기본값은 없습니다. 제거할 비즈니스 논리가 COM 구성 요소이면 이 매개 변수는 해당 구성 요소의 이름이며 비즈니스 논리가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 어셈블리이면 이 매개 변수는 어셈블리의 이름입니다.  
  
`[ @resolver_clsid = ] 'resolver_clsid' OUTPUT`*Article_resolver* 매개 변수에 지정 된 사용자 지정 비즈니스 논리의 이름과 연결 된 COM 개체의 CLSID 값입니다. *resolver_clsid* 는 **nvarchar (50)** 이며 기본값은 NULL입니다.  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly' OUTPUT`등록할 사용자 지정 비즈니스 논리의 유형을 지정 합니다. *is_dotnet_assembly* 은 **bit**이며 기본값은 0입니다. **1** 은 등록할 사용자 지정 비즈니스 논리가 비즈니스 논리 처리기 어셈블리 임을 나타냅니다. **0** 은 COM 구성 요소 임을 나타냅니다.  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT`비즈니스 논리 처리기를 구현 하는 어셈블리의 이름입니다. *dotnet_assembly_name* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT`는를 재정의 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 하 여 비즈니스 논리 처리기를 구현 하는 클래스의 이름입니다. *dotnet_class_name* 은 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다. 저장 프로시저가 게시자에서 호출되지 않을 경우 이 매개 변수를 사용하십시오. 지정하지 않으면 로컬 서버가 게시자인 것으로 가정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_lookupcustomresolver** 는 병합 복제에 사용 됩니다.  
  
 **sp_lookupcustomresolver** 는 구성 요소가 배포에 등록 되어 있지 않을 때 *RESOLVER_CLSID* 에 대해 NULL 값을 반환 하 고, 등록이 비즈니스 논리 처리기로 등록 된 .NET Framework 어셈블리에 속하는 경우 값 "00000000-0000-0000-0000-000000000000"을 반환 합니다.  
  
 지정 된 *article_resolver*의 유효성을 검사 하기 위해 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 및 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 에서 **sp_lookupcustomresolver** 를 호출 합니다.  
  
## <a name="permissions"></a>사용 권한  
 게시 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_lookupcustomresolver**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [병합 동기화 중 비즈니스 논리 실행](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [병합 아티클에 대 한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [병합 아티클 해결 프로그램 지정](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [Transact-sql&#41;sp_registercustomresolver &#40;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Transact-sql&#41;sp_unregistercustomresolver &#40;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
