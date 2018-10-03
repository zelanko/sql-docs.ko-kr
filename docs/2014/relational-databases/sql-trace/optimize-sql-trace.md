---
title: SQL 추적 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b4c021e29180c25981582bab0d1ecb888345e82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165973"
---
# <a name="optimize-sql-trace"></a>SQL 추적 최적화
  SQL 추적을 실행하면 데이터 수집을 위해 시스템 리소스가 사용되기 때문에 성능 비용이 발생하지만 여러 가지 방법으로 이 비용을 최소화할 수 있습니다. 추적으로 인한 성능 비용을 최적화하려면 다음을 시도하십시오.  
  
-   명령 프롬프트를 사용하여 추적을 실행해 봅니다. 그래픽 사용자 인터페이스를 사용하면 성능이 저하됩니다. 자세한 내용은 [sp_trace_create&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)를 참조하세요.  
  
-   자주 발생하는 이벤트를 포함하지 않습니다. 가능하면 특정 이벤트 클래스와 필터를 사용하여 추적 범위를 좁힙니다. 수집하는 추적 이벤트가 적을수록 추적 지원에 필요한 시스템 리소스가 줄어듭니다.  
  
-   추적에 포커스를 맞추어 관련 데이터를 제공하는 이벤트만 수집합니다. 예를 들어 추적에서 교착 상태를 식별하려면 **Lock:Deadlock** 이벤트 클래스를 포함하고 **Lock:Acquired** 이벤트 클래스는 제외합니다. 두 이벤트 클래스를 모두 포함하면 추적이 획득한 잠금에 모두 응답해야 하므로 실행 비용은 두 배가 됩니다.  
  
-   중복 데이터를 수집하지 않습니다. 예를 들어 **SQL:BatchStarted** 와 **SQL:BatchCompleted**를 수집할 경우 **SQL:BatchStarted** 이벤트 클래스의 텍스트 데이터만 수집하여 결과 집합 크기를 최소화할 수 있습니다.  
  
-   추적 정의에 필터를 사용합니다. 예를 들어 특정 사용자가 임시 쿼리를 수행하는 동안 성능이 느려지면 **LoginName**에 필터를 만듭니다. 필터를 설정하여 **LoginName** 이 해당 사용자 이름과 일치하는 이벤트만 포함합니다.  
  
 성능에 크게 영향을 미치는 이벤트를 추적해야 할 경우 다음 방법 중 하나를 사용하여 서버에 대한 성능 영향을 제한하십시오.  
  
-   단기간에 추적을 실행합니다. 중지 시간을 설정하여 추적이 실행되는 시간을 제어할 수 있습니다. 이벤트 클래스를 제한하거나 이벤트를 필터링할 수 없을 때 특히 유용합니다. 중지 시간을 설정하면 성능 저하를 멈출 수 있습니다.  
  
-   추적 결과의 크기를 제한합니다. 추적 결과의 크기를 최대 파일 크기로 제한할 수 있습니다. 이렇게 하면 파일 크기 제한에 도달했을 때 성능 비용이 중지됩니다(파일 롤오버를 사용하지 않는 경우).  
  
-   반환되는 이벤트의 수를 제한합니다. [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 를 사용하면 추적을 테이블에 저장하고 최대 행 개수를 설정하여 반환되는 이벤트의 수를 제한할 수 있습니다. 최대 행 개수에 도달한 후에도 추적 결과가 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 화면에 반환되지만 테이블에 결과를 기록하는 데 필요한 비용이 없어집니다.  
  
## <a name="see-also"></a>관련 항목  
 [추적 필터링](../sql-trace/filter-a-trace.md)  
  
  
