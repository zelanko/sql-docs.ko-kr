---
title: "병합 구독 유형 및 충돌 해결 우선 순위 지정(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "병합 복제 충돌 해결 [SQL Server 복제], 병합 구독 해결 프로그램"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 병합 구독 유형 및 충돌 해결 우선 순위 지정(SQL Server Management Studio)
  새 구독 마법사의 **구독 유형** 페이지에서 병합 구독 유형 및 충돌 해결 우선 순위를 지정합니다. 이 마법사의 사용 방법은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 및 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)를 참조하십시오.  
  
 구독 유형을 변경할 수는 구독을 만든 후에 서버 구독 유형에 대 한 우선 순위를 수정할 수 있습니다는 **구독 속성-\< 게시자>: \< PublicationDatabase>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
### 병합 구독 유형 및 충돌 해결 우선 순위를 지정하려면  
  
1.  새 구독 마법사의 **구독 유형** 페이지에서 **구독 유형** 옵션에 대해 **클라이언트** 나 **서버** 를 선택합니다.  
  
2.  구독 유형을 선택 하는 경우 **서버**, 값 (0.00 99.99)에 대 한 입력은 **충돌 해결의 우선 순위** 옵션입니다.  
  
### 충돌 해결 우선 순위를 수정하려면  
  
1.  에 **구독 속성-\< 게시자>: \< PublicationDatabase>** 게시자의 값을 입력 (0.00 99.99)는 **우선 순위** 옵션입니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  