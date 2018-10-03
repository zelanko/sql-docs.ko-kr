---
title: 동기화 (복제 TRANSACT-SQL 프로그래밍) 하는 동안 트리거 및 제약 조건 동작 제어 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9f7a3cefc4d85893cf3aa431c590971699215ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070953"
---
# <a name="control-the-behavior-of-triggers-and-constraints-during-synchronization-replication-transact-sql-programming"></a>동기화하는 동안 트리거 및 제약 조건 동작 제어(복제 Transact-SQL 프로그래밍)
  동기화하는 동안 복제 에이전트는 복제된 테이블에서 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [UPDATE&#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) 및 [DELETE&#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) 문을 실행합니다. 그러면 이 테이블에서 DML(데이터 조작 언어) 트리거가 실행될 수 있습니다. 그러나 동기화하는 동안 이러한 트리거 실행을 방지하거나 제약 조건을 적용하지 않아야 하는 경우가 있습니다. 이 동작은 트리거 또는 제약 조건을 만드는 방법에 따라 달라집니다.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>동기화하는 동안 트리거 실행을 방지하려면  
  
1.  새 트리거를 만들 때 [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)의 NOT FOR REPLICATION 옵션을 지정합니다.  
  
2.  기존 트리거에 대해서는 [ALTER TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)의 NOT FOR REPLICATION 옵션을 지정합니다.  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>동기화하는 동안 제약 조건을 적용하지 않으려면  
  
1.  새 CHECK 또는 FOREIGN KEY 제약 조건을 만들 때 [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)의 제약 조건 정의에서 CHECK NOT FOR REPLICATION 옵션을 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 만들기&#40;데이터베이스 엔진&#41;](../tables/create-tables-database-engine.md)  
  
  
