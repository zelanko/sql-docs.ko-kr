---
title: sys.resource_governor_workload_groups (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d24885b194f8614e393c7529fac0dc34eb3e15fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857231"
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 저장된 작업 그룹 구성을 반환합니다. 각 작업 그룹은 한 개의 리소스 풀만 구독할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|작업 그룹의 고유한 ID입니다. Null을 허용하지 않습니다.|  
|NAME|**sysname**|작업 그룹의 이름입니다. Null을 허용하지 않습니다.|  
|importance|**sysname**|**참고:** 중요도 동일한 리소스 풀의 작업 그룹에만 적용 됩니다.<br /><br /> 이 작업 그룹에 있는 요청의 상대적 중요도입니다. 중요도 다음 중 하나, 미디어를 사용 하 여 됨이 기본값: 낮음, 보통, 높음.<br /><br /> Null을 허용하지 않습니다.|  
|request_max_memory_grant_percent|**int**|단일 요청에 대한 최대 메모리 부여(%)입니다. 기본값은 25입니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 큰 쿼리가 한 번에 하나씩 실행 됩니다이 설정이 50% 보다 높은 경우. 따라서 쿼리가 실행되는 동안 메모리가 부족할 위험이 높아집니다.|  
|request_max_cpu_time_sec|**int**|단일 요청에 대한 최대 CPU 사용 제한입니다. 기본값은 0이며 제한 없음을 지정합니다. Null을 허용하지 않습니다.<br /><br /> **참고:** 자세한 내용은 참조 하십시오 [CPU Threshold Exceeded 이벤트 클래스](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)합니다.|  
|request_memory_grant_timeout_sec|**int**|단일 요청에 대한 메모리 부여 시간 초과(초)입니다. 기본값은 0이며 쿼리 비용에 따라 내부 계산을 사용합니다. Null을 허용하지 않습니다.|  
|max_dop|**int**|작업 그룹에 대한 최대 병렬 처리 수준입니다. 기본값은 0이며 글로벌 설정을 사용합니다. Null을 허용하지 않습니다.<br /><br /> **노드:** 이 설정은 쿼리 옵션을 재정의 **maxdop**합니다.|  
|group_max_requests|**int**|최대 동시 요처 수입니다. 기본값은 0이며 제한 없음을 지정합니다. Null을 허용하지 않습니다.|  
|pool_id|**int**|이 작업 그룹이 사용하는 리소스 풀의 ID입니다.|  
|external_pool_id|**int**|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 이 작업 그룹이 사용 하는 외부 리소스 풀의 ID입니다.|  
  
## <a name="remarks"></a>Remarks  
 카탈로그 뷰는 저장된 메타데이터를 표시합니다. 메모리 구성을 표시 하려면 해당 동적 관리 뷰를 사용 하 여 [sys.dm_resource_governor_workload_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)합니다.  
  
 리소스 관리자 구성이 변경되었지만 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 적용되지 않은 경우 저장 및 인-메모리 구성은 다를 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 내용을 보려면 VIEW ANY DEFINITION 권한이 필요하고, 내용을 변경하려면 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_resource_governor_workload_groups&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [리소스 관리자 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
