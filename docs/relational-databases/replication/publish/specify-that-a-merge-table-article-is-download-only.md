---
title: 새 병합 테이블 아티클을 다운로드 전용으로 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
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
manager: craigg
ms.openlocfilehash: f8db9ebe7ac98ce8111cc70912a6607cf4a2ef2b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718861"
---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>새 병합 테이블 아티클을 다운로드 전용으로 지정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 테이블 아티클을 다운로드 전용으로 지정하는 방법에 대해 설명합니다. 다운로드 전용 아티클은 데이터가 구독자에서 업데이트되지 않는 응용 프로그램용으로 디자인되었습니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   **새 병합 테이블 아티클을 다운로드 전용으로 지정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   구독이 초기화된 후 아티클을 다운로드 전용으로 지정하면 해당 아티클을 받은 모든 클라이언트 구독을 다시 초기화해야 합니다. 서버 구독은 다시 초기화할 필요가 없습니다. 속성 변경의 효과에 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **아티클** 페이지 또는 **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에서 아티클을 다운로드 전용으로 지정합니다. 이 대화 상자는 새 게시 마법사 및 **게시 속성 - \<게시>** 대화 상자에서 사용할 수 있습니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>아티클 페이지에서 아티클을 다운로드 전용으로 지정하려면  
  
-   새 게시 마법사의 **아티클** 페이지에서 테이블을 선택한 다음 **강조 표시된 테이블은 다운로드 전용**확인란을 선택합니다.  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>아티클 속성 - \<Article> 대화 상자의 속성 탭에서 아티클을 다운로드 전용으로 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택하고 **아티클 속성**을 클릭합니다.  
  
2.  **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **속성** 탭에 있는 **대상 개체** 섹션에서 **동기화 방향**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **구독자로 다운로드 전용, 구독자 변경 금지**  
  
    -   **구독자로 다운로드 전용, 구독자 변경 허용**  
  
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>새 병합 테이블 아티클을 다운로드 전용으로 지정하려면  
  
1.  매개 변수 **@subscriber_upload_options**에 **1** 또는 **2**의 값을 지정하여 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. 다음은 숫자 값과 이에 해당하는 동작입니다.  
  
    -   **0** - 제한이 없습니다(기본값). 구독자의 변경 내용이 게시자에 업로드됩니다.  
  
    -   **1** - 구독자에서 변경이 허용되지만 변경 내용이 게시자로 업로드되지 않습니다.  
  
    -   **2** - 구독자에서 변경이 허용되지 않습니다.  
  
        > [!NOTE]  
        >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 두 아티클의 **@subscriber_upload_options** 값이 동일해야 합니다.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>기존의 병합 테이블 아티클을 다운로드 전용으로 수정하려면  
  
1.  아티클이 다운로드 전용인지 확인하려면 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행합니다. 결과 집합에서 아티클의 **upload_options** 값을 확인합니다.  
  
2.  1단계에서 반환된 값이 **0**이면 [@property](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)매개 변수에 값을 **subscriber_upload_options** 값, **@property**및 **1** 값, **@force_invalidate_snapshot** 및 **@force_reinit_subscription**에 다음 동작에 해당하는 **1** 을 사용하여 **2** 값, **@value**을 실행합니다.  
  
    -   **1** - 구독자에서 변경이 허용되지만 변경 내용이 게시자로 업로드되지 않습니다.  
  
    -   **2** - 구독자에서 변경이 허용되지 않습니다.  
  
        > [!NOTE]  
        >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 두 아티클의 다운로드 전용 동작이 동일해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
