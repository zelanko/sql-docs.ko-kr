---
title: MSSQLSERVER_10536 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b8c4e7237aa7ea39673b62543d77f9796c5bc46a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554108"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10536|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_TOO_MANY_STMTS|  
|메시지 텍스트|지정된 `@plan_handle`에 해당하는 일괄 처리 또는 모듈에 적합한 문이 1000개 이상 포함되어 있으므로 계획 지침 '%\**ls'을(를) 만들 수 없습니다. 각 문에 `statement_start_offset` 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드십시오.|  
  
## <a name="explanation"></a>설명  
 지정된 `@plan_handle`에 해당하는 일괄 처리 또는 모듈에 적합한 문이 1000개 이상 포함되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 각 문에 `statement_start_offset` 값을 지정하여 일괄 처리 또는 모듈의 각 문에 대해 계획 지침을 만드십시오.  
  
## <a name="see-also"></a>참고 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
