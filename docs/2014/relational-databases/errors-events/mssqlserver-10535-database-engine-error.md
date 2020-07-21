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
ms.openlocfilehash: 68070291c5e7f50d423b74338dc1f6baeb9c6dfa
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554118"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_create_plan_guide_from_handle &#40;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
