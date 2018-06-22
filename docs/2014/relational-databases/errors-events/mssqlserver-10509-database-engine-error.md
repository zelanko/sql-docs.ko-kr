---
title: MSSQLSERVER_10509 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fb203b703df342107384cf0c082917aea18c5f20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090214"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10509|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INVALID_STMT|  
|메시지 텍스트|계획 지침 ' %. \*l s에서 지정 된 문이 `@stmt` 또는 `@statement_start_offset` 구문 오류가 포함 되었거나이 계획 지침에 사용 하기에 적합 합니다. 올바른 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 안에 있는 문의 올바른 시작 위치를 지정하십시오. 올바른 시작 위치를 가져오려면 sys.dm_exec_query_stats 동적 관리 함수의 statement_start_offset 열을 쿼리하십시오.|  
  
## <a name="explanation"></a>설명  
 `@stmt` 또는 `@statement_start_offset`으로 지정된 문에 구문 오류가 있거나 계획 지침으로 사용하기에 적합하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 올바른 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 안에 있는 문의 올바른 시작 위치를 지정하십시오. 올바른 시작 위치를 가져오려면 sys.dm_exec_query_stats 동적 관리 함수의 statement_start_offset 열을 쿼리하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
