---
title: "업데이트할 수 있는 구독 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.updatablesubscriptions.f1"
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 업데이트할 수 있는 구독
  트랜잭션 복제로 복제 된 데이터 처리 해야 읽기 전용으로 그러나에서 복제 된 데이터를 수정할 수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트할 수 있는 구독을 사용 하 여 구독자입니다. 구독자에서 데이터를 수정해야 하는 경우 요구 사항에 따라 다음 옵션 중 하나를 선택합니다.  
  
|업데이트할 수 있는 구독 유형|요구 사항|  
|---------------------------------|------------------|  
|즉시 업데이트|구독자에서 데이터를 업데이트하기 위해 게시자 및 구독자를 연결해야 합니다.|  
|지연 업데이트|구독자에서 데이터를 업데이트하기 위해 게시자 및 구독자를 연결할 필요가 없습니다. 오프라인 상태에서 업데이트한 다음 나중에 게시자와 구독자 간에 동기화할 수 있습니다.|  
  
## 옵션  
 **구독자 변경 내용 복제**  
 확인란을 선택 된 **복제** 으로 업데이트할 수 있어야 하는 각 구독자에 대 한 열입니다. 드롭다운 목록 상자에서 적절 한 옵션을 선택 하는 업데이트를 수행할 수 있는 구독자에 대 한는 **게시자에서 커밋** 열:  
  
-   즉시 업데이트 구독에 대해 **동시에 변경 내용 커밋** 을 선택합니다.  
  
-   지연 업데이트 구독에 대해 **변경 내용 대기 및 가능 시 커밋** 을 선택합니다.  
  
## 참고 항목  
 [끌어오기 구독 만들기](../../relational-databases/replication/create-a-pull-subscription.md)   
 [밀어넣기 구독 만들기](../../relational-databases/replication/create-a-push-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [트랜잭션 복제를 위한 업데이트 가능 구독](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  