---
title: MSmerge_genhistory (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a56efcc95965d3af9d01f618baba416a65226ce
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807885"
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSmerge_genhistory** 테이블 (보존 기간) 구독자에서 인식 하는 각 세대에 대해 하나의 행을 포함 합니다. 교환 기간 동안 공통 generation을 보내지 못하게 하고 백업에서 복원한 구독자를 다시 동기화하는 데 사용됩니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|구독자에서 generation에 의해 식별되는 변경 사항의 전역 식별자입니다.|  
|**pubid**|**uniqueidentifier**|게시 식별자입니다.|  
|**generation**|**bigint**|생성 값입니다.|  
|**art_nick**|**int**|아티클의 애칭입니다.|  
|**애칭**|**varbinary(1001)**|이미 이 generation이 있음이 알려진 다른 구독자의 애칭 목록입니다. 이미 해당되는 변경 사항을 알고 있는 구독자에게 generation을 보내는 것을 방지하는 데 사용합니다. 애칭 목록의 애칭은 검색을 더욱 효과적으로 하기 위해 정렬된 순서로 유지 관리됩니다. 이 필드에 수용할 수 있는 것보다 애칭 수가 많은 경우에는 이러한 최적화가 도움이 되지 않습니다.|  
|**coldate**|**datetime**|현재 generation이 테이블에 추가된 날짜입니다.|  
|**발견 했습니다**|**tinyint**|generation의 상태입니다.<br /><br /> **0** = 열려 있습니다.<br /><br /> **1** = 닫힙니다.<br /><br /> **2** = 닫혀 있고 다른 구독자에서 발생 합니다.|  
|**changecount**|**int**|지정된 generation에 반영된 변경 횟수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
