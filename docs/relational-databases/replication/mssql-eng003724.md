---
title: "MSSQL_ENG003724 | Microsoft Docs"
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
  - "MSSQL_ENG003724 오류"
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG003724
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3724|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|%S_MSG '%.*ls'은(는) 복제에 사용 중이므로 %S_MSG할 수 없습니다.|  
  
## 설명  
 데이터베이스의 개체 복제 되 면 것으로 표시 되는 시스템 테이블에 복제 **sysarticles** (에 대 한 스냅숏 및 트랜잭션 게시의 경우) 또는 **sysmergearticles** (병합 게시용). 복제된 개체를 삭제하려고 하면 이 오류가 발생합니다.  
  
## 사용자 동작  
 데이터베이스 개체를 삭제하기 전에 복제되지 않았는지 확인합니다. 예를 들어  
  
-   게시 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 게시에서 해당 아티클을 삭제합니다. 자세한 내용은 참조 [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다.  
  
-   구독 데이터베이스에서 오류가 발생한 경우 개체를 삭제하기 전에 해당 구독을 삭제합니다. 자세한 내용은 참조 [게시를 구독할](../../relational-databases/replication/subscribe-to-publications.md)합니다. 트랜잭션 게시에 대한 구독의 경우 전체 게시 대신 개별 아티클에 대한 구독을 삭제할 수 있습니다. 자세한 내용은 참조 [sp_dropsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)합니다.  
  
 에 복제 되지 않은 데이터베이스에서이 오류가 발생 하는 경우 실행 [sp_removedbreplication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 되도록 복제 되는 데이터베이스의 개체 표시 되지 않습니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  