---
description: sp_addmergefilter(Transact-SQL)
title: sp_addmergefilter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1149db6cfbebcc1dc1ec2b62fcbb0ce02b93fad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489668"
---
# <a name="sp_addmergefilter-transact-sql"></a>sp_addmergefilter(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  다른 테이블과의 조인을 기반으로 하는 파티션을 만들기 위해 새 병합 필터를 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 병합 필터를 추가할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'` 병합 필터를 추가할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @filtername = ] 'filtername'` 필터의 이름입니다. *filtername* 는 필수 매개 변수입니다. *filtername*는 **sysname**이며 기본값은 없습니다.  
  
`[ @join_articlename = ] 'join_articlename'`*아티클에*지정 된 자식 아티클이 병합 필터의 필터 조건을 충족 하는 자식 아티클의 행을 확인 하기 위해 *join_filterclause*에 지정 된 join 절을 사용 하 여 조인 되어야 하는 부모 아티클입니다. *join_articlename* 는 **sysname**이며 기본값은 없습니다. 아티클은 *게시*에 지정 된 게시에 있어야 합니다.  
  
`[ @join_filterclause = ] join_filterclause`병합 필터를 정규화 하는 행을 결정 하기 위해 *join_article*에 지정 된 *아티클*및 부모 아티클에 지정 된 자식 아티클을 조인 하는 데 사용 해야 하는 join 절입니다. *join_filterclause* 는 **nvarchar (1000)** 입니다.  
  
`[ @join_unique_key = ] join_unique_key` 자식 아티클 *문서*와 부모 아티클 *join_article*간의 조인이 일 대 다, 일 대 일, 다 대 일 또는 다 대 다 인지를 지정 합니다. *join_unique_key* 은 **int**이며 기본값은 0입니다. **0** 은 다 대 일 또는 다 대 다 조인을 나타냅니다. **1** 은 일 대 일 또는 일 대 다 조인을 나타냅니다. 이 값은 조인 하는 열이 *join_article*에서 고유 키를 형성 하거나 *아티클의* 외래 키와 *join_article*의 기본 키 사이에 *join_filterclause* 있는 경우 **1** 입니다.  
  
> [!CAUTION]  
>  부모 아티클의 기본 테이블에 있는 조인 열에 고유성을 보장 하는 제약 조건이 있는 경우에만이 매개 변수를 **1** 로 설정 합니다. *Join_unique_key* **1** 로 잘못 설정 된 경우 데이터가 일치 하지 않을 수 있습니다.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 해당 저장 프로시저가 새 스냅샷이 필요한 변경을 검색할 경우, 오류가 발생하여 변경할 수 없습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되도록 지정 합니다. 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화 해야 할 수도 있습니다. *force_reinit_subscription* 은 **bit**이며 기본값은 0입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다. 해당 저장 프로시저가 구독을 다시 초기화해야 하는 변경을 검색할 경우, 오류가 발생하여 변경할 수 없습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 되도록 지정 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
`[ @filter_type = ] filter_type` 추가할 필터의 유형을 지정 합니다. *filter_type* 은 **tinyint**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|조인 필터 전용입니다. 이 기능은 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자를 지원하는 데 필요합니다.|  
|**2**|논리적 레코드 관계 전용입니다.|  
|**3**|조인 필터 및 논리적 레코드 관계 모두를 사용할 수 있습니다.|  
  
 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addmergefilter** 는 병합 복제에 사용 됩니다.  
  
 **sp_addmergefilter** 은 테이블 아티클에만 사용할 수 있습니다. 뷰 및 인덱싱된 뷰 아티클은 지원되지 않습니다.  
  
 이 프로시저는 조인 필터가 있을 수도 있고 없을 수도 있는 두 아티클 사이에 논리적 관계를 추가하는 데 사용할 수도 있습니다. *filter_type* 는 추가 되는 병합 필터가 조인 필터 인지, 논리적 관계 인지 또는 둘 다 인지를 지정 하는 데 사용 됩니다.  
  
 논리적 레코드를 사용하려면 게시 및 아티클이 여러 가지 요구 사항을 만족해야 합니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
 이 옵션은 일반적으로 자체 아티클에 필터가 정의된 게시된 기본 키 테이블에 대한 외래 키 참조를 가진 아티클에 사용됩니다. 구독자로 복제되는 외래 키 행을 결정하기 위해 기본 키 행의 하위 집합이 사용됩니다.  
  
 두 아티클의 원본 테이블이 동일한 테이블 개체 이름을 공유할 경우 게시된 두 개의 아티클 간에 조인 필터를 추가할 수 없습니다. 이럴 경우 두 개의 테이블을 서로 다른 스키마가 소유하고 있고 고유한 아티클 이름을 가지고 있더라도 조인 필터를 만들 수 없습니다.  
  
 매개 변수가 있는 행 필터 및 조인 필터 모두를 테이블 아티클에서 사용할 경우 복제에 의해 행이 구독자의 파티션에 속하는지 여부가 결정됩니다. 이렇게 하려면 [and](../../t-sql/language-elements/and-transact-sql.md) 연산자를 사용 하 여 두 조건의 교집합을 계산 하는 대신 [or](../../t-sql/language-elements/or-transact-sql.md) 연산자를 사용 하 여 필터링 함수 또는 조인 필터를 평가 합니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addmergefilter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Transact-sql&#41;sp_changemergefilter &#40;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
