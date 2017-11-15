---
title: "MSSQLSERVER_10519 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 2161f49985d7e88db78f80da855894b93ca4f5a6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10519|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|메시지 텍스트|**@hints**에 지정된 힌트를 **@stmt** 또는 **@statement_start_offset**으로 지정된 문에 적용할 수 없으므로 계획 지침 '%.\*ls'을(를) 만들 수 없습니다. 힌트를 문에 적용할 수 있는지 확인하십시오.|  
  
## <a name="explanation"></a>설명  
**@hints**에 지정된 힌트를 **@stmt** 또는 **@statement_start_offset**으로 지정된 문에 적용할 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
문에 적용할 수 있는 힌트를 지정하십시오.  
  
## <a name="see-also"></a>관련 항목:  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
