---
title: "트랜잭션 복제에 대한 게시 유형 | Microsoft Docs"
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
  - "트랜잭션 복제, 게시"
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 트랜잭션 복제에 대한 게시 유형
  트랜잭션 복제는 다음과 같은 3가지 게시 유형을 제공합니다.  
  
|게시 유형|설명|  
|----------------------|-----------------|  
|표준 트랜잭션 게시|구독자의 모든 데이터가 읽기 전용인 토폴로지에 적합합니다. 트랜잭션 복제는 구독자의 모든 데이터를 읽기 전용으로 변경하지 않습니다.<br /><br /> 표준 트랜잭션 게시는 Transact-SQL 또는 RMO(복제 관리 개체)를 사용하는 경우 기본적으로 생성됩니다. 새 게시 마법사를 사용하는 경우에는 **게시 유형** 페이지에서 **트랜잭션 게시** 를 선택하면 해당 게시가 생성됩니다.<br /><br /> 게시를 만드는 방법에 대 한 자세한 내용은 참조 [게시 데이터 및 데이터베이스 개체](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)합니다.|  
|피어 투 피어 토폴로지의 트랜잭션 게시|이 게시 유형의 특성은 다음과 같습니다.<br /><br /> -각 위치가 동일한 데이터를 가지며 게시자와 구독자 역할을 합니다.<br /><br /> -같은 행은 한 번에 한 위치에서만 변경될 수 있습니다.<br /><br /> -이 토폴로지는 고가용성 및 읽기 확장성이 필요한 서버 환경에 가장 적합합니다.<br /><br /> <br /><br /> 자세한 내용은 참조 [피어 투 피어 트랜잭션 복제](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)합니다.|  
  
## 참고 항목  
 [트랜잭션 복제](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  