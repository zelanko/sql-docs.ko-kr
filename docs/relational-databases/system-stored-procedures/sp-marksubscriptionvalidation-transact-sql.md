---
title: sp_marksubscriptionvalidation (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab5a5937b2f3baf3b97aeacbee79424f9a701d3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719267"
---
# <a name="sp_marksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  현재 열려 있는 트랜잭션을 지정된 구독자에 대한 구독 수준 유효성 검사 트랜잭션으로 표시합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 sysname 이며 기본값은 없습니다.  
  
`[ @destination_db = ] 'destination_db'`대상 데이터베이스의 이름입니다. *destination_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'`이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 속하는 게시에는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_marksubscriptionvalidation** 은 트랜잭션 복제에 사용 됩니다.  
  
 **sp_marksubscriptionvalidation** 는 이외 구독자를 지원 하지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 이외 게시자의 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 명시적 트랜잭션 내에서 **sp_marksubscriptionvalidation** 를 실행할 수 없습니다. 이는 게시자에 액세스하는 데 사용되는 연결된 서버 연결을 통해서는 명시적 트랜잭션이 지원되지 않기 때문입니다.  
  
 **sp_marksubscriptionvalidation** 는 *subscription_level*에 대해 값 **1** 을 지정 하 고 sp_marksubscriptionvalidation에 대 한 다른 호출에서 다른 구독자에 대해 현재 열려 있는 트랜잭션을 **표시 하는** 데 사용할 수 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)와 함께 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_marksubscriptionvalidation**을 실행할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 쿼리는 게시 데이터베이스가 구독 수준 유효성 검사 명령을 게시하는 데 적용할 수 있습니다. 다음 명령은 지정한 구독자의 배포 에이전트에 의해 적용됩니다. 첫 번째 트랜잭션은 '**art1**' 아티클의 유효성을 검사 하는 반면 두 번째 트랜잭션은 '**art2**'의 유효성을 검사 합니다. 또한 **sp_marksubscriptionvalidation** 및 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 에 대 한 호출이 트랜잭션에 캡슐화 되어 있습니다. 트랜잭션 당 [transact-sql&#41;&#40;sp_article_validation](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 에는 한 번만 호출 하는 것이 좋습니다. 이는 [sp_article_validation &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 트랜잭션 기간 동안 원본 테이블에 대 한 공유 테이블 잠금을 보유 하 고 있기 때문입니다. 반드시 트랜잭션 길이를 짧게 유지하여 동시성을 최대화해야 합니다.  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
