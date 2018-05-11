---
title: MSSQLSERVER_8689 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf60cb3bb8959b42446b872ffce2e379a608ca70
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8689|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|USEPLAN_ERR_NO_DB|  
|메시지 텍스트|USE PLAN 힌트에 지정된 데이터베이스 '%.*ls'이(가) 없습니다. 기존 데이터베이스를 지정하십시오.|  
  
## <a name="explanation"></a>설명  
USE PLAN 힌트에 지정된 데이터베이스가 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
USE PLAN 힌트에 지정된 모든 데이터베이스가 있는지 확인하십시오.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 힌트&#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-query.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
  
