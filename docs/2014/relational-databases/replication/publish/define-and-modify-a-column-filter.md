---
title: 열 필터 정의 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], column
- modifying filters, column
- modifying filters
- column filters [SQL Server replication]
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e0c26e32425f204f7dab29aa65c66f3a11f09d7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753715"
---
# <a name="define-and-modify-a-column-filter"></a>열 필터 정의 및 수정
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 열 필터를 정의하고 수정하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   일부 열은 필터링할 수 없습니다. 자세한 내용은 [게시된 데이터 필터링](filter-published-data.md)을 참조하세요. 구독을 초기화한 후 열 필터를 수정할 경우 새 스냅숏을 만들고 변경 내용을 적용한 후 모든 구독을 다시 초기화해야 합니다. 속성 변경 요구 사항에 대한 자세한 내용은 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **아티클** 페이지에서 열 필터를 정의합니다. 새 게시 마법사 사용 방법에 대한 자세한 내용은 [게시 만들기](create-a-publication.md)를 참조하세요.  
  
 **게시 속성 - \<게시>** 대화 상자의 **아티클** 페이지에서 열 필터를 정의하고 수정합니다. 게시 및 아티클 속성에 대한 자세한 내용은 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-define-a-column-filter"></a>열 필터를 정의하려면  
  
1.  새 게시 마법사의 **아티클** 페이지에 있는 **게시할 개체** 창에서 필터링할 테이블을 확장합니다.  
  
2.  필터링할 각 열 옆에 있는 확인란의 선택을 취소합니다.  
  
#### <a name="to-modify-column-filtering"></a>열 필터링을 수정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **아티클** 페이지에 있는 **게시할 개체** 창에서 필터링할 테이블을 확장합니다.  
  
2.  필터링할 각 열 옆에 있는 확인란의 선택은 취소하고 아티클에 포함시킬 각 열에 대한 확인란은 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 테이블 아티클을 만들 때 아티클에 포함할 열을 정의할 수 있으며 아티클이 정의된 후 이 열을 변경할 수 있습니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 필터링된 열을 만들고 수정할 수 있습니다.  
  
> [!NOTE]  
>  다음 절차에서는 기본 테이블이 변경되지 않은 것으로 가정합니다. DDL(데이터 정의 언어) 변경 내용을 게시된 테이블에 복제하는 방법에 대한 자세한 내용은 [게시 데이터베이스의 스키마 변경](make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 열 필터를 정의하려면  
  
1.  필터링할 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)을 실행합니다. 이렇게 하면 아티클에 포함할 열 또는 아티클에서 제거할 열이 정의됩니다.  
  
    -   많은 열을 포함한 테이블에서 몇 개의 열만 게시하는 경우 추가할 각 열에 대해 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **add** 값을 지정합니다.  
  
    -   많은 열을 포함한 테이블에서 대부분의 열을 게시하는 경우 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)에 **null** 에 대한 **@column** 에 대한 열 이름 및 **@operation** 에 대한 **@operation** 을 실행하여 모든 열을 추가합니다. 그런 다음 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)에 **drop** 에 대한 **@operation** 에 제외되는 열 이름을 지정하고 제외할 각 열에 대해 **@column**에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)를 실행합니다. **@publication**에 게시 이름을, **@article**에 필터링된 아티클의 이름을 지정합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 만들어집니다.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 추가 열을 포함하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 추가할 각 열에 대해 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **add** 값을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)를 실행합니다. **@publication**에 게시 이름을, **@article**에 필터링된 아티클의 이름을 지정합니다. 게시에 기존 구독이 있는 경우 **@change_active** 에 대한 **@change_active**에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 다시 만들어집니다.  
  
3.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
4.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 열을 제거하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 제거할 각 열에 대해 [sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **drop** 값을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)를 실행합니다. **@publication**에 게시 이름을, **@article**에 필터링된 아티클의 이름을 지정합니다. 게시에 기존 구독이 있는 경우 **@change_active** 에 대한 **@change_active**에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 다시 만들어집니다.  
  
3.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
4.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="to-define-a-column-filter-for-an-article-published-in-a-merge-publication"></a>병합 게시에 게시된 아티클에 대한 열 필터를 정의하려면  
  
1.  필터링할 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)을 실행합니다. 이렇게 하면 아티클에 포함할 열 또는 아티클에서 제거할 열이 정의됩니다.  
  
    -   많은 열을 포함한 테이블에서 몇 개의 열만 게시하는 경우 추가할 각 열에서 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **add** 값을 지정합니다.  
  
    -   많은 열을 포함한 테이블에서 대부분의 열을 게시하는 경우 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)에 **null** 에 대한 **@column** 에 대한 열 이름 및 **@operation** 에 대한 **@operation** 을 실행하여 모든 열을 추가합니다. 그런 다음 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)에 **drop** 에 대한 **@operation** 에 제외되는 열 이름을 지정하고 제외할 각 열에 대해 **@column**에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
#### <a name="to-change-a-column-filter-to-include-additional-columns-for-an-article-published-in-a-merge-publication"></a>병합 게시에 게시된 아티클에 대한 추가 열을 포함하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 추가할 각 열에 대해 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **add** 값을, **@force_invalidate_snapshot** 및 **@force_reinit_subscription** 둘 다에 **1** 값을 지정합니다.  
  
2.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="to-change-a-column-filter-to-remove-columns-for-an-article-published-in-a-merge-publication"></a>병합 게시에 게시된 아티클에 대한 열을 제거하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 제거할 각 열에 대해 [sp_mergearticlecolumn](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql) 을 한 번씩 실행합니다. **@column**에 열 이름을, **@operation**에 **drop** 값을, **@force_invalidate_snapshot** 및 **@force_reinit_subscription** 둘 다에 **1** 값을 지정합니다.  
  
2.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../reinitialize-subscriptions.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 트랜잭션 복제 예제에서는 `DaysToManufacture` 테이블에 기반한 아티클에서 `Product` 열이 제거되었습니다.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createtranpub.sql#sp_addtranarticle)]  
  
 이 병합 복제 예제에서는 `CreditCardApprovalCode` 테이블에 기반한 아티클에서 `SalesOrderHeader` 열이 제거되었습니다.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)   
 [게시된 데이터 필터링](filter-published-data.md)   
 [병합 복제의 게시된 데이터 필터링](../merge/filter-published-data-for-merge-replication.md)  
  
  
