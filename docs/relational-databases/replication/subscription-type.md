---
title: "구독 유형 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscriptiontype.f1"
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 구독 유형
  병합 복제에는 두 가지 구독 유형을 제공 합니다: 서버 및 클라이언트 (이전 버전의에서 참조 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전역 및 로컬, 각각). 서버 구독이 있는 구독자는 다음을 수행할 수 있습니다.  
  
-   데이터를 다른 구독자에 다시 게시합니다.  
  
-   대체 동기화 파트너 역할을 수행합니다.  
  
-   설정한 우선 순위에 따라 충돌을 해결합니다.  
  
 대부분의 구독자는 이 기능이 필요하지 않으며 클라이언트 구독을 사용할 수 있습니다. 클라이언트 구독을 사용하면 충돌 감지 및 해결이 가능하지만 구독자에게 우선 순위가 할당되지 않습니다. 변경 내용을 게시자에 전송할 첫 번째 구독자는 해당 변경 내용으로 인해 발생하는 모든 충돌에서 우선 적용됩니다.  
  
> [!NOTE]  
>  구독 유형은 구독을 만든 후에는 변경할 수 없습니다.  
  
## 옵션  
 **구독 속성**  
 각 구독자에 대 한 선택 **클라이언트** 또는 **서버** 드롭다운 목록 상자에서 **구독 유형** 열입니다. 서버 구독이 있는 구독자에 대 한 0에서 99.99 사이의 숫자를 입력는 **충돌 해결의 우선 순위** 열 (숫자가 클수록, 구독자에 대 한 클수록 우선 순위).  
  
## 참고 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  