---
title: MSSQLSERVER_10520 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 79274cf031103e50151b6e93a9daff781005abad
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916175"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
    
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
 [Transact-sql&#41;sp_create_plan_guide &#40;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)  
  
  
