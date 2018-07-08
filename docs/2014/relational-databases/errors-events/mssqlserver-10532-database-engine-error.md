---
title: MSSQLSERVER_10532 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be808412900aed583450824dca873deea4697f40
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409481"
---
# <a name="mssqlserver10532"></a>MSSQLSERVER_10532
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10532|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_NO_ELIGIBLE_STMT|  
|메시지 텍스트|계획 지침 ' %. \*l s로 지정 된 일괄 처리 또는 모듈 `@plan_handle` 계획 지침에 대 한 적합 한 문을 포함 하지 않습니다. `@plan_handle`에 다른 값을 지정하십시오.|  
  
## <a name="explanation"></a>설명  
 `@plan_handle`로 지정된 일괄 처리 또는 모듈이 계획 지침에 적합한 문을 포함하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 `@plan_handle`에 다른 값을 지정하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
