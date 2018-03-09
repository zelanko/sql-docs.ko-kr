---
title: sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
caps.latest.revision: "8"
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1f5fa2851b5b03708eb28c42d4e2496258d187b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmresourcegovernorexternalresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 및 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

현재 외부 리소스 풀 구성에 대 한 CPU 선호도 정보를 반환합니다.
  
|열 이름|데이터 형식|Description|
|----------------|---------------|-----------------|
|pool_id|**int**|외부 리소스 풀의 ID입니다. Null을 허용하지 않습니다.|
|processor_group|**smallint**|Windows 논리 프로세서 그룹의 ID입니다. Null을 허용하지 않습니다.|
|cpu_mask|**bigint**|이 풀과 연결 된 Cpu를 나타내는 이진 마스크입니다. Null을 허용하지 않습니다.|
  
## <a name="remarks"></a>주의

풀의 선호도 사용 하 여 만든 `AUTO` 선호도 없기 때문에이 보기에 표시 되지 않습니다. 자세한 내용은 참조는 [외부 리소스 풀 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 및 [외부 RESOURCE pool&#40; 변경 Transact SQL &#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) 문.

## <a name="permissions"></a>Permissions

`VIEW SERVER STATE` 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[SQL Server의 기계 학습에 대 한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys.dm_resource_governor_resource_pool_affinity &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
