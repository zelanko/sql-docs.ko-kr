---
title: "MSSQL_ENG021385 | Microsoft Docs"
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
  - "MSSQL_ENG021385 오류"
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021385
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21385|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|스냅숏이 게시 '%s'을(를) 처리하지 못했습니다. 활성 스키마 변경 작업 또는 추가 중인 새 아티클 때문인 것 같습니다.|  
  
## 설명  
 아티클 추가 또는 삭제 및 게시된 개체의 스키마 변경 등 게시 데이터베이스에 진행 중인 변경 내용이 있을 때 스냅숏 에이전트가 실행되면 이 오류가 발생합니다.  
  
## 사용자 동작  
 게시 데이터베이스에 대한 변경이 완료된 후에 스냅숏 에이전트를 다시 시작합니다. 자세한 내용은 참조 [시작 및 중지 복제 에이전트 & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  