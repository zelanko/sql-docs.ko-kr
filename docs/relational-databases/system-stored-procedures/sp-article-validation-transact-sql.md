---
title: sp_article_validation (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 6f5ee076163ff3cf0f69daab7ceff115bf5876a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769019"
---
# <a name="sp_article_validation-transact-sql"></a>sp_article_validation(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정한 아티클에 대한 데이터 유효성 검사 요청을 시작합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`아티클이 있는 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`유효성을 검사할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @rowcount_only = ] type_of_check_requested`테이블에 대 한 행 개수만 반환 되는지 여부를 지정 합니다. *type_of_check_requested* 은 **smallint**이며 기본값은 **1**입니다.  
  
 **0**인 경우 rowcount 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬을 수행 합니다.  
  
 **1**인 경우에는 rowcount 검사만 수행 합니다.  
  
 **2**인 경우 행 개수와 이진 체크섬을 수행 합니다.  
  
`[ @full_or_fast = ] full_or_fast`행 개수를 계산 하는 데 사용 되는 방법입니다. *full_or_fast* 은 **tinyint**이며 다음 값 중 하나일 수 있습니다.  
  
|**값**|**설명**|  
|---------------|---------------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|**Sysindexes 행**에서 빠른 카운트를 수행 합니다. **Sysindexes** 에서 행을 계산 하는 것은 실제 테이블의 행 수를 계산 하는 것 보다 빠릅니다. 그러나 **sysindexes** 는 지연 업데이트 되며 rowcount는 정확 하지 않을 수 있습니다.|  
|**2** (기본값)|조건에 따라 계산 방법을 결정합니다. 먼저 빠른 계산 방법이 시도됩니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. *Expected_rowcount* 가 NULL이 고 저장 프로시저를 사용 하 여 값을 가져오는 경우에는 항상 전체 개수 (*)가 사용 됩니다.|  
  
`[ @shutdown_agent = ] shutdown_agent`유효성 검사가 완료 되 면 배포 에이전트가 즉시 종료 되어야 하는지 여부를 지정 합니다. *shutdown_agent* 은 **bit**이며 기본값은 **0**입니다. **0**인 경우 배포 에이전트 종료 되지 않습니다. **1**인 경우 아티클의 유효성을 검사 한 후 배포 에이전트 종료 됩니다.  
  
`[ @subscription_level = ] subscription_level`구독자 집합에서 유효성 검사를 선택 하는지 여부를 지정 합니다. *subscription_level* 은 **bit**이며 기본값은 **0**입니다. **0**인 경우 모든 구독자에 유효성 검사가 적용 됩니다. **1**인 경우 현재 열려 있는 트랜잭션의 **sp_marksubscriptionvalidation** 에 대 한 호출로 지정 된 구독자의 하위 집합에만 유효성 검사가 적용 됩니다.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  ** 게시자에 대 한 유효성 검사를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 요청할 때는 게시자를 사용 하면 안 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_article_validation** 은 트랜잭션 복제에 사용 됩니다.  
  
 **sp_article_validation** 지정 된 아티클에서 유효성 검사 정보를 수집 하 고 트랜잭션 로그에 유효성 검사 요청을 게시 합니다. 배포 에이전트는 이 요청을 받아 구독자 테이블이 받은 요청의 유효성 검사 정보와 비교합니다. 유효성 검사의 결과는 복제 모니터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 표시됩니다.  
  
## <a name="permissions"></a>사용 권한  
 유효성을 검사할 아티클의 원본 테이블에 대 한 SELECT ALL 권한이 있는 사용자만 **sp_article_validation**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Transact-sql&#41;sp_marksubscriptionvalidation &#40;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [Transact-sql&#41;sp_publication_validation &#40;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [Transact-sql&#41;sp_table_validation &#40;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
