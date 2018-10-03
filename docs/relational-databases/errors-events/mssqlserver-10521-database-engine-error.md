---
title: MSSQLSERVER_10521 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5e7e54dbf0728f3cc2705153f1bd9c56e9b000c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646101"
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10521|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_PARAM_NEEDED|  
|메시지 텍스트|**@type**이 '%ls'(으)로 지정되었고 매개 변수 '%ls'이(가) NULL이므로 계획 지침 '%.\*ls'을(를) 만들 수 없습니다. 이 유형은 매개 변수에 NULL이 아닌 값이 필요합니다. 매개 변수에 NULL이 아닌 값을 지정하거나, 매개 변수에 NULL 값을 허용하는 유형으로 유형을 변경하십시오.|  
  
## <a name="explanation"></a>설명  
**@type**에 지정된 유형에서 지정된 매개 변수에 NULL이 아닌 값이 필요하지만 NULL 값이 지정되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
매개 변수에 NULL이 아닌 값을 지정하거나, 매개 변수에 NULL 값을 허용하는 유형으로 유형을 변경하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
