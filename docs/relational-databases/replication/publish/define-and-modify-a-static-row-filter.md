---
description: 정적 행 필터 정의 및 수정
title: 정적 행 필터 정의 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying filters, static row
- static row filters
- filters [SQL Server replication], static row
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 626665bff61cd6f0c1799ef52134c50688d962b6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477734"
---
# <a name="define-and-modify-a-static-row-filter"></a>정적 행 필터 정의 및 수정
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 정적 행 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 정적 행 필터를 정의하고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   게시에 대한 구독이 초기화된 후 정적 행 필터를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅샷을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경 요구 사항에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
-   게시에서 피어 투 피어 트랜잭션 복제를 사용할 수 있도록 설정한 경우에는 테이블을 필터링할 수 없습니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이러한 필터는 정적이므로 모든 구독자가 데이터의 동일한 하위 집합을 받습니다. 병합 게시에 속한 테이블 아티클에서 동적으로 행을 필터링하여 각 구독자가 서로 다른 데이터 파티션을 받게 하려면 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요. 병합 게시에서도 기존 행 필터에 따라 관련 행을 필터링할 수 있습니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자의 **행 필터** 페이지에서 정적 행 필터를 정의, 수정 및 삭제합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-define-a-static-row-filter"></a>정적 행 필터를 정의하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자의 **행 필터** 페이지에서 수행하는 작업은 게시 유형에 따라 달라집니다.  
  
    -   스냅샷 또는 트랜잭션 게시의 경우 **추가** 를 클릭합니다.  
  
    -   병합 게시의 경우 **추가** 를 클릭한 다음 **필터 추가** 를 클릭합니다.  
  
2.  **필터 추가** 대화 상자의 드롭다운 목록 상자에서 필터링할 테이블을 선택합니다.  
  
3.  **필터 문** 텍스트 영역에서 필터 문을 만듭니다. 텍스트 영역에 직접 입력할 수도 있고 **열** 목록 상자에서 열을 끌어서 놓을 수도 있습니다.  
  
    > [!NOTE]  
    >  WHERE 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 지원되지 않습니다. Oracle 게시자의 게시인 경우 WHERE 절은 Oracle 구문과 호환되어야 합니다.  
  
    -   **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
        ```sql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   기본 텍스트는 변경할 수 없습니다. 표준 SQL 구문을 사용하여 WHERE 키워드 뒤에 필터 절을 입력합니다. 전체 필터 절은 다음과 같습니다.  
  
        ```sql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   정적 행 필터에는 사용자 정의 함수가 포함될 수 있습니다. 사용자 정의 함수가 있는 정적 행 필터에 대한 전체 필터 절은 다음과 같습니다.  
  
        ```sql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **게시 속성 - \<Publication>** 대화 상자에서 **확인** 을 클릭하여 저장하고 대화 상자를 닫습니다.  

#### <a name="to-modify-a-static-row-filter"></a>정적 행 필터를 수정하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **편집** 을 클릭합니다.  
  
2.  **필터 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-static-row-filter"></a>정적 행 필터를 삭제하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **삭제** 를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 테이블 아티클을 만들 때 WHERE 절을 정의하여 아티클에서 행을 필터링할 수 있습니다. 정의한 행 필터를 변경할 수도 있습니다. 복제 저장 프로시저를 사용하면 정적 행 필터를 프로그래밍 방식으로 만들거나 수정할 수 있습니다.  
  
#### <a name="to-define-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 대한 정적 행 필터를 정의하려면  
  
1.  필터링할 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [sp_articlefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)를 실행합니다. 이때 **\@article** 에 아티클 이름, **\@publication** 에 게시 이름, **\@filter_name** 에 필터 이름, **\@filter_clause** 에 필터링 절(`WHERE`를 포함하지 않음)을 지정합니다.  
  
3.  계속 열 필터를 정의하려면 [열 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요. 그러지 않으면 [sp_articleview&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)를 실행합니다. 이때 **\@publication** 에 게시 이름, **\@article** 에 필터링된 아티클 이름, **\@filter_clause** 에 2단계에서 지정한 필터 절을 지정합니다. 이렇게 하면 필터링된 아티클에 대한 동기화 개체가 만들어집니다.  
  
#### <a name="to-modify-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 대한 정적 행 필터를 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_articlefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)를 실행합니다. 이때 **\@article** 에 아티클 이름, **\@publication** 에 게시 이름, **\@filter_name** 에 새 필터 이름, **\@filter_clause** 에 새 필터링 절(`WHERE`를 포함하지 않음)을 지정합니다. 이와 같이 변경하면 기존 구독의 데이터가 무효화되므로 **\@force_reinit_subscription** 에 **1** 값을 지정합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_articleview&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)를 실행합니다. 이때 **\@publication** 에 게시 이름, **\@article** 에 필터링된 아티클 이름, **\@filter_clause** 에 1단계에서 지정한 필터 절을 지정합니다. 이렇게 하면 필터링된 아티클을 정의하는 뷰가 다시 만들어집니다.  
  
3.  게시에 대해 스냅샷 에이전트 작업을 다시 실행하여 업데이트된 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
4.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="to-delete-a-static-row-filter-for-a-snapshot-or-transactional-publication"></a>스냅샷 또는 트랜잭션 게시에 대한 정적 행 필터를 삭제하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_articlefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)를 실행합니다. 이때 **\@article** 에 아티클 이름, **\@publication** 에 게시 이름, **\@filter_name** 에 NULL 값, **\@filter_clause** 에 NULL 값을 지정합니다. 이와 같이 변경하면 기존 구독의 데이터가 무효화되므로 **\@force_reinit_subscription** 에 **1** 값을 지정합니다.  
  
2.  게시에 대해 스냅샷 에이전트 작업을 다시 실행하여 업데이트된 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
#### <a name="to-define-a-static-row-filter-for-a-merge-publication"></a>병합 게시에 대한 정적 행 필터를 정의하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. 이때 **\@subset_filterclause** 에 필터링 절( `WHERE`를 포함하지 않음)을 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  계속 열 필터를 정의하려면 [열 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요.  
  
#### <a name="to-modify-a-static-row-filter-for-a-merge-publication"></a>병합 게시에 대한 정적 행 필터를 수정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. 이때 **\@publication** 에 게시 이름, **\@article** 에 필터링된 아티클 이름, **\@property** 에 **subset_filterclause** 값, **\@value** 에 새 필터링 절(`WHERE`를 포함하지 않음)을 지정합니다. 이와 같이 변경하면 기존 구독의 데이터가 무효화되므로 **\@force_reinit_subscription** 에 1 값을 지정합니다.  
  
2.  게시에 대해 스냅샷 에이전트 작업을 다시 실행하여 업데이트된 스냅샷을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
3.  구독을 다시 초기화합니다. 자세한 내용은 [구독 다시 초기화](../../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 트랜잭션 복제 예에서는 지원되지 않는 모든 제품을 제거하도록 아티클을 행 필터링합니다.  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 다음 병합 복제 예에서는 지정된 영업 사원에 속한 행만 반환하도록 아티클을 행 필터링하고 조인 필터도 사용합니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)   
 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
