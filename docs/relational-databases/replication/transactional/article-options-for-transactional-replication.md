---
title: "트랜잭션 복제를 위한 아티클 옵션 | Microsoft Docs"
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
  - "아티클 [SQL Server 복제], 트랜잭션 복제 옵션"
  - "트랜잭션 복제, 아티클 옵션"
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 트랜잭션 복제를 위한 아티클 옵션
  트랜잭션 게시의 아티클에는 여러 가지 옵션이 있습니다. 트랜잭션 복제를 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   게시자에서 구독자로 변경 내용이 전파되는 방법을 지정합니다. 자세한 내용은 참조 [트랜잭션 아티클에 대 한 변경 내용이 전파 되는 방법을 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)합니다.  
  
-   저장 프로시저의 실행 결과를 복제하도록 지정합니다. 이는 많은 데이터에 영향을 주는 유지 관리 관련 저장 프로시저의 결과를 복제할 때 유용합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
-   제약 조건 및 트리거를 구독자로 복사할지 여부와 같은 스키마 옵션을 지정합니다. 자세한 내용은 참조 [스키마 옵션 지정](../../../relational-databases/replication/publish/specify-schema-options.md)합니다.  
  
-   행 필터와 열 필터를 사용합니다. 테이블 아티클을 필터링하여 게시할 데이터 파티션을 만들 수 있습니다. 자세한 내용은 참조 [데이터를 게시 하는 필터](../../../relational-databases/replication/publish/filter-published-data.md)합니다.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  