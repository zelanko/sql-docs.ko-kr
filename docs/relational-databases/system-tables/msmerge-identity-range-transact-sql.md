---
title: MSmerge_identity_range (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27906e593020d45a9fb5e79be6ac53bc0e7fafcc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62904795"
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_identity_range** 테이블 게시를 구독에 대 한 id 열에 할당 된 숫자 범위 추적을 사용 하는 복제에서 자동으로 관리 하는 이러한 범위 할당 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|지정된 구독의 고유 ID입니다.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**range_begin**|**numeric(38)**|현재 범위의 시작 ID 값입니다.|  
|**range_end**|**numeric(38)**|현재 범위의 끝 ID 값입니다.|  
|**next_range_begin**|**numeric(38)**|할당될 다음 범위의 시작 ID 값입니다.|  
|**next_range_end**|**numeric(38)**|할당될 다음 범위의 끝 ID 값입니다.|  
|**is_pub_range**|**bit**|값이 **1** id 범위가 게시에 할당 된 경우.|  
|**max_used**|**numeric(38)**|할당할 수 있는 최대 ID 값입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
