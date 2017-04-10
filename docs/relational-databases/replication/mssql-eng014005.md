---
title: "MSSQL_ENG014005 | Microsoft Docs"
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
  - "MSSQL_ENG014005 오류"
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG014005
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14005|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시를 삭제할 수 없습니다. 게시에 대한 구독이 존재합니다.|  
  
## 설명  
 하나 이상의 연결된 구독이 있는 게시를 삭제하려 했습니다. 연결된 구독이 없는 경우에만 게시를 삭제할 수 잇습니다.  
  
## 사용자 동작  
 게시를 삭제하기 전에 구독을 삭제합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 게시를 삭제하는 경우 게시를 삭제하기 전에 연결된 구독을 모두 자동으로 삭제하는 옵션이 제공됩니다. 저장 프로시저를 사용하는 경우에는 먼저 명시적으로 구독을 삭제해야 합니다. 자세한 내용은 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) 및 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)를 참조하세요.  
  
 게시에 대한 구독이 없거나 게시를 만들 때 이러한 오류가 나타나는 경우에는 이전 구독을 완전히 제거하지 않았을 수 있습니다. 실행 [sp_removedbreplication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 모든 개체 및 설정을 제거 하려면 데이터베이스에 복제 될 때까지 관련이 있습니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  