---
title: MSSQLSERVER_10502 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33bb9c3e6bc3e3f1d198be344832451eafe9b22c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095668"
---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10502|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_DUP_FOUND|  
|메시지 텍스트|@stmt 및 @module_or_batch 또는 @plan_handle 및 @statement_start_offset으로 지정된 문이 데이터베이스의 기존 계획 지침 '%.\*ls'과(와) 일치하므로 계획 지침 '%.*ls'을(를) 만들 수 없습니다. 새 계획 지침을 만들기 전에 기존 계획 지침을 삭제하십시오.|  
  
## <a name="explanation"></a>설명  
지정된 문에 대한 계획 지침이 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
새 계획 지침을 만들기 전에 기존 계획 지침을 삭제하십시오.  
  
## <a name="see-also"></a>참고 항목  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
