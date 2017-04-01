---
title: "병합 아티클의 충돌 추적 및 해결 수준 지정 | Microsoft Docs"
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
  - "병합 복제 충돌 해결 [SQL Server 복제], 수준"
  - "아티클 [SQL Server 복제], 충돌 해결"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 병합 아티클의 충돌 추적 및 해결 수준 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클에 대한 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
 병합 게시에 대한 구독이 동기화되면 복제 시 게시자와 구독자에 있는 동일 데이터가 변경되서 발생하는 충돌이 있는지 확인합니다. 충돌을 행 수준에서 검색할지(행이 변경되면 충돌로 간주) 아니면 열 수준에서 검색할지(동일 행 및 열이 변경되는 경우에만 충돌로 간주)를 지정할 수 있습니다. 아티클에 대한 충돌 해결은 행 수준에서 수행됩니다. 논리적 레코드를 사용하는 경우의 충돌 감지 및 해결에 대한 자세한 내용은 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 병합 아티클의 충돌 추적 및 해결 수준을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   구독이 초기화된 후에 추적 수준을 수정하면 해당 구독을 다시 초기화해야 합니다. 속성 변경의 영향에 대 한 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
-   행 및 열 수준 추적을 사용하면 충돌 해결이 항상 행 수준에서 수행되고 적용되는 행이 무시되는 행을 덮어씁니다. 병합 복제를 사용하면 충돌을 추적하고 논리적 레코드 수준에서 충돌이 해결되도록 지정할 수도 있지만 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서는 이러한 옵션을 사용할 수 없습니다. 복제 저장 프로시저에서 이러한 옵션을 설정하는 방법은 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 행 수준 또는 열 수준에서 병합 아티클에 대 한 추적 지정는 **속성** 탭은 **아티클 속성** 새 게시 마법사에서 사용할 수 있는 대화 상자 및 **게시 속성-\< 게시>** 대화 상자. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 행 또는 열 수준 추적을 지정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택 합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **속성** 탭은 **아티클 속성 \< 문서>** 대화 상자에서 다음 중 하나에 대 한 값은 **추적 수준** 속성: **행 수준 추적** 또는 **열 수준 추적**합니다.  
  
4.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 새 병합 아티클에 대한 충돌 추적 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 에 대해 다음 값 중 하나를 지정 하 고 **@column_tracking**:  
  
    -   **true 이면** -아티클에 대 한 열 수준 추적을 사용 합니다.  
  
    -   **false** -기본값 사용 하 여 행 수준 추적 합니다.  
  
#### 병합 아티클에 대한 충돌 추적 옵션을 변경하려면  
  
1.  병합 아티클에 대 한 옵션을 추적 하 여 충돌을 확인 하려면 실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)합니다. 값을 확인는 **column_tracking** 결과 문서에 대 한 집합의 옵션입니다. 값이 **1** 열 수준 추적이 사용 되는 의미가 고 값 **0** 행 수준 추적 사용 되 고 있음을 의미 합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **column_tracking** 에 대 한 **@property** 는 다음 값 중 하나에 대 한 고 **@value**:  
  
    -   **true 이면** -아티클에 대 한 열 수준 추적을 사용 합니다.  
  
    -   **false** -기본값 사용 하 여 행 수준 추적 합니다.  
  
     값을 지정 **1** 모두에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**합니다.  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [논리적 레코드에서 충돌 감지 및 해결](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)   
 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  