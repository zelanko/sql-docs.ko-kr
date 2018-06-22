---
title: MSSQLSERVER_10536 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ffa9509c55632c5f041f060c499be0a8bc7cbf4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080198"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10536|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_TOO_MANY_STMTS|  
|메시지 텍스트|계획 지침 ' %. \*l s 때문에 일괄 처리 또는 모듈에 해당 하는 지정 된 `@plan_handle` 적합 한 문이 1000 개 이상 포함 합니다. 각 문에 `statement_start_offset` 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드십시오.|  
  
## <a name="explanation"></a>설명  
 지정된 `@plan_handle`에 해당하는 일괄 처리 또는 모듈에 적합한 문이 1000개 이상 포함되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 각 문에 `statement_start_offset` 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드십시오.  
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
