---
title: MSSQLSERVER_601 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2bd673d06329937145bb3eff3dacbb6bb5afe40e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|601|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|데이터 이동으로 인해 NOLOCK으로 계속 검색할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 다른 트랜잭션에 의해 업데이트 또는 삭제된 데이터를 읽으려 하므로 쿼리를 계속 실행할 수 없습니다. 쿼리에서 NOLOCK 잠금 힌트나 READ UNCOMMITTED 트랜잭션 격리 수준 중 하나를 사용하고 있습니다.  
  
일반적으로 다른 트랜잭션에 의해 변경된 데이터에 대한 액세스는 해당 데이터에 설정된 잠금으로 인해 거부됩니다. 그러나 NOLOCK 잠금 힌트 및 READ UNCOMMITTED 트랜잭션 격리 수준을 사용하면 다른 트랜잭션에 의해 잠긴 데이터를 쿼리가 읽을 수 있게 됩니다. 아직 커밋되지 않아 변경될 수 있는 값을 읽을 수 있으므로 이를 커밋되지 않은 읽기라고 합니다.  
  
## <a name="user-action"></a>사용자 동작  
이 오류가 발생하면 쿼리가 취소됩니다. 쿼리를 다시 전송하거나 NOLOCK 잠금 힌트를 제거하십시오.  
  
## <a name="see-also"></a>참고 항목  
[MSSQLSERVER_605](../../relational-databases/errors-events/mssqlserver-605-database-engine-error.md)  
[테이블 힌트&#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-table.md)  
[SELECT&#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](~/t-sql/statements/set-transaction-isolation-level-transact-sql.md)  
  
