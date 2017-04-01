---
title: "매개 변수가 있는 행 필터 최적화 | Microsoft Docs"
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
  - "사전 계산 파티션 [SQL Server 복제]"
  - "필터 [SQL Server 복제], 매개 변수가 있는"
  - "병합 복제 사전 계산 파티션 [SQL Server 복제], SQL Server Management Studio"
  - "매개 변수가 있는 필터 [SQL Server 복제], 최적화"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 매개 변수가 있는 행 필터 최적화
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 매개 변수가 있는 행 필터를 최적화하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **매개 변수가 있는 행 필터를 최적화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   매개 변수가 있는 필터를 사용하는 경우 게시를 만들 때 **use partition groups** 옵션 또는 **keep partition changes** 옵션을 지정하여 병합 복제에서 필터가 처리되는 방법을 제어할 수 있습니다. 이러한 옵션은 게시 데이터베이스에 추가 메타데이터를 저장함으로써 필터링된 아티클이 있는 게시의 동기화 성능을 개선합니다. 아티클을 만들 때 **partition options** 를 설정하면 구독자 간에 데이터가 공유되는 방법을 제어할 수 있습니다. 이러한 요구 사항에 대한 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)를 참조하세요.  
  
     삭제가 올바르게 전파되도록 보장하려면 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact 구독자에서 keep_partition_changes를 true로 설정해야 합니다. false로 설정한 경우 구독자에 예상한 것보다 많은 행이 포함될 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 설정을 사용하여 매개 변수가 있는 행 필터를 최적화할 수 있습니다.  
  
 **파티션 옵션**  
 이 옵션을 설정는 **속성** 의 페이지는 **아티클 속성-\< 아티클>** 대화 상자 또는 **필터 추가** 대화 상자. 두 대화 상자는 새 게시 마법사에서 사용할 수 있는 고 **게시 속성-\< 게시>** 대화 상자입니다.  **아티클 속성-\< 아티클>** 대화 상자에서 사용할 수 없는이 옵션에 대 한 추가 값을 지정할 수 있습니다는 **필터 추가** 대화 상자입니다.  
  
 **파티션 미리 계산**  
 이 옵션 설정 **True** 게시의 아티클에 요구 사항 준수 하는 경우 기본적으로 합니다. 이러한 요구 사항에 대 한 자세한 내용은 참조 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)합니다. 이 옵션을 수정 된 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다.  
  
 **동기화 최적화**  
 이 옵션 설정 해야 **True** 경우에만 **파티션 미리 계산** 로 설정 된 **False**합니다. 이 옵션을 설정 된 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자입니다.  
  
 새 게시 마법사를 사용 하 고 액세스 하는 방법에 대 한 자세한 내용은 **게시 속성-\< 게시>** 대화 상자, 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 필터 추가 또는 필터 편집 대화 상자에서 파티션 옵션을 설정하려면  
  
1.  에 **테이블 행 필터** 새 게시 마법사의 페이지 또는 **행 필터** 의 페이지는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **추가**, 클릭 하 고 **필터 추가**.  
  
2.  매개 변수가 있는 필터를 만듭니다. 자세한 내용은 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
3.  구독자 간에 데이터를 공유하는 방식과 일치하는 옵션을 선택합니다.  
  
    -   **이 테이블의 행을 여러 구독으로 이동**  
  
    -   **이 테이블의 행을 단일 구독으로 이동**  
  
     **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서는 보다 작은 메타데이터를 저장하고 처리하여 성능을 최적화할 수 있습니다. 그러나 한 행이 둘 이상의 구독자로 복제될 수 없도록 데이터가 분할되어야 합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 아티클 속성-에서 파티션 옵션을 설정 하려면 \< 문서> 대화 상자  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성**합니다.  
  
2.  **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **대상 개체** 의 섹션은 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자에 다음 값 중 하나를 지정 합니다 **파티션 옵션**:  
  
    -   **겹침**  
  
    -   **겹침, 파티션 외부 데이터 변경 내용 허용 안 함**  
  
    -   **겹치지 않음, 단일 구독**  
  
    -   **겹치지 않음, 구독 간 공유**  
  
     이러한 옵션 및 이 옵션이 **필터 추가** 및 **필터 편집** 대화 상자에서 사용 가능한 옵션과 어떻게 관련되어 있는지에 대한 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)의 "'partition options' 설정" 섹션을 참조하십시오.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 파티션 미리 계산을 설정하려면  
  
1.  에 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 선택에 대 한 값의 **파티션 미리 계산** 옵션입니다. 다음과 같은 경우 이 속성은 읽기 전용입니다.  
  
    -   게시가 사전 계산 파티션의 요구 사항을 충족시키지 못합니다.  
  
    -   게시에 대한 스냅숏이 아직 생성되지 않았습니다. 이 경우 해당 옵션은 **스냅숏 생성 시기 자동 설정**의 값을 표시합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 동기화 최적화를 설정하려면  
  
1.  에 **구독 옵션** 의 페이지는 **게시 속성-\< 게시>** 대화 상자에서 값 선택 **True** 에 대 한는 **동기화 최적화** 옵션입니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 에 대 한 필터링 옵션의 정의 대 한 **@keep_partition_changes** 및 **@use_partition_groups**, 참조 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다.  
  
#### 새 게시를 만들 때 병합 필터 최적화를 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)합니다. **@publication** 을 지정하고 다음 매개 변수 중 하나에 **true** 값을 지정합니다.  
  
    -   **@use_partition_groups**:-제공 문서 사전 계산 파티션의 요구 사항을 충족 하는 가장 높은 성능 최적화 합니다. 자세한 내용은 참조 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)합니다.  
  
    -   **@keep_partition_changes** -파티션을 사용할 수 없는 사전 계산 하는 경우이 최적화를 사용 합니다.  
  
2.  게시에 대한 스냅숏 작업을 추가합니다. 자세한 내용은 참조 [발행물 만들기](../../../relational-databases/replication/publish/create-a-publication.md)합니다.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), 다음 매개 변수를 지정 합니다.  
  
    -   **@publication** -1 단계에서 게시의 이름입니다.  
  
    -   **@article** -아티클의 이름  
  
    -   **@source_object** -게시 되는 데이터베이스 개체입니다.  
  
    -   **@subset_filterclause** -아티클을 행 필터링 하는 데 사용 되는 선택적 매개 변수가 있는 필터 절.  
  
    -   **@partition_options** -필터링 된 아티클에 대 한 파티션 옵션.  
  
4.  게시의 각 아티클에 대해 3단계를 반복합니다.  
  
5.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 두 아티클 간의 조인 필터를 정의할 수 있습니다. 자세한 내용은 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
#### 기존 게시에 대한 병합 필터 동작을 확인 및 수정하려면  
  
1.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), 로 지정 하 여 **@publication**합니다. 값을 확인 **keep_partition_changes** 및 **use_partition_groups** 결과 집합에 있습니다.  
  
2.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)합니다. 값을 지정 **use_partition_groups** 에 대 한 **@property** 와 **true** 또는 **false** 에 대 한 **@value**합니다.  
  
3.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)합니다. 값을 지정 **keep_partition_changes** 에 대 한 **@property** 와 **true** 또는 **false** 에 대 한 **@value**합니다.  
  
    > [!NOTE]  
    >  사용 하도록 설정할 때 **keep_partition_changes**, 을 먼저 해제 해야 **use_partition_groups** 값을 지정 하 고 **1** 에 대 한 **@force_reinit_subscription**합니다.  
  
4.  (선택 사항) 게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **partition_options** 에 대 한 **@property** 및에 대 한 적절 한 값 **@value**합니다. 참조 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 이러한 정의 대 한 필터링 옵션입니다.  
  
5.  필요에 따라 스냅숏 에이전트를 시작하여 스냅숏을 다시 생성합니다. 변경 내용이 필요한 새 스냅숏을 생성 해야 하는 대 한 내용은 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
## 참고 항목  
 [병합 아티클 & #40; 사이의 조인 필터 집합 자동 생성 SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [매개 변수가 있는 행 필터](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  