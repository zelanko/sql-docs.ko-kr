---
title: MSSQLSERVER_10507 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 90d22a2b85d2f6257af927158484af8927a4ce11
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10507|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_STMT_DOES_NOT_MATCH|  
|메시지 텍스트|**@stmt** 및 **@module_or_batch** 또는 **@plan_handle** 및 **@statement_start_offset**으로 지정된 문이 지정된 모듈 또는 일괄 처리 문과 일치하지 않아 계획 지침 '%.\*ls'을(를) 만들 수 없습니다. 모듈 또는 일괄 처리 문과 일치하도록 값을 수정하십시오.|  
  
## <a name="explanation"></a>설명  
지정한 모듈 또는 일괄 처리 문이 지정된 문 또는 문 오프셋 값과 일치하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
모듈 또는 일괄 처리 문과 일치하도록 지정된 매개 변수 값을 수정하십시오.  
  
## <a name="see-also"></a>참고 항목  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
