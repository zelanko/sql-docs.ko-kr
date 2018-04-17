---
title: MSmerge_identity_range (Transact SQL) | Microsoft Docs
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
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c50e81c520d8c70c0fb243f6466bd05ec51e5436
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range** 테이블은 게시에 구독에 대 한 id 열에 할당 된 숫자 범위를 추적 하는 데 복제에서 자동으로 관리 하는 범위 할당 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|지정된 구독의 고유 ID입니다.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**range_begin**|**numeric(38)**|현재 범위의 시작 ID 값입니다.|  
|**range_end**|**numeric(38)**|현재 범위의 끝 ID 값입니다.|  
|**next_range_begin**|**numeric(38)**|할당될 다음 범위의 시작 ID 값입니다.|  
|**next_range_end**|**numeric(38)**|할당될 다음 범위의 끝 ID 값입니다.|  
|**is_pub_range**|**bit**|값이 **1** id 범위가 게시에 할당 되는 경우.|  
|**max_used**|**numeric(38)**|할당할 수 있는 최대 ID 값입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
