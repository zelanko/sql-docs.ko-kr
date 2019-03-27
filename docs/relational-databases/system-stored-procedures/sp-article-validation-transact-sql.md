---
title: sp_article_validation (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be3ccf8b0c85b61f536c381e4a42d1b5e37fbacf
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493274"
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
`[ @publication = ] 'publication'` 문서 존재 하는 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 유효성을 검사할 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @rowcount_only = ] type_of_check_requested` 테이블의 행 개수만 반환 되는지 지정 합니다. *type_of_check_requested* 됩니다 **smallint**, 기본값은 **1**합니다.  
  
 하는 경우 **0**를 수행할 행 개수와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬.  
  
 하는 경우 **1**, 행 개수 검사만 수행 합니다.  
  
 하는 경우 **2**, 행 개수 및 이진 체크섬을 수행 합니다.  
  
`[ @full_or_fast = ] full_or_fast` 행 개수를 계산 하려면 메서드가 사용 됩니다. *full_or_fast* 됩니다 **tinyint**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|**Value**|**설명**|  
|---------------|---------------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|빠른 계산을 수행 **sysindexes.rows**합니다. 사용한 행 계산은 **sysindexes** 실제 테이블의 행 계산 보다 빠릅니다. 그러나 **sysindexes** 는 느리게 업데이트 되므로 행 개수가 정확 하 게 되지 않을 수 있습니다.|  
|**2** (기본값)|조건에 따라 계산 방법을 결정합니다. 먼저 빠른 계산 방법이 시도됩니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. 하는 경우 *expected_rowcount* 가 NULL이 저장된 프로시저 되 고 값을 가져오려면, 전체 그룹은 항상 사용 합니다.|  
  
`[ @shutdown_agent = ] shutdown_agent` 하는 경우 배포 에이전트가 즉시 종료 되어야 유효성 검사 완료 시를 지정 합니다. *shutdown_agent* 됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **0**, 배포 에이전트가 종료 되지 않습니다. 하는 경우 **1**, 문서의 유효성을 검사 한 후 배포 에이전트를 종료 합니다.  
  
`[ @subscription_level = ] subscription_level` 구독자 집합에 의해 유효성 검사 선택 여부를 지정 합니다. *subscription_level* 됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **0**, 유효성 검사가 모든 구독자에 적용 됩니다. 하는 경우 **1**, 유효성 검사를 호출 하 여 지정 된 구독자 하위 집합에만 적용 됩니다 **sp_marksubscriptionvalidation** 현재 열려 있는 트랜잭션을에서.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'` 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 유효성 검사를 요청할 때를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_article_validation** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_article_validation** 유효성 검사 정보를 지정 된 문서에서 수집 하 고 트랜잭션 로그에 유효성 검사 요청을 게시 합니다. 배포 에이전트는 이 요청을 받아 구독자 테이블이 받은 요청의 유효성 검사 정보와 비교합니다. 유효성 검사의 결과는 복제 모니터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자 유효성을 검사할 문서 실행 수에 대 한 원본 테이블에 대 한 모든 권한을 선택만 **sp_article_validation**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 된 데이터 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_marksubscriptionvalidation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
