---
title: 병합 아티클의 충돌 추적 및 해결 수준 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 951dd630889bb34e69b888ffec4beb18025b6f8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841701"
---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>병합 아티클의 충돌 추적 및 해결 수준 지정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클에 대한 충돌 추적 및 해결 수준을 지정하는 방법에 대해 설명합니다.  
  
 병합 게시에 대한 구독이 동기화되면 복제 시 게시자와 구독자에 있는 동일 데이터가 변경되서 발생하는 충돌이 있는지 확인합니다. 충돌을 행 수준에서 검색할지(행이 변경되면 충돌로 간주) 아니면 열 수준에서 검색할지(동일 행 및 열이 변경되는 경우에만 충돌로 간주)를 지정할 수 있습니다. 아티클에 대한 충돌 해결은 행 수준에서 수행됩니다. 논리적 레코드를 사용하는 경우의 충돌 감지 및 해결에 대한 자세한 내용은 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
-   **다음을 사용하여 병합 아티클의 충돌 추적 및 해결 수준을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   구독이 초기화된 후에 추적 수준을 수정하면 해당 구독을 다시 초기화해야 합니다. 속성 변경의 영향에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
-   행 및 열 수준 추적을 사용하면 충돌 해결이 항상 행 수준에서 수행되고 적용되는 행이 무시되는 행을 덮어씁니다. 병합 복제를 사용하면 충돌을 추적하고 논리적 레코드 수준에서 충돌이 해결되도록 지정할 수도 있지만 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서는 이러한 옵션을 사용할 수 없습니다. 복제 저장 프로시저에서 이러한 옵션을 설정하는 방법은 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)를 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사 및 **게시 속성 - \<게시>** 대화 상자에서 사용할 수 있는 **아티클 속성** 대화 상자의 **속성** 탭에서 병합 아티클에 대한 행 또는 열 수준 추적을 지정합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>행 또는 열 수준 추적을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<게시>** 대화 상자에서 테이블을 선택합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정** 또는 **모든 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성 \<Article>** 대화 상자의 **속성** 탭에서 **추적 수준** 속성에 대해 **행 수준 추적** 또는 **열 수준 추적** 중 하나를 선택합니다.  
  
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>새 병합 아티클에 대한 충돌 추적 옵션을 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 을 실행하고 **@column_tracking**에 대해 다음 값 중 하나를 지정합니다.  
  
    -   **true** - 아티클에 대해 열 수준 추적을 사용합니다.  
  
    -   **false** - 행 수준 추적을 사용합니다(기본값).  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>병합 아티클에 대한 충돌 추적 옵션을 변경하려면  
  
1.  병합 아티클에 대한 충돌 추적 옵션을 확인하려면 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행합니다. 결과 집합에서 아티클에 대한 **column_tracking** 옵션의 값을 확인합니다. 값이 **1** 이면 열 수준 추적을 사용 중이고 **0** 이면 행 수준 추적을 사용 중입니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. **@property**에 **column_tracking** 값을 지정하고 **@value**에 다음 값 중 하나를 지정합니다.  
  
    -   **true** - 아티클에 대해 열 수준 추적을 사용합니다.  
  
    -   **false** - 행 수준 추적을 사용합니다(기본값).  
  
     **@force_invalidate_snapshot** 및 **@force_reinit_subscription** 모두에 **1**의 값을 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
