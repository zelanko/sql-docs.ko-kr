---
title: MSsync_states (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 58f7f1e887039a5b2ef497a52643a793985f090e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758662"
---
# <a name="mssync_states-transact-sql"></a>MSsync_states(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSsync_states** 테이블은 아직 동시 스냅숏 모드에 있는 게시를 추적 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;&#40;테이블 Integration Services](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [로그 전달 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
