---
title: MSSQLSERVER_601 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0cb9c16487408f5be8598a7fee3c748efd8591e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183255"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
    
## <a name="details"></a>설명  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
