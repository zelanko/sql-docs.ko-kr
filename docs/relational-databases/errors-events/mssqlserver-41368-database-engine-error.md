---
title: MSSQLSERVER_41368 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: f635eecdbaab6cbcb078fa59992928a66315a736
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|41368|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|메시지 텍스트|READ COMMITTED 격리 수준을 사용한 메모리 액세스에 최적화된 테이블 액세스는 자동 커밋 트랜잭션에서만 지원됩니다. 명시적 또는 암시적 트랜잭션에서는 지원되지 않습니다. WITH (SNAPSHOT) 같은 테이블 힌트를 사용하여 메모리 액세스에 최적화된 테이블에 대해 지원되는 격리 수준을 제공합니다.|  
  
## <a name="explanation"></a>설명  
READ COMMITTED 격리 수준을 사용한 메모리 최적화 테이블 액세스는 자동 커밋 트랜잭션에서만 지원됩니다. 자세한 내용은 [메모리 내 테이블 및 프로시저와의 트랜잭션](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)을 참조하세요.  
  
BEGIN TRANSACTION으로 시작된 명시적 트랜잭션에서 메모리 최적화 테이블에 액세스할 때 IMPLICIT_TRANSACTIONS가 ON으로 설정되어 있으면 READ COMMITTED 격리 수준이 지원되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
명시적 또는 암시적 READ COMMITTED 트랜잭션에서 메모리 최적화 테이블에 액세스할 때는 SNAPSHOT을 사용하여 테이블에 액세스합니다. 이렇게 하려면 테이블 힌트 WITH (SNAPSHOT)를 사용(자세한 내용은 [메모리 내 테이블 및 프로시저와의 트랜잭션](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) 참조)하거나 데이터베이스 옵션 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT을 ON으로 설정(자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md) 참조)할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
