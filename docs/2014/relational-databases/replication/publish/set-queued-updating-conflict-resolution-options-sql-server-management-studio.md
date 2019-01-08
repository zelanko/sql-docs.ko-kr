---
title: 지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f05328a43c75158e9be6c13e4fc23b0cc9ab2799
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749006"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio)
  **게시 속성 - \<Publication>** 대화 상자의 **구독 옵션** 페이지에서 지연 업데이트 구독을 지원하는 게시에 대한 충돌 해결 옵션을 설정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>지연 업데이트 충돌 해결 옵션을 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **충돌 해결 정책** 옵션에 대해 다음 값 중 하나를 선택합니다.  
  
    -   **게시자 변경 내용 유지**  
  
    -   **구독자 변경 내용 유지**  
  
    -   **구독 다시 초기화**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
