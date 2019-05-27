---
title: 데이터 흐름 분석 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e67c5448a6625b37c7fb17bc24ea6bdd7cb879ff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061597"
---
# <a name="analysis-of-data-flow"></a>데이터 흐름 분석
  사용할 수는 [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB` 데이터베이스 뷰를 패키지의 데이터 흐름을 분석 합니다. 이 뷰는 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 이 정보를 사용하여 각 구성 요소로 보내진 행을 자세하게 파악할 수 있습니다.  
  
> [!NOTE]  
>  catalog.execution_data_statistics 뷰를 사용하여 정보를 캡처하려면 로깅 수준을 **자세히** 로 설정해야 합니다.  
  
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
  
 `HAVING` 계산에서 0으로 나누기 오류를 방지 하기 위해 절을 사용 합니다.  
  
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
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 디버깅](troubleshooting/debugging-data-flow.md)  
  
 [패키지 실행 문제 해결 도구](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 흐름의 데이터](data-flow/data-in-data-flows.md)  
  
  
