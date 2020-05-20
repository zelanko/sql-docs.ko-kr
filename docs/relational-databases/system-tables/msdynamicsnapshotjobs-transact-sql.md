---
title: MSdynamicsnapshotjobs (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f717d5cf35349dcb99ec2022c5c0c92df5ea4286
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812810"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotjobs** 테이블은 필터링 된 데이터 스냅숏을 생성 하기 위해 적용 된 매개 변수가 있는 행 필터 정보를 추적 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링된 데이터 스냅샷 작업의 ID입니다.|  
|**name**|**sysname**|필터링된 데이터 스냅샷 작업의 이름입니다.|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID입니다.|  
|**job_id**|**uniqueidentifier**|배포자에서 SQL Server 에이전트 작업의 ID입니다.|  
|**agent_id**|**int**|SQL Server 에이전트의 ID입니다.|  
|**dynamic_filter_login**|**sysname**|게시에 대해 정의 된 매개 변수가 있는 행 필터에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수를 계산 하는 데 사용 되는 값입니다.|  
|**dynamic_filter_hostname**|**sysname**|게시에 대해 정의 된 매개 변수가 있는 행 필터에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수를 계산 하는 데 사용 되는 값입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|필터링된 데이터 스냅샷을 사용하는 경우에 스냅샷 파일을 읽을 대상 폴더 경로입니다.|  
|**partition_id**|**int**|작업이 속한 데이터 파티션의 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
