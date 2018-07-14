---
title: 병합 아티클에 대한 상호 충돌 해결 프로그램 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], interactive resolvers
- interactive conflict resolution [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 518cf304e143eb7737a21f3c55791d51f0865d89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227153"
---
# <a name="specify-interactive-conflict-resolution-for-merge-articles"></a>병합 아티클에 대한 상호 충돌 해결 프로그램 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클에 대한 상호 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자에서 요청 시 동기화 중에 수동으로 충돌을 해결할 수 있는 대화형 해결 프로그램을 제공합니다. 대화형 충돌 해결 기능을 설정하면 대화형 해결 프로그램을 사용하여 동기화 중 대화형으로 충돌을 해결할 수 있습니다. 대화형 해결 프로그램은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자를 통해 사용할 수 있습니다. 자세한 내용은 [Windows 동기화 관리자를 사용하여 구독 동기화&#40;Windows 동기화 관리자&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md)를 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클에 대한 상호 충돌 해결 프로그램을 지정하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   Windows 동기화 관리자 외부에서 동기화가 수행된 경우(예: SQL Server Management Studio 또는 복제 모니터의 예약된 동기화 또는 요청 시 동기화) 아티클에 지정된 기본 충돌 해결을 사용하여 사용자 개입 없이 자동으로 충돌이 해결됩니다. 자세한 내용은 [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-enable-interactive-conflict-resolution-for-an-article"></a>아티클에 대해 대화형 충돌 해결 기능을 설정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 또는 **아티클 속성 - \<ArticleType>** 페이지에서 **해결 프로그램** 탭을 클릭합니다.  
  
4.  **요청 시 동기화 중 구독자가 대화형으로 충돌 해결**을 선택합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>구독이 대화형 충돌 해결 기능을 사용하도록 지정하려면  
  
1.  **구독 속성 - \<Subscriber>: \<SubscriptionDatabase>** 대화 상자에서 **대화형으로 충돌 해결** 옵션에 **True** 값을 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 병합 게시에 대한 끌어오기 구독을 만드는 경우 구독자에서 이 그래픽 인터페이스를 사용하여 아티클 충돌을 해결하도록 프로그래밍 방식으로 지정할 수 있습니다. 이 옵션을 지원하는 아티클에서 발생한 충돌만 대화형 해결 프로그램에 표시됩니다.  
  
#### <a name="to-create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>대화형 해결 프로그램을 사용하는 병합 끌어오기 구독을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 [@publication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)을 지정하고 **@publication**에서 병합 아티클에 대한 상호 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다. 대화형 해결 프로그램을 사용할 결과 집합의 각 아티클에 대해 **allow_interactive_resolver** 값을 확인합니다.  
  
    -   이 값이 **1**이면 대화형 해결 프로그램이 사용됩니다.  
  
    -   값이 **0**이면 각 아티클에서 먼저 대화형 해결 프로그램을 설정해야 합니다. 이렇게 하려면 [@publication](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 지정하고 **@publication**을 지정하고 **@article**에 **allow_interactive_resolver** 값, **@property**에 **true** 값, **@value**에서 병합 아티클에 대한 상호 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
2.  구독 데이터베이스의 구독자에서 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)을 실행합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md)를 참조하세요.  
  
3.  구독 데이터베이스의 구독자에서 다음 매개 변수를 지정하여 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)를 실행합니다.  
  
    -   **@publisher**을 지정하고 **@publisher_db** (게시된 데이터베이스) 및 **@publication**에서 병합 아티클에 대한 상호 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
    -   **@enabled_for_syncmgr** - **true** 값  
  
    -   **@use_interactive_resolver** - **true** 값  
  
    -   병합 에이전트에 필요한 보안 계정 정보. 자세한 내용은 [Create a Pull Subscription](../create-a-pull-subscription.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)을 실행합니다.  
  
#### <a name="to-define-an-article-that-supports-the-interactive-resolver"></a>대화형 해결 프로그램을 지원하는 아티클을 정의하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행합니다. **@publication**에 아티클이 속한 게시 이름, **@article**에 아티클 이름, **@source_object**에 게시할 데이터베이스 개체 및 **@allow_interactive_resolver**에 **true** 값을 지정합니다. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [병합 게시에 대한 데이터 충돌 보기 및 해결&#40;SQL Server Management Studio&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Interactive Conflict Resolution](../merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
