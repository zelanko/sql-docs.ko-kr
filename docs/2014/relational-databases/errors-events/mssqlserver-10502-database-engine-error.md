---
title: MSSQLSERVER_10502 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b9094d390a6a28251382c1bad3f12467ef39a7f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36078815"
---
# <a name="mssqlserver10502"></a>MSSQLSERVER_10502
    
## <a name="details"></a>설명  
  
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
  
## <a name="see-also"></a>관련 항목  
 [계획 지침](../performance/plan-guides.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
