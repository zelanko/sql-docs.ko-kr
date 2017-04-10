---
title: "새 병합 테이블 아티클을 다운로드 전용으로 지정 | Microsoft Docs"
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
  - "병합 복제 [SQL Server 복제], 다운로드 전용 아티클"
  - "아티클 [SQL Server 복제], 다운로드 전용"
  - "다운로드 전용 아티클"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 새 병합 테이블 아티클을 다운로드 전용으로 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 테이블 아티클을 다운로드 전용으로 지정하는 방법에 대해 설명합니다. 다운로드 전용 아티클은 데이터가 구독자에서 업데이트되지 않는 응용 프로그램용으로 디자인되었습니다. 자세한 내용은 참조 [with Download-Only Articles 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
-   **새 병합 테이블 아티클을 다운로드 전용으로 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   구독이 초기화된 후 아티클을 다운로드 전용으로 지정하면 해당 아티클을 받은 모든 클라이언트 구독을 다시 초기화해야 합니다. 서버 구독은 다시 초기화할 필요가 없습니다. 속성 변경의 효과에 자세한 내용은 참조 [변경 게시 및 아티클 속성](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 아티클을 다운로드 전용으로 지정 된 **문서** 새 게시 마법사의 페이지 또는 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자. 이 대화 상자는 새 게시 마법사에서 사용할 수 있는 고 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 아티클 페이지에서 아티클을 다운로드 전용으로 지정하려면  
  
-   에 **문서** 페이지는 새 게시 마법사 테이블을 선택한 다음 선택 확인란의 **강조 표시 된 테이블은 다운로드 전용**합니다.  
  
#### 아티클을 다운로드 전용 아티클 속성-필터 탭의 속성을 지정 하려면 \< 문서> 대화 상자  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성**합니다.  
  
2.  **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **대상 개체** 의 섹션은 **속성** 탭은 **아티클 속성-\< 문서>** 대화 상자에 다음 값 중 하나를 지정 합니다 **동기화 방향**:  
  
    -   **구독자로 다운로드 전용, 구독자 변경 금지**  
  
    -   **구독자로 다운로드 전용, 구독자 변경 허용**  
  
4.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 새 병합 테이블 아티클을 다운로드 전용으로 지정하려면  
  
1.  실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), 값을 지정 하면 **1** 또는 **2** 매개 변수에 대해 **@subscriber_upload_options**합니다. 다음은 숫자 값과 이에 해당하는 동작입니다.  
  
    -   **0** -제한이 없습니다 (기본값). 구독자의 변경 내용이 게시자에 업로드됩니다.  
  
    -   **1** -허용 되지만 변경 내용이 구독자에서 게시자로 업로드 되지 않습니다.  
  
    -   **2** -구독자에서 변경이 허용 되지 않습니다.  
  
        > [!NOTE]  
        >  아티클의 원본 테이블이 이미 다른 게시의 값에 게시 된 경우 **@subscriber_upload_options** 두 아티클에 대해 동일 해야 합니다.  
  
#### 기존의 병합 테이블 아티클을 다운로드 전용으로 수정하려면  
  
1.  아티클을 다운로드 전용 인지를 확인 하려면 실행 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)합니다. 값을 확인 **upload_options** 결과에 문서에 대 한 설정입니다.  
  
2.  1 단계는 값에 반환 하는 경우 **0**, 실행 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 값을 지정 하면 **subscriber_upload_options** 에 대 한 **@property**, 값이 **1** 에 대 한 **@force_invalidate_snapshot** 및 **@force_reinit_subscription**, 및의 값 **1** 또는 **2** 에 대 한 **@value**, 다음과 같은 동작에 해당 하는:  
  
    -   **1** -허용 되지만 변경 내용이 구독자에서 게시자로 업로드 되지 않습니다.  
  
    -   **2** -구독자에서 변경이 허용 되지 않습니다.  
  
        > [!NOTE]  
        >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 두 아티클의 다운로드 전용 동작이 동일해야 합니다.  
  
## 참고 항목  
 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)   
 [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  