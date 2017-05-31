---
title: "MSSQLSERVER_10534 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 316e6b85f0bea4ff6f58da2b8ec0a9596f67364f
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10534|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INVALID_PARAMS|  
|메시지 텍스트|**@params**에 지정된 값이 잘못되었으므로 계획 지침 '%.\*ls'을(를) 만들 수 없습니다. *parameter_name parameter_type* 형식으로 값을 지정하거나 NULL을 지정하세요.|  
  
## <a name="explanation"></a>설명  
**@params**에 지정된 값이 잘못되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
*parameter_name parameter_type* 형식으로 값을 지정하거나 NULL을 지정하세요.  
  
## <a name="see-also"></a>관련 항목:  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

