---
title: "MSSQLSERVER_3413 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 38900b11bc5e2892ea85f22db2a6c1490d6399fb
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3413|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|MARKDB|  
|메시지 텍스트|데이터베이스 ID %d. 데이터베이스를 주의 대상으로 표시할 수 없습니다. sys.databases.database_id의 Getnext NC 검색이 실패했습니다. 오류 로그에서 이전 오류를 참조하여 원인을 확인하고 관련 문제를 모두 해결하십시오.|  
  
## <a name="explanation"></a>설명  
카탈로그에서 사용자 데이터베이스를 SUSPECT로 표시하려는 동안 예기치 않은 오류가 발생했습니다. SUSPECT 상태는 지속되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
이전 오류를 참조하여 문제를 해결하십시오.  
  

