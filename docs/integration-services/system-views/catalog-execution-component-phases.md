---
title: catalog.execution_component_phases | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: b3459ce6d7e9eb0b9580ffa54e3b87e16f3e8fb0
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  각 실행 단계에서 데이터 흐름 구성 요소에 의해 소비된 시간을 표시합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|단계의 고유 ID(식별자)입니다.|  
|execution_id|**bigint**|실행 인스턴스의 고유 ID입니다.|  
|package_name|**nvarchar (260)**|실행 중에 시작된 첫 번째 패키지의 이름입니다.|  
|task_name|**nvarchar(4000)**|데이터 흐름 태스크의 이름입니다.|  
|subcomponent_name|**nvarchar(4000)**|데이터 흐름 구성 요소의 이름입니다.|  
|phase|**nvarchar (128)**|실행 단계의 이름입니다.|  
|start_time|**(7)**|단계가 시작된 시간입니다.|  
|end_time|**(7)**|단계가 종료된 시간입니다.|  
|execution_path|**nvarchar(max)**|데이터 흐름 태스크의 실행 경로입니다.|  
  
## <a name="remarks"></a>주의  
 이 뷰는 데이터 흐름 구성 요소의 각 실행 단계(예: 유효성 검사, 실행 전, 실행 후, PrimeOutput, ProcessInput)에 대한 행을 표시합니다. 각 행은 특정 실행 단계의 시작 및 종료 시간을 표시합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 catalog.execution_component_phases 뷰를 사용 하 여 모든 단계에서 실행의 특정 패키지에 소요 된 시간의 총 크기를 찾을 수 (**active_time**), 및 패키지에 대 한 총 경과 시간 (**total_time**).  
  
> [!WARNING]  
>  catalog.execution_component_phases 뷰는 패키지 실행의 로깅 수준이 성능 또는 자세히로 설정된 경우에 이 정보를 제공합니다. 자세한 내용은 [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)을 참조하세요.  
  
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
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
> [!NOTE]  
>  서버에서 작업을 수행할 권한이 있으면 작업에 대한 정보를 볼 수 있는 권한도 있습니다. 행 수준 보안이 적용됩니다. 따라서 볼 수 있는 권한이 있는 행만 표시됩니다.  
  
  
