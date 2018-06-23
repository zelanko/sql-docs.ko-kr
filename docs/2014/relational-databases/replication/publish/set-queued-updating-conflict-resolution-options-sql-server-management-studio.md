---
title: 지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 32
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d4b372dc750822d965474d93d40ff7911cf0cf7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091047"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>지연 업데이트 충돌 해결 옵션 설정(SQL Server Management Studio)
  **게시 속성 - \<Publication>** 대화 상자의 **구독 옵션** 페이지에서 지연 업데이트 구독을 지원하는 게시에 대한 충돌 해결 옵션을 설정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>지연 업데이트 충돌 해결 옵션을 설정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 **구독 옵션** 페이지에서 **충돌 해결 정책** 옵션에 대해 다음 값 중 하나를 선택합니다.  
  
    -   **게시자 변경 내용 유지**  
  
    -   **구독자 변경 내용 유지**  
  
    -   **구독 다시 초기화**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  