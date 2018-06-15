---
title: MSdynamicsnapshotjobs (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8cdfc74bad45bcb3e77bfdf8b438df45e1491633
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33004230"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotjobs** 테이블은 필터링된 된 데이터 스냅숏을 생성 하기 위해 적용 하는 매개 변수가 있는 행 필터 정보를 추적 합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링된 데이터 스냅숏 작업의 ID입니다.|  
|**name**|**sysname**|필터링된 데이터 스냅숏 작업의 이름입니다.|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID입니다.|  
|**job_id**|**uniqueidentifier**|배포자에서 SQL Server 에이전트 작업의 ID입니다.|  
|**agent_id**|**int**|SQL Server 에이전트의 ID입니다.|  
|**dynamic_filter_login**|**sysname**|평가 하는 데 사용 되는 값은 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터의 함수입니다.|  
|**dynamic_filter_hostname**|**sysname**|평가 하는 데 사용 되는 값은 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터의 함수입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|필터링된 데이터 스냅숏을 사용하는 경우에 스냅숏 파일을 읽을 대상 폴더 경로입니다.|  
|**partition_id**|**int**|작업이 속한 데이터 파티션의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
