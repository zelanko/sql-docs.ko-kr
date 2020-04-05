---
title: sys.dm_resource_governor_external_resource_pool_affinity (거래-SQL) | 마이크로 소프트 문서
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
ms.openlocfilehash: 77d0d322139be1f1c6086622855600a7c24fc4c9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664318"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_external_resource_pool_affinity (거래 SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 및 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

현재 외부 리소스 풀 구성에 대한 CPU 선호도 정보를 반환합니다.
  
|열 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|pool_id|**Int**|외부 리소스 풀의 ID입니다. Null을 허용하지 않습니다.|
|processor_group|**Smallint**|Windows 논리 프로세서 그룹의 ID입니다. Null을 허용하지 않습니다.|
|cpu_mask|**bigint**|이 풀과 연결된 CPU를 나타내는 이진 마스크입니다. Null을 허용하지 않습니다.|
  
## <a name="remarks"></a>설명

선호도를 통해 생성된 풀은 선호도가 없기 때문에 이 보기에 나타나지 `AUTO` 않습니다. 자세한 내용은 [트랜스트 SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) &#40;외부 리소스 풀 만들기 및 [외부 리소스 풀 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) 문을 참조하십시오.

## <a name="permissions"></a>사용 권한

`VIEW SERVER STATE` 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[SQL Server에서 머신 러닝을 위한 리소스 거버넌스](../../machine-learning/administration/resource-governor.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;거래-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[External Scripts Enabled 서버 구성 옵션](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
