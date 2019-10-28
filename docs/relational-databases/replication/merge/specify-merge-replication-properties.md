---
title: 병합 복제 속성 지정| Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ae39654a19c73c71c602801b3aa5f594f7d0828
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908154"
---
# <a name="specify-merge-replication-properties"></a>병합 복제 속성 지정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 병합 복제의 다양한 속성을 지정하는 방법을 설명합니다. 

## <a name="merge-article-is-download-only"></a>병합 문서는 다운로드 전용입니다.
다운로드 전용 아티클은 데이터가 구독자에서 업데이트되지 않는 애플리케이션용으로 디자인되었습니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
   
###  <a name="considerations"></a>고려 사항   
-   구독이 초기화된 후 아티클을 다운로드 전용으로 지정하면 해당 아티클을 받은 모든 클라이언트 구독을 다시 초기화해야 합니다. 서버 구독은 다시 초기화할 필요가 없습니다. 속성 변경의 효과에 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
#### <a name="on-the-articles-page"></a>문서 페이지에서
새 게시 마법사의 **아티클** 페이지에서 테이블을 선택한 다음 **강조 표시된 테이블은 다운로드 전용**확인란을 선택합니다.  
  
#### <a name="on-the-properties-tab-of-the-article-properties"></a>문서 속성의 속성 탭에서  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택하고 **아티클 속성**을 클릭합니다.    
2.  **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **대상 개체** 섹션에서 **동기화 방향**에 대해 다음 값 중 하나를 지정합니다.    
    -   **구독자로 다운로드 전용, 구독자 변경 금지**    
    -   **구독자로 다운로드 전용, 구독자 변경 허용**    
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  

###  <a name="use-transact-sql"></a>Transact-SQL 사용  
  
#### <a name="new-article"></a>새 아티클  
  
1.  `@subscriber_upload_options` 매개 변수에 **1** 또는 **2** 값을 지정하고 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. 다음은 숫자 값과 이에 해당하는 동작입니다.  
  
    -   **0** - 제한이 없습니다(기본값). 구독자의 변경 내용이 게시자에 업로드됩니다.    
    -   **1** - 구독자에서 변경이 허용되지만 변경 내용이 게시자로 업로드되지 않습니다.    
    -   **2** - 구독자에서 변경이 허용되지 않습니다.  
  
       > [!NOTE]  
       > 아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 두 아티클의 `@subscriber_upload_options` 값이 동일해야 합니다.  
  
#### <a name="existing-article"></a>기존 아티클
  
1.  아티클이 다운로드 전용인지를 확인하려면 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행하고 결과 집합의 문서에 대해 **upload_options** 값을 확인합니다. 
  
2.  1단계에서 반환된 값이 **0**이면 `@property`에 **subscriber_upload_options** 값, `@force_invalidate_snapshot` 및 `@force_reinit_subscription`에 **1** 값, `@value`에 다음 동작에 해당하는 **1** 또는 **2** 값을 지정하고 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.  
  
    -   **1** - 구독자에서 변경이 허용되지만 변경 내용이 게시자로 업로드되지 않습니다.    
    -   **2** - 구독자에서 변경이 허용되지 않습니다.  
  
        > [!NOTE]  
        >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 두 아티클의 다운로드 전용 동작이 동일해야 합니다.  
  
## <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution 
  
 Microsoft SQL Server 복제는 Microsoft Windows 동기화 관리자에서 요청 시 동기화 중에 수동으로 충돌을 해결할 수 있는 대화형 해결 프로그램을 제공합니다. 대화형 충돌 해결 기능을 설정하면 대화형 해결 프로그램을 사용하여 동기화 중 대화형으로 충돌을 해결할 수 있습니다. 대화형 해결 프로그램은 Microsoft Windows 동기화 관리자를 통해 사용할 수 있습니다. 자세한 내용은 [Windows 동기화 관리자를 사용하여 구독 동기화&#40;Windows 동기화 관리자&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)를 참조하세요.  
  
  
### <a name="Recommendations"></a> 권장 사항  
  
-   Windows 동기화 관리자 외부에서 동기화가 수행된 경우(예: SQL Server Management Studio 또는 복제 모니터의 예약된 동기화 또는 요청 시 동기화) 아티클에 지정된 기본 충돌 해결을 사용하여 사용자 개입 없이 자동으로 충돌이 해결됩니다. 자세한 내용은 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하세요.  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>문서에 대해 대화형 충돌 해결 사용  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.   
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.    
3.  **아티클 속성 - \<Article>** 또는 **아티클 속성 - \<ArticleType>** 페이지에서 **해결 프로그램** 탭을 클릭합니다.    
4.  **요청 시 동기화 중 구독자가 대화형으로 충돌 해결**을 선택합니다.    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>구독에서 대화형 충돌 해결 기능을 사용하도록 지정  
  
1.  **구독 속성 - \<Subscriber>: \<SubscriptionDatabase>** 대화 상자에서 **대화형으로 충돌 해결** 옵션에 대해 **True** 값을 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.   
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="use-transact-sql"></a>Transact-SQL 사용  
 병합 게시에 대한 끌어오기 구독을 만드는 경우 구독자에서 이 그래픽 인터페이스를 사용하여 아티클 충돌을 해결하도록 프로그래밍 방식으로 지정할 수 있습니다. 이 옵션을 지원하는 아티클에서 발생한 충돌만 대화형 해결 프로그램에 표시됩니다.  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>대화형 해결 프로그램을 사용하는 병합 끌어오기 구독 만들기  
  
1.  게시 데이터베이스의 게시자에서 `@publication`을 지정하고 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)을 실행합니다. 대화형 해결 프로그램을 사용할 결과 집합의 각 아티클에 대해 **allow_interactive_resolver** 값을 확인합니다.   
    -   이 값이 **1**이면 대화형 해결 프로그램이 사용됩니다.    
    -   값이 **0**이면 각 아티클에서 먼저 대화형 해결 프로그램을 설정해야 합니다. 이렇게 하려면 `@publication`, `@article`을 지정한 다음 `@property`에 **allow_interactive_resolver** 값, `@value`에 **true** 값을 지정하고 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.    
2.  구독 데이터베이스의 구독자에서 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)을 실행합니다. 자세한 내용은 [끌어오기 구독 만들기](../../../relational-databases/replication/create-a-pull-subscription.md)를 참조하세요.    
3.  구독 데이터베이스의 구독자에서 다음 매개 변수를 지정하여 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)를 실행합니다.    
    -   `@publisher`, `@publisher_db`(게시된 데이터베이스) 및 `@publication`    
    -   `@enabled_for_syncmgr`에 **true** 값    
    -   `@use_interactive_resolver`에 **true** 값    
    -   병합 에이전트에 필요한 보안 계정 정보. 자세한 내용은 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.    
4.  게시 데이터베이스의 게시자에서 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)을 실행합니다.  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>대화형 해결 프로그램을 지원하는 문서 정의  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. `@publication`에 아티클이 속한 게시의 이름, `@article`에 아티클의 이름, `@source_object`에 게시되는 데이터베이스 개체, `@allow_interactive_resolver`에 **true** 값을 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
 
## <a name="conflict-tracking-and-resolution-level-for-merge-articles"></a>병합 문서의 충돌 추적 및 해결 수준
이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클에 대한 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
 병합 게시에 대한 구독이 동기화되면 복제 시 게시자와 구독자에 있는 동일 데이터가 변경되서 발생하는 충돌이 있는지 확인합니다. 충돌을 행 수준에서 검색할지(행이 변경되면 충돌로 간주) 아니면 열 수준에서 검색할지(동일 행 및 열이 변경되는 경우에만 충돌로 간주)를 지정할 수 있습니다. 아티클에 대한 충돌 해결은 행 수준에서 수행됩니다. 논리적 레코드를 사용하는 경우의 충돌 감지 및 해결에 대한 자세한 내용은 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)을 참조하세요.  
 
### <a name="limitations-and-restrictions"></a>제한 사항  
  
-   구독이 초기화된 후에 추적 수준을 수정하면 해당 구독을 다시 초기화해야 합니다. 속성 변경의 영향에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.   
-   행 및 열 수준 추적을 사용하면 충돌 해결이 항상 행 수준에서 수행되고 적용되는 행이 무시되는 행을 덮어씁니다. 병합 복제를 사용하면 충돌을 추적하고 논리적 레코드 수준에서 충돌이 해결되도록 지정할 수도 있지만 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서는 이러한 옵션을 사용할 수 없습니다. 복제 저장 프로시저에서 이러한 옵션을 설정하는 방법은 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)를 참조하세요.  
  
### <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용  
 새 게시 마법사 및 **게시 속성 - \<게시>** 대화 상자에서 사용할 수 있는 **아티클 속성** 대화 상자의 **속성** 탭에서 병합 아티클에 대한 행 또는 열 수준 추적을 지정합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="specify-row--or-column-level-tracking"></a>행 또는 열 수준 추적 지정  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택합니다.  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.   
3.  **문서 속성 \<Article>** 대화 상자의 **속성** 탭에서 **추적 수준** 속성에 대해 다음 값 중 하나를 선택합니다. **행 수준 추적** 또는 **열 수준 추적**.   
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
### <a name="use-transact-sql"></a>Transact-SQL 사용  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>새 병합 아티클에 대한 충돌 추적 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 `@column_tracking`에 다음 값 중 하나를 지정하고 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다.  
  
    -   **true** - 아티클에 대해 열 수준 추적을 사용합니다.    
    -   **false** - 행 수준 추적을 사용합니다(기본값).  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>병합 문서에 대한 충돌 추적 옵션 변경  
  
1.  병합 아티클에 대한 충돌 추적 옵션을 확인하려면 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행합니다. 결과 집합에서 아티클에 대한 **column_tracking** 옵션의 값을 확인합니다. 값이 **1** 이면 열 수준 추적을 사용 중이고 **0** 이면 행 수준 추적을 사용 중입니다.    
2.  게시 데이터베이스의 게시자에서 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. `@property`에 **column_tracking** 값, `@value`에 다음 값 중 하나를 지정합니다.  
  
    -   **true** - 아티클에 대해 열 수준 추적을 사용합니다.    
    -   **false** - 행 수준 추적을 사용합니다(기본값).  
  
     `@force_invalidate_snapshot` 및 `@force_reinit_subscription`에 모두 **1** 값을 지정합니다. 

## <a name="manage-tracking--deletes"></a>추적 삭제 관리
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 기본적으로 병합 복제는 게시자와 구독자 간에 DELETE 명령을 동기화합니다. 병합 복제에서는 행을 게시에서 삭제한 경우에도 구독 데이터베이스에는 그대로 유지할 수 있으며 반대의 경우도 마찬가지입니다. 새 아티클을 만들 때 DELETE 명령을 무시할지 여부를 프로그래밍 방식으로 지정할 수 있으며 복제 저장 프로시저를 사용하여 이 기능을 나중에 활성화할 수도 있습니다.  
  
> [!IMPORTANT]  
>  이 기능을 활성화하면 불일치가 발생합니다. 이는 구독자에 있는 데이터가 게시자에 있는 데이터를 정확하게 반영하지 않음을 의미합니다. 이 경우 삭제된 행을 수동으로 제거하기 위한 메커니즘을 직접 구현해야 합니다.  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>새 병합 문서에 대해 삭제가 무시되도록 지정  
  
게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. `@delete_tracking`에 **false** 값을 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.
  
    > [!NOTE]  
    >  If the source table for an article is already published in another publication, the value of **delete_tracking** must be the same for both articles.  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>기존 병합 문서에 대해 삭제가 무시되도록 지정  
  
1.  아티클에 대해 오류 보정이 설정되어 있는지 확인하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행하고 결과 집합에서 **delete_tracking**의 값을 확인합니다. 이 값이 **0**이면 삭제가 이미 무시되고 있는 것입니다.  
  
2.  1단계의 값이 **1**이면 게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. `@property`에 `delete_tracking` 값, `@value`에 **false** 값을 지정합니다.  
  
    > [!NOTE]  
    >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 **delete_tracking** 값은 두 아티클에 대해 동일해야 합니다.  
  

## <a name="processing-order"></a>처리 순서
  병합 복제를 사용하면 동기화 프로세스 중에 병합 에이전트에서 아티클을 처리하는 순서를 지정할 수 있습니다. 아티클을 작성할 때 복제 저장 프로시저를 사용하여 각 아티클 순서를 프로그래밍 방식으로 할당할 수 있습니다. 아티클은 최하위에서 최상위의 순서로 처리됩니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 

### <a name="how-processing-order-is-determined"></a>처리 순서 결정 방식  
 병합 동기화 중 아티클은 기본적으로 기본 테이블에 정의된 DRI(선언적 참조 무결성) 제약 조건을 포함하여 개체 간 종속 관계에 필요한 순서대로 처리됩니다. 아티클 처리 시 테이블에 변경 내용을 열거한 다음 이들 변경 내용을 적용합니다. DRI가 없지만 조인 필터 또는 논리적 레코드가 테이블 아티클 사이에 존재할 경우 아티클은 필터 및 논리적 레코드에 필요한 순서대로 처리됩니다. DRI, 조인 필터, 논리적 레코드 또는 기타 종속 관계를 통해 다른 아티클과 관련되어 있지 않은 아티클은 [sysmergearticles&#40;Transact-SQL&#41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 시스템 테이블에서의 아티클 애칭에 따라 처리됩니다.  
  
 **SalesOrderHeader** 테이블에는 기본 키 열 **SalesOrderID** 가 있고 **SalesOrderDetail** 테이블에는 해당 외래 키 열 **SalesOrderID** 가 있는 **SalesOrderHeader** 및 **SalesOrderDetail** 테이블을 포함하는 게시가 있다고 가정합니다. 이 게시를 동기화할 때 병합 복제에서 **SalesOrderHeader** 에 새 행을 삽입한 다음 **SalesOrderDetail**에 연결된 행을 삽입하여 외래 키 위반을 방지합니다. 마찬가지로 **SalesOrderDetail** 에서 행을 삭제한 다음 **SalesOrderHeader**에서 연결된 행을 삭제합니다.  
  
 그러나 일부 애플리케이션에서는 DRI가 아닌 애플리케이션 수준에서나 데이터베이스 트리거를 통해 참조 무결성이 적용됩니다. DRI 대신 위에서 설명한 게시를 제공한 경우 **SalesOrderDetail** 테이블에는 삽입을 허용하기 전에 **SalesOrderHeader** 테이블에 연결된 행이 존재하도록 하는 삽입 트리거가 있을 수 있습니다. **SalesOrderHeader** 에는 삭제를 허용하기 전에 **SalesOrderDetail** 에 연결된 행이 없도록 하는 삭제 트리거가 있을 수 있습니다. 병합 복제는 트리거가 발생될 때까지 트리거의 결과를 확인할 수 없으므로 아티클의 처리 순서를 결정할 때 트리거를 고려하지 않습니다. 마찬가지로 복제는 애플리케이션 수준에서 정의된 제약 조건을 고려할 수 없습니다.  
  
 참조 무결성이 트리거를 통해서 또는 애플리케이션 수준에서 유지 관리되는 경우 아티클이 처리되는 순서를 지정해야 합니다. 트리거가 있는 예제에서 아티클 순서는 삽입 순서에 따라 지정되므로 **SalesOrderDetail** 전에 **SalesOrderHeader**테이블이 처리되도록 지정합니다. 병합 복제는 삭제 순서를 자동으로 반대로 바꿉니다. 병합 에이전트는 제약 조건 위반이 발생해도 아티클을 계속 처리하고 다른 아티클이 처리된 후 실패한 작업을 모두 다시 시도하므로 병합 복제는 아티클 순서를 지정하지 않아도 실패하지 않습니다. 아티클 순서를 지정하면 다시 시도 및 다시 시도와 연결된 추가 처리 작업이 실행되지 않도록 할 수 있습니다. 헤더 레코드 전에 정보 레코드가 처리되도록 하는 등 순서를 잘못 지정하면 병합 복제는 성공할 때까지 처리를 다시 시도합니다.   
  
### <a name="new-article"></a>새 아티클
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. 이때 `@processing_order`에 아티클의 처리 순서를 나타내는 정수 값을 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  정렬된 아티클을 만들려면 아티클 순서 값 사이에 간격을 두어야 합니다. 그러면 나중에 새 값을 쉽게 설정할 수 있습니다. 예를 들어 3개 아티클의 고정 처리 순서를 지정해야 하는 경우 `@processing_order` 값을 각각 1, 2, 3이 아닌 10, 20, 30으로 설정합니다.  
  
### <a name="existing-article"></a>기존 아티클
  
1.  아티클의 처리 순서를 결정하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행하고 결과 집합에서 **processing_order** 값을 확인합니다.   
2.  게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. 이때 `@property`에 **processing_order** 값, `@value`에 처리 순서를 나타내는 정수 값을 지정합니다.  


## <a name="see-also"></a>참고 항목  
 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
