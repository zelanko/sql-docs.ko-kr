---
title: MSSQLSERVER_10507 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68829d55be0b080e9b4beb9d7b284e3f57a46581
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305913"
---
# <a name="mssqlserver_10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10507|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_STMT_DOES_NOT_MATCH|  
|메시지 텍스트|**\@stmt** 및 **\@module_or_batch** 또는 **\@plan_handle** 및 **\@statement_start_offset**으로 지정된 문이 지정한 모듈 또는 일괄 처리 문과 일치하지 않아서 계획 지침 ‘%.*\*ls’을(를) 만들 수 없습니다. 모듈 또는 일괄 처리 문과 일치하도록 값을 수정하십시오.|  
  
## <a name="explanation"></a>설명  
지정한 모듈 또는 일괄 처리 문이 지정된 문 또는 문 오프셋 값과 일치하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
모듈 또는 일괄 처리 문과 일치하도록 지정된 매개 변수 값을 수정하십시오.  
  
## <a name="see-also"></a>참고 항목  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
