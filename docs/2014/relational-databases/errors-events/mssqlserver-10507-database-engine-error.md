---
title: MSSQLSERVER_10507 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c32441ebcf8804f712fad3061bbd380864db3426
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214053"
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|10507|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_STMT_DOES_NOT_MATCH|  
|메시지 텍스트|계획 지침 ' %. \*l s에서 지정 된 문이 `@stmt` 하 고 `@module_or_batch`, 또는 `@plan_handle` 및 `@statement_start_offset`을 하거나 하지 않는 지정된 된 모듈의 문과 일치 일괄 처리 합니다. 모듈 또는 일괄 처리 문과 일치하도록 값을 수정하십시오.|  
  
## <a name="explanation"></a>설명  
 지정한 모듈 또는 일괄 처리 문이 지정된 문 또는 문 오프셋 값과 일치하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
 모듈 또는 일괄 처리 문과 일치하도록 지정된 매개 변수 값을 수정하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
