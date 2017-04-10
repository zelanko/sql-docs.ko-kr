---
title: "동기화하는 동안 트리거 및 제약 조건 동작 제어(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "ID [SQL Server 복제]"
  - "제약 조건 [SQL Server], 복제"
  - "트리거 [SQL Server], 복제"
  - "트리거 [SQL Server 복제]"
  - "제약 조건 [SQL Server 복제]"
  - "NOT FOR REPLICATION 옵션"
  - "NFR 옵션"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 동기화하는 동안 트리거 및 제약 조건 동작 제어(복제 Transact-SQL 프로그래밍)
  복제 에이전트를 실행 하 여 동기화 중 [삽입 & #40; TRANSACT-SQL & #41;](../../t-sql/statements/insert-transact-sql.md), [업데이트 & #40; TRANSACT-SQL & #41;](../../t-sql/queries/update-transact-sql.md), 및 [삭제 및 #40; TRANSACT-SQL & #41;](../../t-sql/statements/delete-transact-sql.md) 일으킬 수 있는 데이터 조작 언어 (DML) 트리거를 실행할 수 있는 이러한 테이블에 복제 된 테이블에 대 한 문입니다. 그러나 동기화하는 동안 이러한 트리거 실행을 방지하거나 제약 조건을 적용하지 않아야 하는 경우가 있습니다. 이 동작은 트리거 또는 제약 조건을 만드는 방법에 따라 달라집니다.  
  
### 동기화하는 동안 트리거 실행을 방지하려면  
  
1.  새 트리거를 만들 때의 NOT FOR REPLICATION 옵션을 지정 합니다. [CREATE TRIGGER & #40; TRANSACT-SQL & #41;](../../t-sql/statements/create-trigger-transact-sql.md)합니다.  
  
2.  NOT FOR REPLICATION 옵션을 지정 하는 기존 트리거에 대 한 [ALTER TRIGGER & #40; TRANSACT-SQL & #41;](../../t-sql/statements/alter-trigger-transact-sql.md)합니다.  
  
### 동기화하는 동안 제약 조건을 적용하지 않으려면  
  
1.  새 CHECK 또는 FOREIGN KEY 제약 조건을 만들 때의 제약 조건 정의에서 CHECK NOT FOR REPLICATION 옵션을 지정 [CREATE TABLE & #40; TRANSACT-SQL & #41;](../../t-sql/statements/create-table-transact-sql.md)합니다.  
  
## 참고 항목  
 [테이블 및 #40; 데이터베이스 엔진 및 #41; 만들기](../../relational-databases/tables/create-tables-database-engine.md)  
  
  