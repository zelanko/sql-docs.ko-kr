---
title: MSSQLSERVER_10531 | Microsoft 문서
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
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7e1c38822b6386d011723c15cdd7a58c48c65029
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187415"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10531|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NO_ELIGIBLE_STMT|  
|메시지 텍스트|사용자에게 적절한 권한이 없으므로 캐시에서 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 사용자가 계획 지침을 만들 수 있도록 VIEW SERVER STATE 권한을 부여하십시오.|  
  
## <a name="explanation"></a>설명  
 사용자에게 계획 캐시에서 지정된 계획 지침을 만들 수 있는 적절한 권한이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
 사용자가 계획 지침을 만들 수 있도록 VIEW SERVER STATE 권한을 부여하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
