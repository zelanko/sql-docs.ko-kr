---
title: MSSQLSERVER_10537 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a3dfb73f5ca3b073cf0d5ded864669f977c6aee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048584"
---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
