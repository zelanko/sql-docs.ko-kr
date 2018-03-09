---
title: "MSSQLSERVER_8712 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6231e5d0aac503b257657130a2fecb4fa9699375
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8712|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|USEPLAN_ERR_NO_INDEX|  
|메시지 텍스트|USE PLAN 힌트에 지정된 인덱스 '%.*ls'이(가) 없습니다. 기존 인덱스를 지정하거나 지정된 이름의 인덱스를 만드십시오.|  
  
## <a name="explanation"></a>설명  
USE PLAN 힌트에 지정된 인덱스가 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
USE PLAN 힌트에 지정된 모든 인덱스가 있는지 확인하십시오.  
  
## <a name="see-also"></a>관련 항목:  
[쿼리 힌트&#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
  
