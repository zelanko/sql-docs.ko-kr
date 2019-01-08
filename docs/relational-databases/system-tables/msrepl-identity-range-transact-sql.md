---
title: MSrepl_identity_range (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_identity_range_TSQL
- MSrepl_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_identity_range system table
ms.assetid: 6e92a8e8-7667-4c98-b1c4-46735bac50d8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4ba871571c3e5d82596e0ab252c9625ef645237
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52809245"
---
# <a name="msreplidentityrange-transact-sql"></a>MSrepl_identity_range(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSrepl_identity_range** 테이블은 id 범위 관리 지원을 제공 합니다. 이 테이블은 게시, 배포 및 구독 데이터베이스에 저장됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
