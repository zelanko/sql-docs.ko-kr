---
title: sp_registercustomresolver (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7873d4288addbeaaba44fc7030f140180458e301
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608751"
---
# <a name="spregistercustomresolver-transact-sql"></a>sp_registercustomresolver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제 동기화 프로세스를 수행하는 동안 호출될 수 있는 비즈니스 논리 처리기 또는 COM 기반 사용자 지정 해결 프로그램을 등록합니다. 이 저장 프로시저는 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 등록할 사용자 지정 비즈니스 논리의 이름을 지정합니다. *article_resolver* 됩니다 **nvarchar(255)**, 기본값은 없습니다.  
  
 [  **@resolver_clsid=** ] **'***resolver_clsid***'**  
 등록할 COM 개체의 CLSID 값을 지정합니다. 사용자 지정 비즈니스 논리 *resolver_clsid* 됩니다 **nvarchar (50)**, 기본값은 NULL입니다. 이 매개 변수는 유효한 CLSID로 설정하거나 비즈니스 논리 처리기 어셈블리를 등록할 때는 NULL로 설정해야 합니다.  
  
 [  **@is_dotnet_assembly=** ] **'***is_dotnet_assembly***'**  
 등록할 사용자 지정 비즈니스 논리의 유형을 지정합니다. *is_dotnet_assembly* 됩니다 **nvarchar (50)**, 기본값은 FALSE입니다. **true** 등록할 사용자 지정 비즈니스 논리가 비즈니스 논리 처리기 어셈블리 임을 나타냅니다 **false** 은 COM 구성 요소임을 나타냅니다.  
  
 [  **@dotnet_assembly_name=** ] **'***dotnet_assembly_name***'**  
 비즈니스 논리 처리기를 구현하는 어셈블리의 이름입니다. *dotnet_assembly_name* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다. 어셈블리가 병합 에이전트 실행 파일과 같은 디렉터리, 병합 에이전트를 동기적으로 시작하는 응용 프로그램과 같은 디렉터리 또는 GAC(전역 어셈블리 캐시)에서 배포되지 않은 경우 어셈블리에 대한 전체 경로를 지정해야 합니다.  
  
 [  **@dotnet_class_name=** ] **'***dotnet_class_name***'**  
 비즈니스 논리 처리기를 구현하도록 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>을 재정의하는 클래스의 이름입니다. 형식 이름을 지정 해야 **Namespace.Classname**합니다. *dotnet_class_name* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_registercustomresolver** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_registercustomresolver**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
