---
title: MSrepl_identity_range (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83dcaf5b06f5664699e0d6fe9cd6ca509ce46930
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="msreplidentityrange-transact-sql"></a>MSrepl_identity_range(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_identity_range** 테이블은 id 범위 관리 지원을 제공 합니다. 이 테이블은 게시, 배포 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**테이블 이름**|**sysname**|테이블의 이름입니다.|  
|**identity_support**|**int**|자동 ID 범위 처리를 사용하는지 여부를 지정합니다. 0은 자동 ID 범위 처리를 사용하지 않음을 지정합니다.|  
|**next_seed**|**bigint**|자동 ID 범위를 사용하는 경우에 다음 범위의 시작 지점을 나타냅니다.|  
|**pub_range**|**bigint**|게시자 ID의 범위 크기입니다.|  
|**range**|**bigint**|조정 시 구독자에게 할당되는 연속 ID 값의 크기입니다.|  
|**max_identity**|**bigint**|ID 범위의 최대 경계입니다.|  
|**threshold**|**int**|ID 범위 임계값 비율입니다.|  
|**current_max**|**bigint**|할당할 수는 있지만 꼭 할당할 필요는 없는 현재 최대값입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
