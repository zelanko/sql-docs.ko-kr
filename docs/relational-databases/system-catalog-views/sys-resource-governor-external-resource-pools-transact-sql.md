---
title: sys.resource_governor_external_resource_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9ed2152873f40fd2f2ded34a11a2cfded2fbe2a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823542"
---
# <a name="sysresourcegovernorexternalresourcepools-transact-sql"></a>sys.resource_governor_external_resource_pools (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] ~ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

저장 된 외부 리소스 풀 구성을 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 뷰의 각 행에 따라 풀의 구성이 결정됩니다.
  
|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|
|pool_id|**int**|리소스 풀의 고유한 ID입니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 나중에 바꿀 수 있습니다.|
|NAME|**sysname**|리소스 풀의 이름입니다. Null을 허용하지 않습니다.|
|max_cpu_percent|**int**|CPU 충돌이 있으면 리소스 풀의 모든 요청에 대해 허용된 최대 평균 CPU 대역폭입니다. Null을 허용하지 않습니다.|
|max_memory_percent|**int**|이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리의 비율입니다. Null을 허용하지 않습니다. 유효한 최대는 풀 최소에 따라 다릅니다. 예를 들어 max_memory_percent는 100으로 설정할 수 있지만 유효한 최대는 낮습니다.|
|max_processes|**int**|동시 외부 프로세스의 최대 수입니다. 기본값은 0이며 제한 없음을 지정합니다. Null을 허용하지 않습니다.|
|version|**bigint**|내부 버전 번호입니다.|
  
## <a name="permissions"></a>사용 권한

VIEW SERVER STATE 권한이 필요합니다.

## <a name="see-also"></a>참고자료

[SQL Server에서 머신 러닝을 위한 리소스 거버넌스](../../advanced-analytics/r/resource-governance-for-r-services.md)

[리소스 관리자 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[sys.dm_resource_governor_resource_pools&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
