---
title: "MSSQL_ENG020596 | Microsoft Docs"
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
  - "MSSQL_ENG020596 오류"
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020596
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20596|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%s' 또는 db_owner의 멤버만 익명 에이전트를 삭제할 수 있습니다.|  
  
## 설명  
 익명 구독에 대한 에이전트를 삭제할 권한이 없습니다. 호출할 때 사용 되는 로그인 [sp_dropanonymousagent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) 구성원 이어야는 **sysadmin** 배포자에서 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할의 사용자 또는 배포 데이터베이스의 에이전트를 처음 실행 하는 것 이어야 합니다.  
  
## 사용자 동작  
 적절 한 자격 증명으로 로그인 하 고 실행 **sp_dropanonymousagent**합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  