---
title: sp_article_validation (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords: sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed9bf6e4375c3b7afb18ffa938ae29e8d1e9e48e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 아티클에 대한 데이터 유효성 검사 요청을 시작합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=**] **'***게시***'**  
 아티클이 있는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 유효성을 검사할 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 테이블의 행 개수만 반환되는지 지정합니다. *type_of_check_requested* 은 **smallint**, 기본값은 **1**합니다.  
  
 경우 **0**, 수행할 행 개수 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬.  
  
 경우 **1**, 행 개수 검사만 수행 합니다.  
  
 경우 **2**, 행 개수 및 이진 체크섬을 수행 합니다.  
  
 [  **@full_or_fast=**] *full_or_fast*  
 행 개수를 계산하는 데 사용하는 방법입니다. *full_or_fast* 은 **tinyint**, 다음이 값 중 하나일 수 있습니다.  
  
|**Value**|**Description**|  
|---------------|---------------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|빠른 계산을 수행 **sysindexes.rows**합니다. 행 개수 계산 **sysindexes** 실제 테이블에서의 행 계산 보다 빠릅니다. 그러나 **sysindexes** 는 느리게 업데이트 되므로 행 개수가 정확 하 게 되지 않을 수 있습니다.|  
|**2** (기본값)|조건에 따라 계산 방법을 결정합니다. 먼저 빠른 계산 방법이 시도됩니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. 경우 *expected_rowcount* 저장된 프로시저 되 고 null 값을 사용 하는, 전체 그룹 항상 사용 됩니다.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 유효성 검사가 종료되면 배포 에이전트가 즉시 종료되어야 하는지 여부를 지정합니다. *shutdown_agent* 은 **비트**, 기본값은 **0**합니다. 경우 **0**, 배포 에이전트가 종료 되지는 않습니다. 경우 **1**, 아티클의 유효성을 검사 한 후 배포 에이전트를 종료 합니다.  
  
 [  **@subscription_level=**] *subscription_level*  
 구독자 집합에 의해 유효성 검사가 선택되는지 여부를 지정합니다. *subscription_level* 은 **비트**, 기본값은 **0**합니다. 경우 **0**, 유효성 검사가 모든 구독자에 적용 됩니다. 경우 **1**, 유효성 검사를 호출 하 여 지정 된 구독자 하위 집합에만 적용 됩니다 **sp_marksubscriptionvalidation** 현재 열린 트랜잭션에서 합니다.  
  
 [  **@reserved=**] *예약*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher** =] **'***게시자***'**  
 지정 된 비-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에 유효성 검사를 요청할 때 사용할 수 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_article_validation** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_article_validation** 유효성 검사 정보 지정 된 문서를 수집 하 고 트랜잭션 로그에 유효성 검사 요청을 게시 합니다. 배포 에이전트는 이 요청을 받아 구독자 테이블이 받은 요청의 유효성 검사 정보와 비교합니다. 유효성 검사의 결과는 복제 모니터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 표시됩니다.  
  
## <a name="permissions"></a>Permissions  
 유효성을 검사 중인 문서를 실행할 수 있는 사용자가 원본 테이블에 대 한 모든 권한을 선택만 **sp_article_validation**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 된 데이터 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
