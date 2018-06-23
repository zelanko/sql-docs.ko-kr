---
title: MSSQLSERVER_10533 | Microsoft 문서
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
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 458716b859df07b3bef456a1c2e515168fc10744
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180517"
---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10533|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NAME_TOO_BIG|  
|메시지 텍스트|계획 지침 이름이 허용된 최대 문자 수인 124자를 초과하므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 125자 미만의 이름을 지정하십시오.|  
  
## <a name="explanation"></a>설명  
 계획 지침 이름이 허용된 최대 문자 수인 124자를 초과합니다.  
  
## <a name="user-action"></a>사용자 동작  
 125자 미만의 이름을 지정하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
