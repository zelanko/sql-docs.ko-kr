---
title: "MSSQLSERVER_10520 | Microsoft 문서"
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
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57ba200cf6381ddc6d100d516bcf5f0168bb7262
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10520|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_PARAM_NOT_ALLOWED|  
|메시지 텍스트|@type이 '%ls'(으)로 지정되었고 매개 변수 '%ls'에 NULL이 아닌 값이 지정되었으므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 이 유형은 매개 변수에 NULL 값이 필요합니다. 매개 변수에 NULL을 지정하거나, 매개 변수에 NULL이 아닌 값을 허용하는 유형으로 유형을 변경하십시오.|  
  
## <a name="explanation"></a>설명  
@type에 지정된 유형에서 지정된 매개 변수에 NULL 값이 필요하지만 NULL이 아닌 값이 지정되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
매개 변수에 NULL을 지정하거나, 매개 변수에 NULL이 아닌 값을 허용하는 유형으로 유형을 변경하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
  

