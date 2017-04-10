---
title: "병합 아티클에 대한 상호 충돌 해결 프로그램 지정 | Microsoft Docs"
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
  - "병합 복제 충돌 해결 [SQL Server 복제], 대화형 해결 프로그램"
  - "대화형 충돌 해결 [SQL Server 복제]"
  - "아티클 [SQL Server 복제], 충돌 해결"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
ms.assetid: e298dea0-b5ef-4907-a745-cfad9793653f
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 병합 아티클에 대한 상호 충돌 해결 프로그램 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클에 대한 상호 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 요청 시 동기화 중 충돌을 수동으로 해결할 수 있는 대화형 해결 프로그램을 제공 하는 복제 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자입니다. 대화형 충돌 해결 기능을 설정하면 대화형 해결 프로그램을 사용하여 동기화 중 대화형으로 충돌을 해결할 수 있습니다. 대화형 해결 프로그램은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자를 통해 사용할 수 있습니다. 자세한 내용은 참조 [구독 사용 하 여 Windows 동기화 관리자 & #40; 동기화 Windows 동기화 관리자 & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클에 대한 상호 충돌 해결 프로그램을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   Windows 동기화 관리자 외부에서 동기화가 수행된 경우(예: SQL Server Management Studio 또는 복제 모니터의 예약된 동기화 또는 요청 시 동기화) 아티클에 지정된 기본 충돌 해결을 사용하여 사용자 개입 없이 자동으로 충돌이 해결됩니다. 자세한 내용은 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 아티클에 대해 대화형 충돌 해결 기능을 설정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택 합니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **아티클 속성-\< 문서>** 또는 **아티클 속성-\< ArticleType>** 페이지는 **확인자** 탭 합니다.  
  
4.  선택 **요청 시 동기화 중 대화형으로 충돌 해결에 대 한 구독자 허용**합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
#### 구독이 대화형 충돌 해결 기능을 사용하도록 지정하려면  
  
1.  에 **구독 속성-\< 구독자>: \< SubscriptionDatabase>** 대화 상자에서 값을 지정 **True** 에 대 한는 **대화형으로 충돌 해결** 옵션입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 병합 게시에 대한 끌어오기 구독을 만드는 경우 구독자에서 이 그래픽 인터페이스를 사용하여 아티클 충돌을 해결하도록 프로그래밍 방식으로 지정할 수 있습니다. 이 옵션을 지원하는 아티클에서 발생한 충돌만 대화형 해결 프로그램에 표시됩니다.  
  
#### 대화형 해결 프로그램을 사용하는 병합 끌어오기 구독을 만들려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), 로 지정 하 여 **@publication**합니다. 값을 확인 **allow_interactive_resolver** 결과 대화형 해결 프로그램 사용 수에 대 한 집합의 각 아티클에 대해 합니다.  
  
    -   이 값이 **1**이면 대화형 해결 프로그램이 사용됩니다.  
  
    -   값이 **0**이면 각 아티클에서 먼저 대화형 해결 프로그램을 설정해야 합니다. 이 위해 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 로 지정 하 여 **@publication**, **@article**, 값이 **allow_interactive_resolver** 에 대 한 **@property**, 및의 값 **true** 에 대 한 **@value**합니다.  
  
2.  구독 데이터베이스의 구독자에서 실행 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)합니다. 자세한 내용은 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
3.  구독 데이터베이스의 구독자에서 실행 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md), 다음 매개 변수를 지정 합니다.  
  
    -   **@publisher**, **@publisher_db** (게시 된 데이터베이스) 및 **@publication**합니다.  
  
    -   값이 **true** 에 대 한 **@enabled_for_syncmgr**합니다.  
  
    -   값이 **true** 에 대 한 **@use_interactive_resolver**합니다.  
  
    -   병합 에이전트에 필요한 보안 계정 정보. 자세한 내용은 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)을 참조하세요.  
  
4.  게시 데이터베이스의 게시자에서 실행 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)합니다.  
  
#### 대화형 해결 프로그램을 지원하는 아티클을 정의하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 이 문서에 속한 게시의 이름을 지정 **@publication**, 에 대 한 문서에 대 한 이름을 **@article**, 게시할 데이터베이스 개체 **@source_object**, 및의 값 **true** 에 대 한 **@allow_interactive_resolver**합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
## 참고 항목  
 [보기 및 병합 게시 및 #40;에 대 한 데이터 충돌 해결 SQL Server Management Studio & #41;](../../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [대화형 충돌 해결](../../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  