---
title: MSsync_states (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsync_states
- MSsync_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsync_states system table
ms.assetid: b25e17e1-7718-432e-a442-c4946741d474
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7c41d886550bef428590d4d2d39bb09434a9312
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807465"
---
# <a name="mssyncstates-transact-sql"></a>MSsync_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSsync_states** 어떤 게시가 동시 스냅숏 모드는 추적 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Integration Services 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)   
 [백업 및 복원 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [로그 전달 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
