---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL020011 오류"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20011|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%2'에서 '%1'을(를) 실행할 수 없습니다.|  
  
## 설명  
 트랜잭션 복제 로그 판독기 에이전트가 실행 될 때와 같은 처리 하는 동안 다양 한 상황에서에서이 오류를 발생할 수 있습니다 **sp_replcmds** (프로세스 'sp_replcmds'에서 실행할 수 없는 \< 서버 이름>) 또는 **sp_repldone** (프로세스 'sp_repldone'에서 실행할 수 없는 \< 서버 이름>).  
  
## 사용자 동작  
 방금 백업에서 복원한 데이터베이스에서이 오류가 발생 한 경우 실행을 포함 하 여 백업 및 복원 설명서에 설명 된 단계를 수행 했는지 확인 **sp_replrestart** 해당 하는 경우. 자세한 내용은 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)을 참조하세요.  
  
 이 오류는 내부 처리 오류입니다. 이 오류가 복원이 아닌 다른 상황에서 발생한 경우에는 일반적으로 복제를 제거하고 다시 구성해야 합니다. 복제를 제거할 수 없으면 고객 지원 담당자에 문의하십시오.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  