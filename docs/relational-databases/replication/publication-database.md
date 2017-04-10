---
title: "게시 데이터베이스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.publicationdatabase.f1"
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 게시 데이터베이스
  게시 데이터베이스는 복제될 데이터 및 데이터베이스 개체의 원본인 게시자에 있는 데이터베이스입니다. 복제에 사용할 각 게시 데이터베이스는 활성화되어 있어야 합니다. 데이터베이스는 **sysadmin** 고정 서버 역할의 멤버가 다음과 같은 작업을 수행할 때 활성화됩니다.  
  
-   새 게시 마법사를 사용하여 데이터베이스에 게시를 만듭니다.  
  
-   **게시자 속성** 대화 상자에서 데이터베이스를 선택합니다.  
  
-   실행 **sp_replicationdboption** 옵션을 설정 하 고 **게시** (스냅숏 또는 트랜잭션 게시)에 또는 **병합 게시** (병합 게시의 경우)에 대 한를 **True**합니다.  
  
## 옵션  
 **데이터베이스**  
 게시할 데이터 및 데이터베이스 개체를 포함하는 데이터베이스의 이름을 선택합니다.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시자 및 배포자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  