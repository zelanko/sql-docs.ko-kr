---
title: 매개 변수가 있는 행 필터 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- filters [SQL Server replication], parameterized
- merge replication precomputed partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], optimizing
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17edc0c7156513befd584f411c2598fc9fc70bcd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046237"
---
# <a name="optimize-parameterized-row-filters"></a>매개 변수가 있는 행 필터 최적화
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 매개 변수가 있는 행 필터를 최적화하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
-   **매개 변수가 있는 행 필터를 최적화하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   매개 변수가 있는 필터를 사용하는 경우 게시를 만들 때 **use partition groups** 옵션 또는 **keep partition changes** 옵션을 지정하여 병합 복제에서 필터가 처리되는 방법을 제어할 수 있습니다. 이러한 옵션은 게시 데이터베이스에 추가 메타데이터를 저장함으로써 필터링된 아티클이 있는 게시의 동기화 성능을 개선합니다. 아티클을 만들 때 **partition options** 를 설정하면 구독자 간에 데이터가 공유되는 방법을 제어할 수 있습니다. 이러한 요구 사항에 대한 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)를 참조하세요.  
  
     삭제가 올바르게 전파되도록 보장하려면 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact 구독자에서 keep_partition_changes를 true로 설정해야 합니다. false로 설정한 경우 구독자에 예상한 것보다 많은 행이 포함될 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 다음 설정을 사용하여 매개 변수가 있는 행 필터를 최적화할 수 있습니다.  
  
 **Partition Options**  
 **아티클 속성 - \<Article>** 대화 상자 또는 **필터 추가** 대화 상자의 **속성** 페이지에서 이 옵션을 설정합니다. 두 대화 상자는 새 게시 마법사 및 **게시 속성 - \<게시>** 대화 상자에서 사용할 수 있습니다. **아티클 속성 - \<Article>** 대화 상자에서는 **필터 추가** 대화 상자에서 사용할 수 없는 이 옵션에 대한 추가 값을 지정할 수 있습니다.  
  
 **파티션 미리 계산**  
 게시의 아티클이 일련의 요구 사항을 충족하는 경우 이 옵션은 기본적으로 **True** 로 설정됩니다. 이러한 요구 사항에 대한 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요. **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 이 옵션을 수정합니다.  
  
 **동기화 최적화**  
 **파티션 미리 계산** 이 **False** 로 설정된 경우에만 이 옵션을 **True**로 설정해야 합니다. **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 이 옵션을 설정합니다.  
  
 새 게시 마법사 사용 및 **게시 속성 - \<게시>** 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-set-partition-options-in-the-add-filter-or-edit-filter-dialog-box"></a>필터 추가 또는 필터 편집 대화 상자에서 파티션 옵션을 설정하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에서 **추가**를 클릭하고 **필터 추가**를 클릭합니다.  
  
2.  매개 변수가 있는 필터를 만듭니다. 자세한 내용은 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)을 참조하세요.  
  
3.  구독자 간에 데이터를 공유하는 방식과 일치하는 옵션을 선택합니다.  
  
    -   **이 테이블의 행을 여러 구독으로 이동**  
  
    -   **이 테이블의 행을 단일 구독으로 이동**  
  
     **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서는 보다 작은 메타데이터를 저장하고 처리하여 성능을 최적화할 수 있습니다. 그러나 한 행이 둘 이상의 구독자로 복제될 수 없도록 데이터가 분할되어야 합니다. 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-set-partition-options-in-the-article-properties---article-dialog-box"></a>아티클 속성 - \<Article> 대화 상자에서 파티션 옵션을 설정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **대상 개체** 섹션에서 **파티션 옵션**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **겹침**  
  
    -   **겹침, 파티션 외부 데이터 변경 내용 허용 안 함**  
  
    -   **겹치지 않음, 단일 구독**  
  
    -   **겹치지 않음, 구독 간 공유**  
  
     이러한 옵션 및 이 옵션이 **필터 추가** 및 **필터 편집** 대화 상자에서 사용 가능한 옵션과 어떻게 관련되어 있는지에 대한 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)의 "'partition options' 설정" 섹션을 참조하십시오.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-set-precompute-partitions"></a>파티션 미리 계산을 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **파티션 사전 계산** 옵션의 값을 선택합니다. 다음과 같은 경우 이 속성은 읽기 전용입니다.  
  
    -   게시가 사전 계산 파티션의 요구 사항을 충족시키지 못합니다.  
  
    -   게시에 대한 스냅샷이 아직 생성되지 않았습니다. 이 경우 해당 옵션은 **스냅샷 생성 시기 자동 설정**의 값을 표시합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-optimize-synchronization"></a>동기화 최적화를 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **동기화 최적화**에 대해 **True** 값을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **@keep_partition_changes** 및 **@use_partition_groups** 에 대한 필터링 옵션의 정의는 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)을 참조하세요.  
  
#### <a name="to-specify-merge-filter-optimizations-when-creating-a-new-publication"></a>새 게시를 만들 때 병합 필터 최적화를 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)을 실행합니다. 지정할 **@publication** 값 `true` 하나에 대해 다음 매개 변수:  
  
    -   **@use_partition_groups** : - 아티클이 사전 계산 파티션의 요구 사항을 충족하는 경우 가장 높은 성능 최적화를 제공합니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
    -   **@keep_partition_changes** - 사전 계산 파티션을 사용할 수 없는 경우에는 이 최적화를 사용하십시오.  
  
2.  게시에 대한 스냅샷 작업을 추가합니다. 자세한 내용은 [게시 만들기](create-a-publication.md)를 참조하세요.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행하고 다음 매개 변수를 지정합니다.  
  
    -   **@publication** - 1단계에서 만든 게시의 이름입니다.  
  
    -   **@article** - 아티클의 이름.  
  
    -   **@source_object** - 게시되는 데이터베이스 개체.  
  
    -   **@subset_filterclause** - 아티클을 행 필터링하는 데 사용되는 선택적인 매개 변수가 있는 필터 절.  
  
    -   **@partition_options** - 필터링된 아티클에 대한 파티션 옵션.  
  
4.  게시의 각 아티클에 대해 3단계를 반복합니다.  
  
5.  필요에 따라 게시 데이터베이스의 게시자에서 [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql) 를 실행하여 두 아티클 간의 조인 필터를 정의합니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
#### <a name="to-view-and-modify-merge-filter-behaviors-for-an-existing-publication"></a>기존 게시에 대한 병합 필터 동작을 확인 및 수정하려면  
  
1.  필요에 따라 게시 데이터베이스의 게시자에서 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)을 실행하고 **@publication** 에서 매개 변수가 있는 행 필터를 최적화하는 방법에 대해 설명합니다. 결과 집합에서 **keep_partition_changes** 및 **use_partition_groups** 값을 확인합니다.  
  
2.  필요에 따라 게시 데이터베이스의 게시자에서 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)을 실행합니다. 값을 지정 **use_partition_groups** 에 대 한 **@property** 고 `true` 하거나 `false` 에 대 한 **@value** 합니다.  
  
3.  필요에 따라 게시 데이터베이스의 게시자에서 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)을 실행합니다. 값을 지정 **keep_partition_changes** 에 대 한 **@property** 고 `true` 하거나 `false` 에 대 한 **@value** 합니다.  
  
    > [!NOTE]  
    >  **keep_partition_changes**를 설정할 때는 먼저 **use_partition_groups**를 해제하고 **@force_reinit_subscription** 에 **1** 값을 지정해야 합니다.  
  
4.  필요에 따라 게시 데이터베이스의 게시자에서 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 실행합니다. **@property** 에 **partition_options** 값을 지정하고 **@value** 에는 적절한 값을 지정합니다. 이러한 필터링 옵션의 정의는 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 을 참조하십시오.  
  
5.  필요에 따라 스냅샷 에이전트를 시작하여 스냅샷을 다시 생성합니다. 새 스냅샷을 생성해야 하는 변경에 대한 자세한 내용은 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [병합 아티클 간의 조인 필터 집합 자동 생성&#40;SQL Server Management Studio&#41;](automatically-generate-join-filters-between-merge-articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)  
  
  
