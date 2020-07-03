---
title: MSdistribution_status (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_status_TSQL
- MSdistribution_status
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_status view
ms.assetid: 90d447de-3a4a-4f3e-aeab-e8fff6348361
author: stevestein
ms.author: sstein
ms.openlocfilehash: df060b429b48eb1e1a99c48dbb2789fce3e10833
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889161"
---
# <a name="msdistribution_status-transact-sql"></a>MSdistribution_status(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSdistribution_status** 뷰는 배포 데이터베이스의 상태 명령에 대 한 추가 정보를 제공 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|아티클을 식별합니다.|  
|**agent_id**|**int**|복제 에이전트를 식별합니다.|  
|**UndelivCmdsInDistDB**|**int**|구독자에 대한 배달을 보류 중인 명령 수입니다.|  
|**DelivCmdsInDistDB**|**int**|구독자로 배달된 명령 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
