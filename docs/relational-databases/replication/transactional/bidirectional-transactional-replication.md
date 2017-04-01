---
title: "양방향 트랜잭션 복제 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "양방향 복제"
  - "트랜잭션 복제, 양방향 복제"
  - "양방향 트랜잭션 복제"
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 양방향 트랜잭션 복제
  양방향 트랜잭션 복제는 두 개의 서버가 서로 변경 내용을 교환할 수 있는 특수 트랜잭션 복제 토폴로지입니다. 각 서버는 데이터를 게시한 다음 상대 서버에서 게시한 것과 동일한 데이터가 포함된 게시를 구독합니다.  **@loopback_detection** 의 매개 변수 [sp_addsubscription (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 변경 내용을 구독자에만 보내집니다 하 고 게시자로 다시 전송 되 고 변경 발생 하지 않으면 TRUE로 설정 됩니다.  
  
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 이후 버전에서는이 토폴로지는 피어 투 피어 트랜잭션 복제 에서도 지원 되지만 양방향 복제 성능 향상된을 제공할 수 있습니다.  
  
## 참고 항목  
 [피어 투 피어 트랜잭션 복제](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  