---
title: 병합 아티클 사이에서 조인 필터 정의 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- merge replication join filters [SQL Server replication]
- modifying filters, join
- join filters
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf7d996475800dfc34e472b42e76aa86696c0345
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="define-and-modify-a-join-filter-between-merge-articles"></a>병합 아티클 사이에서 조인 필터 정의 및 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클 간의 조인 필터를 정의하고 수정하는 방법에 대해 설명합니다. 병합 복제는 조인 필터를 지원합니다. 조인 필터는 일반적으로 테이블 파티션을 다른 관련 테이블 아티클로 확장하기 위해 매개 변수가 있는 필터와 함께 사용됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클 간의 조인 필터를 정의하고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   조인 필터를 만들려면 게시에 최소한 두 개 이상의 관련 테이블이 포함되어야 합니다. 조인 필터는 행 필터를 확장하므로 다른 테이블과의 조인으로 필터를 확장하려면 한 테이블의 행 필터를 정의해야 합니다. 게시에 추가 관련 테이블이 포함되는 경우 한 조인 필터를 정의한 후에 다른 조인 필터를 사용하여 이 조인 필터를 확장할 수 있습니다.  
  
-   게시에 대한 구독이 초기화된 후 조인 필터를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅숏을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경 요구 사항에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   테이블 집합에 대한 조인 필터를 수동으로 만들거나 테이블에 정의된 외래 키와 기본 키 간의 관계를 기반으로 복제에서 필터를 자동으로 생성할 수 있습니다. 조인 필터 집합을 자동으로 생성하는 방법에 대한 자세한 내용은 [병합 아티클 간의 조인 필터 집합 자동 생성&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에서 조인 필터를 정의, 수정 및 삭제합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-define-a-join-filter"></a>조인 필터를 정의하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 기존 행 필터 또는 조인 필터를 선택합니다.  
  
2.  **추가**를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
3.  조인 문을 작성합니다. 새 조인을 추가하는 경우 **작성기를 사용하여 문 작성** 또는 **조인 문 직접 작성**을 선택합니다.  
  
    -   작성기 사용을 선택하면 표의 열(**결합**, **필터링된 테이블 열**, **연산자**및 **조인된 테이블 열**)을 사용하여 조인 문을 작성합니다.  
  
         표의 각 열에는 드롭다운 콤보 상자가 들어 있습니다. 여기서 두 개의 열과 연산자 1개(**=**, **<>**, **<=**, **\<**, **>=**, **>** 및 **like**)를 선택할 수 있습니다. 결과는 **미리 보기** 텍스트 영역에 표시됩니다. 조인이 둘 이상의 열 쌍을 포함하면 **결합** 열에서 결합(AND 또는 OR)을 선택한 다음 두 개 이상의 열과 연산자를 입력합니다.  
  
    -   수동으로 문 작성을 선택하면 **조인 문** 텍스트 영역에 조인 문을 작성합니다. **필터링된 테이블 열** 목록 상자 및 **조인된 테이블 열** 목록 상자를 사용하여 열을 **조인 문** 텍스트 영역에 끌어다 놓습니다.  
  
    -   완전한 조인 문은 다음과 같습니다.  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 사용할 수 없습니다.  
  
4.  조인 옵션을 지정합니다.  
  
    -   필터링된 테이블(부모 테이블)에서 조인하는 열이 고유하면 **고유 키**를 선택합니다.  
  
        > [!CAUTION]  
        >  이 옵션을 선택하면 조인 필터에서의 자식 테이블과 부모 테이블 간의 관계가 일대일 또는 일대다가 됩니다. 자식 테이블에 있는 조인 열이 고유해야 하는 경우에만 이 옵션을 선택합니다. 이 옵션이 잘못 설정되면 데이터가 일치하지 않을 수 있습니다.  
  
    -   기본적으로 병합 복제는 동기화 과정에서 행별로 변경 내용을 처리합니다. 필터링된 테이블과 조인된 테이블 행의 관련 변경 내용을 하나의 단위로 처리하려면 **논리적 레코드** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후 버전에서만 제공). 논리적 레코드를 사용하기 위한 아티클 및 게시 요구 사항이 충족되는 경우에만 이 옵션을 사용할 수 있습니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)에서 "논리적 레코드 사용 시 고려 사항" 섹션을 참조하세요.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-modify-a-join-filter"></a>조인 필터를 수정하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **편집**을 클릭합니다.  
  
2.  **조인 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-join-filter"></a>조인 필터를 삭제하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **삭제**를 클릭합니다. 삭제하는 조인 필터가 다른 조인에 의해 확장된 경우 해당 조인 또한 삭제됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 다음 절차에서는 부모 아티클의 매개 변수가 있는 필터 및 이 아티클과 관련 자식 아티클 간의 조인 필터를 보여 줍니다. 조인 필터는 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 정의 및 수정할 수 있습니다.  
  
#### <a name="to-define-a-join-filter-to-extend-an-article-filter-to-related-articles-in-a-merge-publication"></a>아티클 필터를 병합 복제의 관련 아티클로 확장하도록 조인 필터를 정의하려면  
  
1.  조인되는 아티클, 즉 부모 아티클에 대한 필터링을 정의합니다.  
  
    -   매개 변수가 있는 행 필터를 사용하여 필터링되는 아티클의 경우 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
    -   정적 행 필터를 사용하여 필터링되는 아티클의 경우 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 게시에 대한 하나 이상의 관련 아티클, 즉 자식 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addmergefilter&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)를 실행합니다. **@publication**을 지정하고 **@filtername**에 이 필터에 대한 고유한 이름을, **@article**에 2단계에서 만든 자식 아티클의 이름을, **@join_articlename**에 조인되는 부모 아티클의 이름을, **@join_unique_key**에 다음 값 중 하나를 지정합니다.  
  
    -   **0** - 부모 아티클과 자식 아티클 간의 다 대 일 또는 다 대 다 조인을 나타냅니다.  
  
    -   **1** - 부모 아티클과 자식 아티클 간의 일 대 일 또는 일 대 다 조인을 나타냅니다.  
  
     이는 두 아티클 간의 조인 필터를 정의합니다.  
  
    > [!CAUTION]  
    >  부모 아티클의 기반 테이블에 있는 조인 열에 고유성을 보장하는 제약 조건이 있는 경우에만 **@join_unique_key** 를 **1** 로 설정하세요. **@join_unique_key**를 **1**로 설정하면 데이터가 일치하지 않을 수 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 정적 행 필터를 사용하여 자체 필터링되는 `SalesOrderDetail` 테이블에 대해 `SalesOrderHeader` 테이블 아티클을 필터링하는 병합 게시에 대한 아티클을 정의합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 다음 예에서는 병합 게시의 아티클 그룹을 정의합니다. 이 병합 게시에서는 `Employee` LoginID [열의](../../../t-sql/functions/host-name-transact-sql.md) HOST_NAME **값을 대상으로 매개 변수가 있는 행 필터를 사용하여 자체 필터링되는** 테이블에 대해 일련의 조인 필터로 아티클이 필터링됩니다. 자세한 내용은 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [조인 필터](../../../relational-databases/replication/merge/join-filters.md)   
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [방법: 병합 아티클 간의 조인 필터 정의 및 수정(SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  
