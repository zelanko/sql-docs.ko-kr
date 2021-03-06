---
description: MSmerge_dynamic_snapshots(Transact-SQL)
title: MSmerge_dynamic_snapshots (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_dynamic_snapshots_TSQL
- MSmerge_dynamic_snapshots
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_dynamic_snapshots system table
ms.assetid: a5592b3c-731b-4fc9-ae4b-2602ed78248e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51e98246a61d18206015e358a83aee5c66a26711
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547093"
---
# <a name="msmerge_dynamic_snapshots-transact-sql"></a>MSmerge_dynamic_snapshots(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_dynamic_snapshots** 테이블은 매개 변수가 있는 행 필터를 사용 하 여 병합 게시에 대해 정의 된 각 파티션에 대해 필터링 된 데이터 스냅숏의 위치를 추적 합니다. 이 테이블은 **게시** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|병합 파티션의 ID입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|파티션에 대한 필터링된 데이터 스냅샷의 위치입니다.|  
|**last_updated**|**datetime**|필터링된 데이터 스냅샷을 새로 고친 날짜입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
