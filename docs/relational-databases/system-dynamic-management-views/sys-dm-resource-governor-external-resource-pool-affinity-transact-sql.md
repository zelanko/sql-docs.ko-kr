---
title: sys.dm_resource_governor_external_resource_pool_affinity (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4439cddb4af80a5d76a5b4e3600fd5e5ede6b900
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636481"
---
# <a name="sysdmresourcegovernorexternalresourcepoolaffinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] ~ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

현재 외부 리소스 풀 구성에 대 한 CPU 선호도 정보를 반환합니다.
  
|열 이름|데이터 형식|Description|
|----------------|---------------|-----------------|
|pool_id|**int**|외부 리소스 풀의 ID입니다. Null을 허용하지 않습니다.|
|processor_group|**smallint**|Windows 논리 프로세서 그룹의 ID입니다. Null을 허용하지 않습니다.|
|cpu_mask|**bigint**|이 풀과 연결 된 Cpu를 나타내는 이진 마스크입니다. Null을 허용하지 않습니다.|
  
## <a name="remarks"></a>Remarks

풀의 선호도 사용 하 여 만든 `AUTO` 선호도 없기 때문에이 보기에 표시 되지 않습니다. 자세한 내용은 참조 하세요. 합니다 [CREATE EXTERNAL RESOURCE POOL &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) 및 [ALTER EXTERNAL RESOURCE POOL &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) 문.

## <a name="permissions"></a>사용 권한

`VIEW SERVER STATE` 권한이 필요합니다.

## <a name="see-also"></a>참고자료

[SQL Server에서 머신 러닝을 위한 리소스 거버넌스](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[외부 스크립트 설정 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
