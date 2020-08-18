---
description: MSSQLSERVER_10536
title: MSSQLSERVER_10536 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a22480940730da65e3274bd9d2fd6a74d72ae479
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338039"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|10536|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_TOO_MANY_STMTS|  
|메시지 텍스트|지정된 **\@plan_handle**에 해당하는 일괄 처리 또는 모듈에 적합한 문이 1000개 이상 포함되어 있으므로 계획 지침 ‘%.\*ls’를 만들 수 없습니다. 각 문에 **statement_start_offset** 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드세요.|  
  
## <a name="explanation"></a>설명  
지정된 **\@plan_handle**에 해당하는 일괄 처리 또는 모듈에 적합한 문이 1000개 이상 포함되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
각 문에 **statement_start_offset** 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드세요.  
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
