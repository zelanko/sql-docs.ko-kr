---
title: MSSQLSERVER_10520 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 353f4bc91c35b5000ab6a02f3b24a11225bc3014
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416602"
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
    
## <a name="details"></a>설명  
  
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
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)  
  
  
