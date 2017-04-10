---
title: "동기화 중 스크립트 실행(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "동기화 [SQL Server 복제], 스크립트"
  - "스크립트 [SQL Server 복제], 동기화 및"
  - "sp_addscriptexec"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 동기화 중 스크립트 실행(복제 Transact-SQL 프로그래밍)
  복제는 트랜잭션 게시 및 병합 게시 구독자의 요청 시 스크립트 실행을 지원합니다. 이 기능은 복제 작업 디렉터리에 스크립트를 복사한 다음 **sqlcmd** 를 사용하여 구독자에서 스크립트를 적용합니다. 구독자의 스크립트를 트랜잭션 게시에 적용할 때 오류가 발생하면 기본적으로 배포 에이전트가 중지됩니다. 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 실행되도록 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 지정할 수 있습니다.  
  
### 스냅숏, 트랜잭션 또는 병합 게시의 모든 구독자에 대해 실행되도록 스크립트를 지정하려면  
  
1.  요청 시 실행되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 작성 및 테스트합니다.  
  
2.  게시에 대한 스냅숏 에이전트가 액세스할 수 있는 위치에 스크립트 파일을 저장합니다.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_addscriptexec (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md)합니다. **@publication**을 지정하고 **@scriptfile**에 2단계에서 만든 전체 UNC 경로를 포함하는 스크립트 파일의 이름을 지정하고 **@skiperror**에 다음 값 중 하나를 지정합니다.  
  
    -   **0** -에이전트에 오류가 발생 하면 스크립트 실행이 중지 됩니다.  
  
    -   **1** -에이전트를 오류를 기록 하 고 스크립트를 실행 하 여 오류가 발생 하면 계속 합니다.  
  
4.  지정된 스크립트는 구독을 동기화하기 위해 다음에 에이전트가 실행될 때 각 구독자에서 실행됩니다.  
  
## 참고 항목  
 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)  
  
  