---
title: MSSQLSERVER_10521 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ecaffb9e40024eca7cbeac77f4b50058e5440cee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62870612"
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10521|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_PARAM_NEEDED|  
|메시지 텍스트|계획 지침 ' %. \*l s 때문에 `@type` 지정 된 매개 변수 ' % l s '와 ' % l s '은 NULL입니다. 이 유형은 매개 변수에 NULL이 아닌 값이 필요합니다. 매개 변수에 NULL이 아닌 값을 지정하거나, 매개 변수에 NULL 값을 허용하는 유형으로 유형을 변경하십시오.|  
  
## <a name="explanation"></a>설명  
 `@type`에 지정된 유형이 지정된 매개 변수에 대해 NULL 값을 허용하지 않지만 NULL 값이 제공되었습니다.  
  
## <a name="user-action"></a>사용자 동작  
 매개 변수에 NULL이 아닌 값을 지정하거나, 매개 변수에 NULL 값을 허용하는 유형으로 유형을 변경하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
