---
title: "지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio) | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee3af1a65573f04bce7f414638b052fdd38c4777
ms.lasthandoff: 04/11/2017

---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio)
  **게시 속성 - \<Publication>** 대화 상자의 **구독 옵션** 페이지에서 지연 업데이트 구독을 지원하는 게시에 대한 충돌 해결 옵션을 설정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>지연 업데이트 충돌 해결 옵션을 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **충돌 해결 정책** 옵션에 대해 다음 값 중 하나를 선택합니다.  
  
    -   **게시자 변경 내용 유지**  
  
    -   **구독자 변경 내용 유지**  
  
    -   **구독 다시 초기화**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
