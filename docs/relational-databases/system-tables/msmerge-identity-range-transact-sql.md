---
title: MSmerge_identity_range (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 9e62d2e8cf46de73bf8f0881b398437ab4ef58fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909041"
---
# <a name="msmerge_identity_range-transact-sql"></a>MSmerge_identity_range(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range** 테이블은 복제에서 자동으로 이러한 범위 할당을 관리 하는 게시에 대 한 구독에 대 한 id 열에 할당 된 숫자 범위를 추적 하는 데 사용 됩니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|지정된 구독의 고유 ID입니다.|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**range_begin**|**numeric (38)**|현재 범위의 시작 ID 값입니다.|  
|**range_end**|**numeric (38)**|현재 범위의 끝 ID 값입니다.|  
|**next_range_begin**|**numeric (38)**|할당될 다음 범위의 시작 ID 값입니다.|  
|**next_range_end**|**numeric (38)**|할당될 다음 범위의 끝 ID 값입니다.|  
|**is_pub_range**|**bit**|Id 범위가 게시에 할당 된 경우 값 **1** 입니다.|  
|**max_used**|**numeric (38)**|할당할 수 있는 최대 ID 값입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
