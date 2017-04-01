---
title: "데이터 흐름 분석 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# 데이터 흐름 분석
  [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** 데이터베이스 뷰를 사용하여 패키지의 데이터 흐름을 분석할 수 있습니다. 이 뷰는 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 이 정보를 사용하여 각 구성 요소로 보내진 행을 자세하게 파악할 수 있습니다.  
  
> [!NOTE]  
>  catalog.execution_data_statistics 뷰를 사용하여 정보를 캡처하려면 로깅 수준을 **자세히**로 설정해야 합니다.  
  
 다음 예에서는 패키지의 구성 요소 간에 보내진 행 수를 표시합니다.  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 다음 예에서는 특정 실행 중 각 구성 요소가 보낸 밀리초당 행 수를 계산합니다. 계산되는 값은 다음과 같습니다.  
  
-   **total_rows** - 구성 요소가 보낸 모든 행의 합계  
  
-   **wall_clock_time_ms** - 각 구성 요소에 대한 총 실행 경과 시간(밀리초)  
  
-   **num_rows_per_millisecond** - 각 구성 요소가 보낸 밀리초당 행 수  
  
 **HAVING** 절은 계산에서 0으로 나누기 오류를 방지하기 위해 사용됩니다.  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## 관련 작업  
 [데이터 흐름 디버깅](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## 관련 항목:  
 [데이터 흐름의 데이터](../../integration-services/data-flow/data-in-data-flows.md)  
  
  