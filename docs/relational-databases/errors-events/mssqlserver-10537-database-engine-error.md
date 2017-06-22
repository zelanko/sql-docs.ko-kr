---
title: "MSSQLSERVER_10537 | Microsoft 문서"
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
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7b71c60cbafb79dac3f93d9b46ef03040a3b1196
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10537|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_DUP_ENABLED|  
|메시지 텍스트|활성화된 계획 지침 '%.\*ls'에 문의 시작 오프셋 값 및 동일한 범위가 들어 있으므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 지정된 계획 지침을 활성화하기 전에 기존 계획 지침을 비활성화하십시오.|  
  
## <a name="explanation"></a>설명  
기존 계획 지침에 지정된 계획 지침의 문과 동일한 범위 및 시작 오프셋 값이 포함되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
지정된 계획 지침을 활성화하기 전에 기존 계획 지침을 비활성화하십시오.  
  
## <a name="see-also"></a>관련 항목:  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

