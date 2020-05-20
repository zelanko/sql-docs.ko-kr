---
title: MSmerge_identity_range_allocations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f9adbc21b0c226746c879bf1b32377c93b2d76c1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829268"
---
# <a name="msmerge_identity_range_allocations-transact-sql"></a>MSmerge_identity_range_allocations(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range_allocations** 테이블은 게시 된 아티클에 대 한 id 범위 할당 기록을 게시자와 구독자 모두에 추적 하는 데 사용 됩니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**nvarchar(128)**|게시 데이터베이스의 이름입니다.|  
|**게시물**|**nvarchar(128)**|게시의 이름입니다.|  
|**자료**|**nvarchar(128)**|아티클의 이름입니다.|  
|**구독자**|**nvarchar(128)**|구독자 이름입니다.|  
|**subscriber_db**|**nvarchar(128)**|구독 데이터베이스의 이름입니다.|  
|**is_pub_range**|**bit**|게시자에 ID 범위가 할당되었는지 여부를 나열합니다.|  
|**ranges_allocated**|**tinyint**|할당된 ID 범위의 수입니다.|  
|**range_begin**|**numeric (38)**|범위의 시작 값입니다.|  
|**range_end**|**numeric (38)**|범위의 마지막 값입니다.|  
|**next_range_begin**|**numeric (38)**|할당할 다음 범위의 시작 값입니다.|  
|**next_range_end**|**numeric (38)**|할당할 다음 범위의 마지막 값입니다.|  
|**max_used**|**numeric (38)**|사용된 최고 ID 값입니다.|  
|**time_of_allocation**|**datetime**|할당된 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
