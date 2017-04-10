---
title: "병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정 | Microsoft Docs"
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
  - "매개 변수가 있는 필터 [SQL Server 복제], 정의"
  - "매개 변수가 있는 필터 [SQL Server 복제], 수정"
  - "병합 복제 [SQL Server 복제], 동적 필터"
  - "병합 복제 매개 변수가 있는 필터 [SQL Server 복제]"
  - "필터 [SQL Server 복제], 매개 변수가 있는"
  - "필터 수정, 매개 변수가 있는 행"
  - "동적 필터 [SQL Server 복제]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 매개 변수가 있는 행 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
 테이블 아티클을 만들 때 매개 변수가 있는 행 필터를 사용할 수 있습니다. 이러한 필터에서는 게시할 해당 데이터를 선택하기 위해 [WHERE](../../../t-sql/queries/where-transact-sql.md) 절을 사용합니다. (작업할 때 처럼 정적 행 필터) 절에 리터럴 값을 지정 하는 대신, 다음 시스템 함수 중 하나 또는 모두를 지정: [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) 및 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 매개 변수가 있는 행 필터를 정의하고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시에 대한 구독이 초기화된 후 매개 변수가 있는 행 필터를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅숏을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경에 대 한 요구 사항에 대 한 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 필터 절에 HOST_NAME을 사용하고 HOST_NAME 값을 재지정할 경우 CONVERT를 사용하여 데이터 형식을 변환해야 할 수 있습니다. 이 경우에 대 한 모범 사례에 대 한 자세한 내용은 항목의 "host_name () 값 재정의" 섹션을 참조 하십시오. [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 정의 수정 및에 매개 변수가 있는 행 필터를 삭제는 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 매개 변수가 있는 행 필터를 정의하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 클릭 **추가**, 를 클릭 하 고 **필터 추가**합니다.  
  
2.  에 **필터 추가** 대화 상자, 드롭 다운 목록 상자에서 필터링 할 테이블을 선택 합니다.  
  
3.  **필터 문** 입력란에서 필터 문을 만듭니다. 텍스트 영역에 직접 입력할 수도 있고 **열** 목록 상자에서 열을 끌어서 놓을 수도 있습니다.  
  
    -   **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   기본 텍스트는 변경할 수 없습니다. 표준 SQL 구문을 사용하여 WHERE 키워드 뒤에 필터 절을 입력합니다. 시스템 함수에 대 한 호출을 포함 하는 매개 변수가 있는 필터 **host_name ()** 및/또는 **suser_sname ()**, 또는 이러한 함수 중 하나 또는 모두를 참조 하는 사용자 정의 함수입니다. 다음 예에서는 매개 변수가 있는 행 필터에 대한 전체 필터 절입니다.  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 지원되지 않습니다.  
  
4.  구독자 간에 데이터를 공유하는 방식과 일치하는 옵션을 선택합니다.  
  
    -   **이 테이블의 행을 여러 구독으로 이동**  
  
    -   **이 테이블의 행을 단일 구독으로 이동**  
  
     **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서는 보다 작은 메타데이터를 저장하고 처리하여 성능을 최적화할 수 있습니다. 그러나 한 행이 둘 이상의 구독자로 복제될 수 없도록 데이터가 분할되어야 합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 매개 변수가 있는 행 필터를 수정하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 에서 필터는 **필터링 된 테이블** 창과 클릭 한 다음 **편집**합니다.  
  
2.  **필터 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 매개 변수가 있는 행 필터를 삭제하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>**, 에서 필터는 **필터링 된 테이블** 창과 클릭 한 다음 **삭제**합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 매개 변수가 있는 행 필터를 프로그래밍 방식으로 만들거나 수정할 수 있습니다.  
  
#### 병합 게시에서 아티클에 대한 매개 변수가 있는 행 필터를 정의하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 에 대 한 게시 되는 테이블 **@source_object**, WHERE 절에 대 한 매개 변수가 있는 필터를 정의 하는 **@subset_filterclause** (포함 하지 않는 `WHERE`)는 다음 값 중 하나에 대 한 고 **@partition_options**, 를 설명 하는 매개 변수가 있는 행 필터에서 결과인 분할의 유형:  
  
    -   **0** -필터링 된 아티클의 정적 이거나 각 파티션에 ("겹치는" 파티션)에 대 한 데이터의 고유 하위 집합을 생성 하지 않습니다.  
  
    -   **1** -결과 파티션이 겹치며 구독자에서 업데이트 한 행이 속한 파티션을 변경할 수 없습니다.  
  
    -   **2** -아티클을 필터링 겹치지 않는 파티션이 생성 되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.  
  
    -   **3** -각 구독에 대해 고유한 문서 생성 겹치지 않는 파티션에 대 한 필터링 합니다.  
  
#### 병합 게시에서 아티클에 대한 매개 변수가 있는 행 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 지정 **@publication**, **@article**, 값이 **subset_filterclause** 에 대 한 **@property**, 에 대 한 매개 변수가 있는 필터를 정의 하는 식 **@value** (포함 하지 않고 `WHERE`), 및의 값 **1** 모두에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
2.  이 변경으로 인해 다른 분할 동작을 하는 경우 다음 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 다시 합니다. 지정 **@publication**, **@article**, 값이 **partition_options** 에 대 한 **@property**, 및에 대 한 가장 적합 한 분할 옵션 **@value**, 다음 중 하나일 수 있습니다.  
  
    -   **0** -필터링 된 아티클의 정적 이거나 각 파티션에 ("겹치는" 파티션)에 대 한 데이터의 고유 하위 집합을 생성 하지 않습니다.  
  
    -   **1** -결과 파티션이 겹치며 구독자에서 업데이트 한 행이 속한 파티션을 변경할 수 없습니다.  
  
    -   **2** -아티클을 필터링 겹치지 않는 파티션이 생성 되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.  
  
    -   **3** -각 구독에 대해 고유한 문서 생성 겹치지 않는 파티션에 대 한 필터링 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 병합 게시의 아티클 그룹을 정의합니다. 이 병합 게시에서는 `Employee` LoginID **열을 기준으로 매개 변수가 있는 행 필터를 사용하여 자체 필터링되는** 테이블에 대해 일련의 조인 필터로 아티클이 필터링됩니다. 동기화 하는 동안 반환한 값은 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 함수가 재정의 됩니다. 자세한 내용은 참조 항목의 host_name () 값 재정의 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)합니다.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## 참고 항목  
 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [조인 필터](../../../relational-databases/replication/merge/join-filters.md)   
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  