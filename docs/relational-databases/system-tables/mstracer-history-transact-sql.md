---
title: MStracer_history (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8c9f554d57935921c068ad25cb51991c47cdbd2a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881485"
---
# <a name="mstracer_history-transact-sql"></a>MStracer_history(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MStracer_history** 테이블은 구독자에서 수신 된 모든 추적 프로그램 토큰의 레코드를 유지 관리 합니다. 이 테이블은 배포 데이터베이스에 저장되며 성능 모니터링을 위해 복제에 사용됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|추적 프로그램 토큰을 고유하게 식별합니다.|  
|**agent_id**|**int**|추적 프로그램 토큰 레코드를 처리한 에이전트를 식별합니다.|  
|**subscriber_commit**|**datetime**|구독자에서 추적 프로그램 토큰 레코드를 접수한 날짜 및 시각입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
