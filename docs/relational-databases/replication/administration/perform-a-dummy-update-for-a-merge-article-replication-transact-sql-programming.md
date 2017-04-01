---
title: "병합 아티클에 대해 더미 업데이트 수행(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "sp_mergedummyupdate"
  - "더미 업데이트 [SQL Server 복제]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 병합 아티클에 대해 더미 업데이트 수행(복제 Transact-SQL 프로그래밍)
  병합 복제에서는 복제 프로세스의 일부로 트리거가 사용됩니다. 게시된 테이블이 업데이트될 경우 업데이트 트리거가 발생합니다. WRITETEXT 및 UPDATETEXT 작업을 수행할 때와 같은 일부 경우에는 트리거를 발생시키지 않고 데이터를 업데이트할 수 있습니다. 이러한 경우 변경 내용을 명시적으로 복제하려면 더미 UPDATE 문을 추가해야 합니다. 복제 저장 프로시저를 사용하여 더미 UPDATE 문을 추가할 수 있습니다.  
  
### 더미 UPDATE 문을 추가하려면  
  
1.  더미 업데이트가 필요한 병합 게시된 테이블의 행에 대해 UPDATETEXT와 같은 작업을 실행합니다.  
  
2.  서버 (게시자 또는 구독자) 변경에 데이터베이스에서 실행 [sp_mergedummyupdate (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md)합니다. 테이블에 변경에 대 한 지정 **@source_object**, 및에 대 한 변경된 된 행의 고유 식별자 **@rowguid**합니다.  
  
3.  구독을 동기화하여 변경된 행을 복제합니다.  
  
  