---
title: "열 필터 정의 및 수정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "필터 [SQL Server 복제], 열"
  - "필터 수정, 열"
  - "필터 수정"
  - "열 필터 [SQL Server 복제]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 열 필터 정의 및 수정
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 열 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 열 필터를 정의하고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   일부 열을 필터링 할 수 없습니다. 자세한 내용은 참조 [데이터를 게시 하는 필터](../../../relational-databases/replication/publish/filter-published-data.md)합니다. 구독을 초기화한 후 열 필터를 수정할 경우 새 스냅숏을 만들고 변경 내용을 적용한 후 모든 구독을 다시 초기화해야 합니다. 속성 변경에 대 한 요구 사항에 대 한 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **아티클** 페이지에서 열 필터를 정의합니다. 새 게시 마법사를 사용 하는 방법에 대 한 자세한 내용은 참조 [발행물 만들기](../../../relational-databases/replication/publish/create-a-publication.md)합니다.  
  
 정의에서 열 필터를 수정 하 고는 **문서** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 게시 및 아티클 속성에 대 한 자세한 내용은 참조 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 열 필터를 정의하려면  
  
1.  새 게시 마법사의 **아티클** 페이지에 있는 **게시할 개체** 창에서 필터링할 테이블을 확장합니다.  
  
2.  필터링할 각 열 옆에 있는 확인란의 선택을 취소합니다.  
  
#### 열 필터링을 수정하려면  
  
1.  에 **문서** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 필터링 할 테이블을 확장 합니다는 **게시할 개체** 창입니다.  
  
2.  필터링할 각 열 옆에 있는 확인란의 선택은 취소하고 아티클에 포함시킬 각 열에 대한 확인란은 선택합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 테이블 아티클을 만들 때 아티클에 포함할 열을 정의할 수 있으며 아티클이 정의된 후 이 열을 변경할 수 있습니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 필터링된 열을 만들고 수정할 수 있습니다.  
  
> [!NOTE]  
>  다음 절차에서는 기본 테이블이 변경되지 않은 것으로 가정합니다. 데이터 정의 언어 (DDL) 변경 내용을 복제 하는 게시 된 테이블에 대 한 자세한 내용은 참조 [게시 데이터베이스에 스키마 변경을 확인](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 열 필터를 정의하려면  
  
1.  필터링할 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)합니다. 이렇게 하면 아티클에 포함할 열 또는 아티클에서 제거할 열이 정의됩니다.  
  
    -   몇 가지 열만 테이블에서 많은 열을 게시 하는 경우 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 추가할 각 열에 대해 한 번씩 합니다. **@column** 에 대한 열 이름 및 **@operation** 에 대한 **add**값을 지정합니다.  
  
    -   대부분의 열을 여러 열이 있는 테이블에서 게시 하는 경우 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), 의 값을 지정 하 **null** 에 대 한 **@column** 값 **추가** 에 대 한 **@operation** 모든 열을 추가 합니다. 다음 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), 제외 되는 각 열에 대 한 값을 지정 하 되 면, **drop** 에 대 한 **@operation** 및에 대 한 제외 된 열 이름을 **@column**합니다.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)합니다. **@publication** 에 대한 게시 이름 및 **@article**에 대한 필터링된 아티클의 이름을 지정합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 만들어집니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 추가 열을 포함하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 추가할 각 열에 대해 한 번씩 합니다. **@column** 에 대한 열 이름 및 **@operation** 에 대한 **add**값을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)합니다. **@publication** 에 대한 게시 이름 및 **@article**에 대한 필터링된 아티클의 이름을 지정합니다. 게시에 기존 구독이 있는 경우 값을 지정 **1** 에 대 한 **@change_active**합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 다시 만들어집니다.  
  
3.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
4.  구독을 다시 초기화합니다. 자세한 내용은 참조 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
#### 스냅숏 또는 트랜잭션 게시에 게시된 아티클에 대한 열을 제거하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 제거할 각 열에 대해 한 번씩 합니다. **@column** 에 열 이름, **@operation** 에 **drop**값을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)합니다. **@publication** 에 대한 게시 이름 및 **@article**에 대한 필터링된 아티클의 이름을 지정합니다. 게시에 기존 구독이 있는 경우 값을 지정 **1** 에 대 한 **@change_active**합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 다시 만들어집니다.  
  
3.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
4.  구독을 다시 초기화합니다. 자세한 내용은 참조 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
#### 병합 게시에 게시된 아티클에 대한 열 필터를 정의하려면  
  
1.  필터링할 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)합니다. 이렇게 하면 아티클에 포함할 열 또는 아티클에서 제거할 열이 정의됩니다.  
  
    -   몇 가지 열만 테이블에서 많은 열을 게시 하는 경우 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 추가할 각 열에 대해 한 번씩 합니다. **@column** 에 대한 열 이름 및 **@operation** 에 대한 **add**값을 지정합니다.  
  
    -   대부분의 열을 여러 열이 있는 테이블에서 게시 하는 경우 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), 의 값을 지정 하 **null** 에 대 한 **@column** 값 **추가** 에 대 한 **@operation** 모든 열을 추가 합니다. 다음 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), 제외 되는 각 열에 대 한 값을 지정 하 되 면, **drop** 에 대 한 **@operation** 및에 대 한 제외 된 열 이름을 **@column**합니다.  
  
#### 병합 게시에 게시된 아티클에 대한 추가 열을 포함하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 추가할 각 열에 대해 한 번씩 합니다. 에 대 한 열 이름을 지정 **@column**, 값이 **추가** 에 대 한 **@operation** 값 **1** 모두에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
2.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 참조 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
#### 병합 게시에 게시된 아티클에 대한 열을 제거하도록 열 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 제거할 각 열에 대해 한 번씩 합니다. 에 대 한 열 이름을 지정 **@column**, 값이 **drop** 에 대 한 **@operation** 값 **1** 모두에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
2.  게시에 대해 스냅숏 에이전트 작업을 다시 실행하여 업데이트된 스냅숏을 생성합니다.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 참조 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 트랜잭션 복제 예제에서는 `DaysToManufacture` 테이블에 기반한 아티클에서 `Product` 열이 제거되었습니다.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 이 병합 복제 예제에서는 `CreditCardApprovalCode` 테이블에 기반한 아티클에서 `SalesOrderHeader` 열이 제거되었습니다.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## 참고 항목  
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)   
 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  