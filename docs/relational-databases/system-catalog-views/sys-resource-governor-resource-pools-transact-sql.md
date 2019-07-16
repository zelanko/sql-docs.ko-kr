---
title: sys.resource_governor_resource_pools (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_resource_pools
- resource_governor_resource_pools
- sys.resource_governor_resource_pools_TSQL
- resource_governor_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_resource_pools catalog view
ms.assetid: 56793e9c-aa90-452e-88c6-d9b799239888
author: stevestein
ms.author: sstein
ms.openlocfilehash: 06ed4b4820ce7a6e6483df6efd1de2e8fbadf954
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904462"
---
# <a name="sysresourcegovernorresourcepools-transact-sql"></a>sys.resource_governor_resource_pools(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 저장된 리소스 풀 구성을 반환합니다. 뷰의 각 행에 따라 풀의 구성이 결정됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|리소스 풀의 고유한 ID입니다. Null을 허용하지 않습니다.|  
|name|**sysname**|리소스 풀의 이름입니다. Null을 허용하지 않습니다.|  
|min_cpu_percent|**int**|CPU 충돌이 있으면 리소스 풀의 모든 요청에 대해 보장된 평균 CPU 대역폭입니다. Null을 허용하지 않습니다.|  
|max_cpu_percent|**int**|CPU 충돌이 있으면 리소스 풀의 모든 요청에 대해 허용된 최대 평균 CPU 대역폭입니다. Null을 허용하지 않습니다.|  
|min_memory_percent|**int**|리소스 풀의 모든 요청에 대해 보장된 메모리 양입니다. 이것은 다른 리소스 풀과 공유되지 않습니다. Null을 허용하지 않습니다.|  
|max_memory_percent|**int**|이 리소스 풀의 요청에서 사용할 수 있는 총 서버 메모리의 비율입니다. Null을 허용하지 않습니다. 유효한 최대는 풀 최소에 따라 다릅니다. 예를 들어 max_memory_percent는 100으로 설정할 수 있지만 유효한 최대는 낮습니다.|  
|cap_cpu_percent|**int**|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 리소스 풀의 모든 요청에서 받을 CPU 대역폭의 하드 캡입니다. 최대 CPU 대역폭을 지정된 수준으로 제한합니다. 허용되는 값의 범위는 1에서 100까지입니다.|  
|min_iops_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 풀에 대한 볼륨 설정당 최소 IOPS(초당 I/O 작업) 0 = 예약 없음. null일 수 없습니다.|  
|max_iops_per_volume|**int**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 풀에 대한 볼륨 설정당 최대 IOPS(초당 I/O 작업) 0 = 제한 없음. null일 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 카탈로그 뷰는 저장된 메타데이터를 표시합니다. 메모리 구성을 표시 하려면 해당 동적 관리 뷰를 사용 하 여 [sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 내용을 보려면 VIEW ANY DEFINITION 권한이 필요하고, 내용을 변경하려면 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [리소스 관리자 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.resource_governor_external_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)  
  
  
