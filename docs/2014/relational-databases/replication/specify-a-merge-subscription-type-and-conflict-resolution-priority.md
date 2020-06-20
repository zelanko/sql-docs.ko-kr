---
title: 병합 구독 유형 및 충돌 해결 우선 순위 지정 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a19ae6246fe59308283fbaf2f35e2c49f96b140c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055562"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>병합 구독 유형 및 충돌 해결 우선 순위 지정(SQL Server Management Studio)
   새 구독 마법사의 **구독 유형** 페이지에서 병합 구독 유형 및 충돌 해결 우선 순위를 지정합니다. 이 마법사의 사용 방법은 [Create a Pull Subscription](create-a-pull-subscription.md) 및 [Create a Push Subscription](create-a-push-subscription.md)를 참조하십시오.  
  
 구독 유형은 구독을 만든 후 수정할 수 없지만 **구독 속성- \<Publisher> : \<PublicationDatabase> ** 대화 상자에서 서버 구독 유형에 대 한 우선 순위를 수정할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>병합 구독 유형 및 충돌 해결 우선 순위를 지정하려면  
  
1.  새 구독 마법사의 **구독 유형** 페이지에서 **구독 유형** 옵션에 대해 **클라이언트** 나 **서버** 를 선택합니다.  
  
2.  구독 유형을 **서버**로 선택한 경우 **충돌 해결의 우선 순위** 에 0.00에서 99.99 사이의 값을 입력합니다.  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>충돌 해결 우선 순위를 수정하려면  
  
1.  **구독 속성- \<Publisher> \<PublicationDatabase> ** 게시자에서 **우선 순위** 옵션에 대 한 값 (0.00 ~ 99.99)을 입력 합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
