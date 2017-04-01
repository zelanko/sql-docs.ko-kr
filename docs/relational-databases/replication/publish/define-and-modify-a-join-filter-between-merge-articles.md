---
title: "병합 아티클 사이에서 조인 필터 정의 및 수정 | Microsoft Docs"
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
  - "필터 [SQL Server 복제], 조인"
  - "병합 복제 조인 필터 [SQL Server 복제]"
  - "필터 수정, 조인"
  - "조인 필터"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 병합 아티클 사이에서 조인 필터 정의 및 수정
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클 간의 조인 필터를 정의하고 수정하는 방법에 대해 설명합니다. 병합 복제는 조인 필터를 지원합니다. 조인 필터는 일반적으로 테이블 파티션을 다른 관련 테이블 아티클로 확장하기 위해 매개 변수가 있는 필터와 함께 사용됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클 간의 조인 필터를 정의하고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   조인 필터를 만들려면 게시에 최소한 두 개 이상의 관련 테이블이 포함되어야 합니다. 조인 필터는 행 필터를 확장하므로 다른 테이블과의 조인으로 필터를 확장하려면 한 테이블의 행 필터를 정의해야 합니다. 게시에 추가 관련 테이블이 포함되는 경우 한 조인 필터를 정의한 후에 다른 조인 필터를 사용하여 이 조인 필터를 확장할 수 있습니다.  
  
-   게시에 대한 구독이 초기화된 후 조인 필터를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅숏을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경에 대 한 요구 사항에 대 한 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   테이블 집합에 대한 조인 필터를 수동으로 만들거나 테이블에 정의된 외래 키와 기본 키 간의 관계를 기반으로 복제에서 필터를 자동으로 생성할 수 있습니다. 조인 필터 집합을 자동으로 생성에 대 한 자세한 내용은 참조 하십시오. [는 설정의 조인 필터 간의 병합 기사 및 #40; 자동으로 생성 SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 정의 수정 및 조인 필터에 삭제는 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 조인 필터를 정의하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 기존 행 필터를 선택 하거나 조인 필터는 **필터링 된 테이블** 창입니다.  
  
2.  **추가**를 클릭한 다음 **선택한 필터 확장을 위해 조인 추가**를 클릭합니다.  
  
3.  조인 문을 작성합니다. 새 조인을 추가하는 경우 **작성기를 사용하여 문 작성** 또는 **조인 문 직접 작성**을 선택합니다.  
  
    -   작성기를 사용 하 여 선택 하는 경우 열을 사용 하 여 표의 (**함께**, **필터링 된 테이블 열**, **연산자**, 및 **조인 된 테이블 열**) 조인 문을 작성 하 합니다.  
  
         눈금에서 각 열은 드롭다운 콤보 상자가 들어 있어 두 개의 열과 연산자를 선택할 수 있습니다 (**=**, **<>**, **<=**, **\<**, **>=**, **>**, 및 **같은**). 결과는 **미리 보기** 텍스트 영역에 표시됩니다. 조인에 둘 이상의 열 쌍을 포함 하는 경우에 결합을 선택 (또는 및 OR)에서 **함께** 열을 두 개 이상의 열과 연산자를 입력 합니다.  
  
    -   수동으로 문 작성을 선택하면 **조인 문** 텍스트 영역에 조인 문을 작성합니다. **필터링된 테이블 열** 목록 상자 및 **조인된 테이블 열** 목록 상자를 사용하여 열을 **조인 문** 텍스트 영역에 끌어다 놓습니다.  
  
    -   완전한 조인 문은 다음과 같습니다.  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 사용할 수 없습니다.  
  
4.  조인 옵션을 지정합니다.  
  
    -   필터링된 된 테이블 (부모 테이블)에서 조인 열이 고유한 경우 선택 **고유 키**합니다.  
  
        > [!CAUTION]  
        >  이 옵션을 선택하면 조인 필터에서의 자식 테이블과 부모 테이블 간의 관계가 일대일 또는 일대다가 됩니다. 자식 테이블에 있는 조인 열이 고유해야 하는 경우에만 이 옵션을 선택합니다. 이 옵션이 잘못 설정되면 데이터가 일치하지 않을 수 있습니다.  
  
    -   기본적으로 병합 복제는 동기화 과정에서 행별로 변경 내용을 처리합니다. 관련 변경 내용을 필터링 된 테이블과 조인된 된 테이블을 하나의 단위로 처리의 행에, 선택 **논리적 레코드** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전만 해당). 논리적 레코드를 사용하기 위한 아티클 및 게시 요구 사항이 충족되는 경우에만 이 옵션을 사용할 수 있습니다. 자세한 내용은 "고려 사항에 대 한 논리적 레코드 사용" 섹션을 참조 [그룹 변경 내용을 논리적 레코드와 관련 된 행에](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 조인 필터를 수정하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 에서 필터는 **필터링 된 테이블** 창과 클릭 한 다음 **편집**합니다.  
  
2.  **조인 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 조인 필터를 삭제하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 에서 필터는 **필터링 된 테이블** 창과 클릭 한 다음 **삭제**합니다. 삭제하는 조인 필터가 다른 조인에 의해 확장된 경우 해당 조인 또한 삭제됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 다음 절차에서는 부모 아티클의 매개 변수가 있는 필터 및 이 아티클과 관련 자식 아티클 간의 조인 필터를 보여 줍니다. 조인 필터는 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 정의 및 수정할 수 있습니다.  
  
#### 아티클 필터를 병합 복제의 관련 아티클로 확장하도록 조인 필터를 정의하려면  
  
1.  조인되는 아티클, 즉 부모 아티클에 대한 필터링을 정의합니다.  
  
    -   매개 변수가 있는 행 필터를 사용하여 필터링되는 아티클의 경우 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
    -   정적 행 필터를 사용하여 필터링되는 아티클의 경우 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 하나 이상의 관련된 아티클, 즉 라 하 고 게시에 대 한 자식 아티클을 정의 합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_addmergefilter (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)합니다. 지정 **@publication**, 이 필터에 대 한 고유한 이름을 **@filtername**, 에 대해 2 단계에서 만든 자식 아티클의 이름을 **@article**, 에 대 한 조인 되는 부모 아티클의 이름을 **@join_articlename**, 는 다음 값 중 하나에 대 한 고 **@join_unique_key**:  
  
    -   **0** -부모 아티클과 자식 아티클 간의 다 대 일 또는 다 대 다 조인을 나타냅니다.  
  
    -   **1** -부모 아티클과 자식 아티클 간의 한 한 일 대 다 조인을 나타냅니다.  
  
     이는 두 아티클 간의 조인 필터를 정의합니다.  
  
    > [!CAUTION]  
    >  설정만 **@join_unique_key** 에 **1** 는 제약 조건을 조인 열에 고유성을 보장 하는 부모 아티클의 기본 테이블에 있는 경우. 경우 **@join_unique_key** 로 설정 된 **1** 올바르게 데이터의 일치성 하지 발생할 수 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 정적 행 필터를 사용하여 자체 필터링되는 `SalesOrderDetail` 테이블에 대해 `SalesOrderHeader` 테이블 아티클을 필터링하는 병합 게시에 대한 아티클을 정의합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 이 예제에서는 일련의 조인 필터에 대해 아티클이 필터링 된 병합 게시에서의 아티클 그룹 정의 `Employee` 테이블에 자체의 값에는 매개 변수가 있는 행 필터를 사용 하 여 필터링 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 에 **LoginID** 열입니다. 자세한 내용은 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## 참고 항목  
 [조인 필터](../../../relational-databases/replication/merge/join-filters.md)   
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [방법: (SQL Server Management Studio) 병합 아티클 간의 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  