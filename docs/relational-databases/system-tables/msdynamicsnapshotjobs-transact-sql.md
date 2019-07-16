---
title: MSdynamicsnapshotjobs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8822b0e7c56fe109a251365050f5aed9cdef178
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907365"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSdynamicsnapshotjobs** 테이블은 필터링된 된 데이터 스냅숏을 생성 하기 위해 적용 하는 매개 변수가 있는 행 필터 정보를 추적 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링된 데이터 스냅숏 작업의 ID입니다.|  
|**name**|**sysname**|필터링된 데이터 스냅숏 작업의 이름입니다.|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID입니다.|  
|**job_id**|**uniqueidentifier**|배포자에서 SQL Server 에이전트 작업의 ID입니다.|  
|**agent_id**|**int**|SQL Server 에이전트의 ID입니다.|  
|**dynamic_filter_login**|**sysname**|평가에 사용 된 값을 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터의 함수입니다.|  
|**dynamic_filter_hostname**|**sysname**|평가에 사용 된 값을 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터의 함수입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|필터링된 데이터 스냅숏을 사용하는 경우에 스냅숏 파일을 읽을 대상 폴더 경로입니다.|  
|**partition_id**|**int**|작업이 속한 데이터 파티션의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
