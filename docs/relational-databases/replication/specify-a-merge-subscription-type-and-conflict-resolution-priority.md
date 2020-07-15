---
title: 유형 및 충돌 해결 우선 순위 지정(병합)
description: SQL Server 병합 구독에서 사용되는 유형 및 충돌 해결 정책을 지정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2981f84bd2cbf6c813a4adf761ddd271c8b68fd1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737050"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>병합 구독 유형 및 충돌 해결 우선 순위 지정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  새 구독 마법사의 **구독 유형** 페이지에서 병합 구독 유형 및 충돌 해결 우선 순위를 지정합니다. 이 마법사의 사용 방법은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 및 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)를 참조하십시오.  
  
 구독을 만든 후에는 구독 유형을 수정할 수 없지만 서버 구독 유형의 우선 순위는 **구독 속성 - \<Publisher>: \<PublicationDatabase>** 대화 상자에서 수정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>병합 구독 유형 및 충돌 해결 우선 순위를 지정하려면  
  
1.  새 구독 마법사의 **구독 유형** 페이지에서 **구독 유형** 옵션에 대해 **클라이언트** 나 **서버** 를 선택합니다.  
  
2.  구독 유형을 **서버**로 선택한 경우 **충돌 해결의 우선 순위** 에 0.00에서 99.99 사이의 값을 입력합니다.  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>충돌 해결 우선 순위를 수정하려면  
  
1.  게시자의 **구독 속성 - \<Publisher>: \<PublicationDatabase>** 에서 **우선 순위** 옵션에 값(0.00~99.99)을 입력합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
