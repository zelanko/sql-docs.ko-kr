---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 718605c140bcf6e44cd78c9b07b8b649e0f593bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65714790"
---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  각 실행 단계에서 데이터 흐름 구성 요소에 의해 소비된 시간을 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|단계의 고유 ID(식별자)입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|package_name|**nvarchar(260)**|실행 중에 시작된 첫 번째 패키지의 이름입니다.|  
|task_name|**nvarchar(4000)**|데이터 흐름 태스크의 이름입니다.|  
|subcomponent_name|**nvarchar(4000)**|데이터 흐름 구성 요소의 이름입니다.|  
|phase|**nvarchar(128)**|실행 단계의 이름입니다.|  
|start_time|**datetimeoffset(7)**|단계가 시작된 시간입니다.|  
|end_time|**datetimeoffset(7)**|단계가 종료된 시간입니다.|  
|execution_path|**nvarchar(max)**|데이터 흐름 태스크의 실행 경로입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 뷰는 데이터 흐름 구성 요소의 각 실행 단계(예: 유효성 검사, 실행 전, 실행 후, PrimeOutput, ProcessInput)에 대한 행을 표시합니다. 각 행은 특정 실행 단계의 시작 및 종료 시간을 표시합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 catalog.execution_component_phases 뷰를 사용하여 모든 단계에서 특정 패키지가 실행하는 데 걸린 총 시간(**active_time**)과 패키지에 대해 경과된 총 시간(**total_time**)을 찾습니다.  
  
> [!WARNING]  
>  catalog.execution_component_phases 뷰는 패키지 실행의 로깅 수준이 성능 또는 자세히로 설정된 경우에 이 정보를 제공합니다. 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)을 참조하세요.  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>사용 권한  
 이 뷰를 보려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
