---
title: "동기화 시 트리거 및 제약 조건의 동작 제어 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 24825a3c9c016588b4ac3d1a9c8fa29741e609b3
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>동기화 시 트리거 및 제약 조건의 동작 제어
  동기화하는 동안 복제 에이전트는 복제된 테이블에서 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [UPDATE&#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 및 [DELETE&#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 문을 실행합니다. 그러면 이 테이블에서 DML(데이터 조작 언어) 트리거가 실행될 수 있습니다. 그러나 동기화하는 동안 이러한 트리거 실행을 방지하거나 제약 조건을 적용하지 않아야 하는 경우가 있습니다. 이 동작은 트리거 또는 제약 조건을 만드는 방법에 따라 달라집니다.  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>동기화하는 동안 트리거 실행을 방지하려면  
  
1.  새 트리거를 만들 때 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)의 NOT FOR REPLICATION 옵션을 지정합니다.  
  
2.  기존 트리거에 대해서는 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)의 NOT FOR REPLICATION 옵션을 지정합니다.  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>동기화하는 동안 제약 조건을 적용하지 않으려면  
  
1.  새 CHECK 또는 FOREIGN KEY 제약 조건을 만들 때 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)의 제약 조건 정의에서 CHECK NOT FOR REPLICATION 옵션을 지정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
