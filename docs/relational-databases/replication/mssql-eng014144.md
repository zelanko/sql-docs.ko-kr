---
title: "MSSQL_ENG014144 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014144 오류"
ms.assetid: fdc744d5-530e-48c4-9420-cca032fd482b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG014144
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14144|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|구독자 '%s'을(를) 삭제할 수 없습니다. 게시 데이터베이스 '%s'에 이 구독자에 대한 구독이 있습니다.|  
  
## 설명  
 구독자로 구성된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 구성된 활성 구독이 있으면 해당 인스턴스를 구독자 역할에서 제거할 수 없습니다.  
  
## 사용자 동작  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 구독자 상태를 변경하기 전에 연결된 구독을 모두 삭제합니다.  
  
1.  실행 [sp_helpsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 구독을 찾을 게시자의 게시 데이터베이스입니다.  
  
2.  실행 [sp_dropsubscription (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md) 구독을 삭제 하려면 게시 데이터베이스입니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  