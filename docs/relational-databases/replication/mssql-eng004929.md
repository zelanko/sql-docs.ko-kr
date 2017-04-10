---
title: "MSSQL_ENG004929 | Microsoft Docs"
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
  - "MSSQL_ENG004929 오류"
ms.assetid: 1d9b1d88-1fbf-4089-b392-687d3b0220ca
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG004929
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|4929|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|%S_MSG '%.*ls'은(는) 복제용으로 게시 중이므로 변경할 수 없습니다.|  
  
## 설명  
 이 오류는 일반적으로 트랜잭션 복제용으로 게시되는 테이블의 PRIMARY KEY 제약 조건을 삭제하려고 할 때 발생합니다. 트랜잭션 복제를 사용하려면 게시된 각 테이블의 기본 키가 필요하므로 이 제약 조건은 삭제할 수 없습니다.  
  
## 사용자 동작  
 이 제약 조건을 삭제하려면 해당 테이블과 연결된 아티클을 먼저 삭제합니다. 자세한 내용은 참조 [기사를 추가 하 고 기존 게시에서 아티클을 삭제할](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)합니다. 에 복제 되지 않은 데이터베이스에서이 오류가 발생 하는 경우 실행 [sp_removedbreplication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 되도록 복제 되는 데이터베이스의 개체 표시 되지 않습니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  