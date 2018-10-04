---
title: MSSQLSERVER_10535 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7f03e63cda6732cd5c39c3242543cf3a6b2b242
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213223"
---
# <a name="mssqlserver10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10535|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NO_PLAN|  
|메시지 텍스트|지정된 계획 핸들에 해당하는 계획 캐시에 계획이 없으므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 캐시된 계획 핸들을 지정하십시오. 캐시된 계획 핸들 목록을 보려면 sys.dm_exec_query_stats 동적 관리 뷰를 쿼리하십시오.|  
  
## <a name="explanation"></a>설명  
 지정된 계획 핸들에 해당하는 계획 캐시에 계획이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 캐시된 계획 핸들을 지정하십시오. 캐시된 계획 핸들 목록을 보려면 sys.dm_exec_query_stats 동적 관리 뷰를 쿼리하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
