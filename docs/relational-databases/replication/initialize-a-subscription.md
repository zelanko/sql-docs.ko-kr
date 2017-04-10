---
title: "구독 초기화 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스냅숏 복제 [SQL Server], 구독 초기화"
  - "트랜잭션 복제, 구독 초기화"
  - "구독 초기화 [SQL Server 복제]"
  - "구독 [SQL Server 복제], 초기화"
  - "구독 초기화 [SQL Server 복제], 구독 초기화 정보"
  - "병합 복제 [SQL Server 복제], 구독 초기화"
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 구독 초기화
  복제 토폴로지의 구독자는 구독한 게시에 있는 각 아티클의 스키마 복사본과 저장 프로시저, 트리거 및 메타데이터 테이블과 같이 필요한 모든 복제 개체를 포함하도록 초기화되어야 합니다. 일반적으로 구독자를 초기화하면 초기 데이터 집합도 구독자로 전달됩니다. 기본 초기화 메서드는 스키마, 복제 개체 및 데이터를 포함하는 전체 스냅숏을 사용하지만 전체 스냅숏 없이도 게시를 초기화할 수 있습니다.  
  
 자세한 내용은 [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) 및 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)를 참조하세요.  
  
  