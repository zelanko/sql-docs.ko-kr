---
title: 병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/02/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], defining
- parameterized filters [SQL Server replication], modifying
- merge replication [SQL Server replication], dynamic filters
- merge replication parameterized filters [SQL Server replication]
- filters [SQL Server replication], parameterized
- modifying filters, parameterized row
- dynamic filters [SQL Server replication]
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86a96f938a036edf39b3602278f9b6b6d2d46719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212113"
---
# <a name="define-and-modify-a-parameterized-row-filter-for-a-merge-article"></a>병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 매개 변수가 있는 행 필터를 정의하고 수정하는 방법에 대해 설명합니다.  
  
 테이블 아티클을 만들 때 매개 변수가 있는 행 필터를 사용할 수 있습니다. 이러한 필터에서는 게시할 해당 데이터를 선택하기 위해 [WHERE](/sql/t-sql/queries/where-transact-sql) 절을 사용합니다. 정적 행 필터와는 달리 해당 절에 리터럴 값을 지정하는 대신 [SUSER_SNAME](/sql/t-sql/functions/suser-sname-transact-sql) 및 [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql) 시스템 함수를 하나 또는 둘 모두 지정합니다. 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
 
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   게시에 대한 구독이 초기화된 후 매개 변수가 있는 행 필터를 추가, 수정 또는 삭제한 경우에는 변경 내용을 적용한 후에 새 스냅샷을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경 요구 사항에 대한 자세한 내용은 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)을 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 필터 절에 HOST_NAME을 사용하고 HOST_NAME 값을 재지정할 경우 CONVERT를 사용하여 데이터 형식을 변환해야 할 수 있습니다. 이를 위한 최선의 구현 방법은 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)항목의 "HOST_NAME() 값 재정의" 섹션을 참조하십시오.  
  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에서 매개 변수가 있는 행 필터를 정의, 수정 및 삭제합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-define-a-parameterized-row-filter"></a>매개 변수가 있는 행 필터를 정의하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 의 **행 필터** 페이지에서 **추가**를 클릭하고 **필터 추가**를 클릭합니다.  
  
2.  **필터 추가** 대화 상자의 드롭다운 목록 상자에서 필터링할 테이블을 선택합니다.  
  
3.  **필터 문** 입력란에서 필터 문을 만듭니다. 텍스트 영역에 직접 입력할 수도 있고 **열** 목록 상자에서 열을 끌어서 놓을 수도 있습니다.  
  
    -   **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   기본 텍스트는 변경할 수 없습니다. 표준 SQL 구문을 사용하여 WHERE 키워드 뒤에 필터 절을 입력합니다. 매개 변수가 있는 필터는 `HOST_NAME()` 및/또는 `SUSER_SNAME()` 시스템 함수 또는 이러한 함수 중 하나 또는 둘 다를 참조하는 사용자 정의 함수에 대한 호출을 포함합니다. 다음 예에서는 매개 변수가 있는 행 필터에 대한 전체 필터 절입니다.  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 지원되지 않습니다.  
  
4.  구독자 간에 데이터를 공유하는 방식과 일치하는 옵션을 선택합니다.  
  
    -   **이 테이블의 행을 여러 구독으로 이동**  
  
    -   **이 테이블의 행을 단일 구독으로 이동**  
  
     **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서는 보다 작은 메타데이터를 저장하고 처리하여 성능을 최적화할 수 있습니다. 그러나 한 행이 둘 이상의 구독자로 복제될 수 없도록 데이터가 분할되어야 합니다. 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-modify-a-parameterized-row-filter"></a>매개 변수가 있는 행 필터를 수정하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **편집**을 클릭합니다.  
  
2.  **필터 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-parameterized-row-filter"></a>매개 변수가 있는 행 필터를 삭제하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **삭제**를 클릭합니다.  
  

  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 매개 변수가 있는 행 필터를 프로그래밍 방식으로 만들거나 수정할 수 있습니다.  
  
#### <a name="to-define-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>병합 게시에서 아티클에 대한 매개 변수가 있는 행 필터를 정의하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행합니다. **@publication** 을 지정하고 **@article** 에 아티클 이름을, **@source_object** 에 게시되는 테이블을, **@subset_filterclause** 에 매개 변수가 있는 필터를 정의하는 WHERE 절(`WHERE` 제외)을, **@partition_options** 에 매개 변수가 있는 행 필터의 결과에 따른 분할 유형을 정의하는 다음 값 중 하나를 지정합니다.  
  
    -   **0** - 아티클의 필터링이 정적이거나 각 파티션에 대한 데이터의 고유 하위 집합을 생성합니다. 즉 "겹치는" 파티션을 생성하지 않습니다.  
  
    -   **1** - 결과 파티션이 겹치며 구독자에 변경된 내용이 있어도 행이 속한 파티션이 변경되지 않습니다.  
  
    -   **2** - 아티클을 필터링하면 겹치지 않는 파티션이 생성되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.  
  
    -   **3** - 아티클을 필터링하면 각 구독에 고유한 겹치지 않는 파티션이 생성됩니다.  
  
#### <a name="to-change-a-parameterized-row-filter-for-an-article-in-a-merge-publication"></a>병합 게시에서 아티클에 대한 매개 변수가 있는 행 필터를 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 실행합니다. 지정 **@publication** 를 **@article** 에 값 `subset_filterclause` 에 대 한 **@property** 에 대 한 매개 변수가 있는 필터를 정의 하는 식 **@value** (제외한 `WHERE`), 값 **1** 모두에 대 한 **@force_invalidate_snapshot** 하 고 **@force_reinit_subscription** .  
  
2.  이 변경 내용으로 인해 파티션에 변화가 생기면 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) 을 다시 실행합니다. 지정 **@publication** 를 **@article** 에 값 `partition_options` 에 대 한 **@property** , 및 가장적합한분할옵션을 **@value** , 다음 중 하나일 수 있습니다.  
  
    -   **0** - 아티클의 필터링이 정적이거나 각 파티션에 대한 데이터의 고유 하위 집합을 생성합니다. 즉 "겹치는" 파티션을 생성하지 않습니다.  
  
    -   **1** - 결과 파티션이 겹치며 구독자에 변경된 내용이 있어도 행이 속한 파티션이 변경되지 않습니다.  
  
    -   **2** - 아티클을 필터링하면 겹치지 않는 파티션이 생성되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.  
  
    -   **3** - 아티클을 필터링하면 각 구독에 고유한 겹치지 않는 파티션이 생성됩니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 병합 게시의 아티클 그룹을 정의합니다. 이 병합 게시에서는 `Employee` LoginID **열을 기준으로 매개 변수가 있는 행 필터를 사용하여 자체 필터링되는** 테이블에 대해 일련의 조인 필터로 아티클이 필터링됩니다. 동기화 중에 [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql) 함수에서 반환하는 값은 재정의됩니다. 자세한 내용은 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)항목의 HOST_NAME() 값 재정의를 참조하십시오.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubdynamic1.sql#sp_mergedynamicpub1)]  
  
  
## <a name="see-also"></a>관련 항목  
 [병합 아티클 사이에서 조인 필터 정의 및 수정](define-and-modify-a-join-filter-between-merge-articles.md)   
 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)   
 [Join Filters](../merge/join-filters.md)   
 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
