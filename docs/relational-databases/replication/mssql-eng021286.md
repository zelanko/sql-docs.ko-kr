---
title: "MSSQL_ENG021286 | Microsoft Docs"
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
  - "MSSQL_ENG021286 오류"
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021286
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21286|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|충돌 테이블 '%s'이(가) 없습니다.|  
  
## 설명  
 아티클에 대 한 충돌 테이블에 나열 된 경우이 오류는 발생 [sysmergearticles (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 실제로 존재 하지 않는 합니다. 병합 복제에 대해 게시된 테이블에서 열을 추가하거나 삭제해도 이 오류가 발생할 수 있습니다.  
  
## 사용자 동작  
 실행 [DBCC CHECKDB & #40; TRANSACT-SQL & #41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 확인 하려면 충돌 테이블이 없는 데이터베이스에 데이터 일관성 문제가 없는지를 나와 있습니다.  
  
 구독자에 충돌 테이블이 없는 경우 해당 구독을 삭제하고 다시 만듭니다. 게시자에 충돌 테이블이 없는 경우 모든 구독을 삭제하고 해당 게시를 삭제한 다음 게시 및 모든 구독을 다시 만듭니다. 자세한 내용은 참조 [게시 데이터 및 데이터베이스 개체](../../relational-databases/replication/publish/publish-data-and-database-objects.md) 및 [게시를 구독할](../../relational-databases/replication/subscribe-to-publications.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  