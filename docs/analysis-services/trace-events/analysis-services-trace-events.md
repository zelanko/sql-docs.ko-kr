---
title: "Analysis Services 추적 이벤트 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- events [Analysis Services]
- event classes [Analysis Services], about event classes
- Profiler [SQL Server Profiler], Analysis Services
- event classes [Analysis Services]
ms.assetid: 6fb219cc-f37e-437a-a544-01cec0953571
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b97d63ba708128fbd4d42f2e5278273609d144e1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-trace-events"></a>Analysis Services 추적 이벤트
  인스턴스에서 생성되는 추적 이벤트를 캡처한 다음 분석하여 Microsoft SQL SSAS(Server Analysis Services) 인스턴스의 작업을 따라갈 수 있습니다.  추적 이벤트는 관련된 추적 이벤트를 더 쉽게 찾을 수 있도록 그룹화되어 있습니다.  각 추적 이벤트에는 이벤트와 관련된 데이터 집합이 포함되어 있습니다. 모든 데이터 조각이 모든 이벤트와 관련이 있는 것은 아닙니다.  
  
 추적 이벤트는 **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**를 사용하여 시작하고 캡처하거나( [SQL Server Profiler를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)참조) XMLA 명령에서 **SQL Server 확장 이벤트** 로 시작하고 나중에 분석할 수 있습니다( [SQL Server 확장 이벤트를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)참조).  
  
 다음 표에서는 각 이벤트 범주 및 해당 범주의 이벤트에 대해 설명합니다. 각 표에는 다음 열이 있습니다.  
  
**이벤트 ID**  
 이벤트 유형을 식별하는 정수 값입니다. 이 값은 이벤트 유형을 필터링하기 위해 테이블 또는 XML 파일로 변환된 추적을 읽을 때 항상 유용합니다.  
  
**이벤트 이름**  
 Analysis Services 클라이언트 응용 프로그램에서 이벤트에 지정된 이름입니다.  
  
**이벤트 설명**  
 이벤트에 대한 간단한 설명  
  
 **[Command Events 이벤트 범주](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 명령에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|15|Command Begin|명령을 시작합니다.|  
|16|Command End|명령을 종료합니다.|  
  
 **[Discover Events 이벤트 범주](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 검색 요청에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|36|Discover Begin|검색 요청을 시작합니다.|  
|38|Discover End|검색 요청을 종료합니다.|  
  
 **[Discover Server State 이벤트 범주](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 서버 상태 검색에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|서버 상태 검색이 시작되었습니다.|  
|34|Server State Discover Data|서버 상태 검색 응답의 내용입니다.|  
|35|Server State Discover End|서버 상태 검색이 종료되었습니다.|  
  
 **[Errors and Warnings 이벤트 범주](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 서버 오류에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|17|오류|서버 오류입니다.|  
  
 **[File Load and Save 이벤트 범주](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 파일 로드 및 저장 작업 보고에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|90|파일 로드를 시작합니다.|파일 로드를 시작합니다.|  
|91|파일 로드를 종료합니다.|파일 로드를 종료합니다.|  
|92|파일 저장을 시작합니다.|파일 저장을 시작합니다.|  
|93|파일 저장을 종료합니다.|파일 저장을 종료합니다.|  
|94|PageOut을 시작합니다.|PageOut을 시작합니다.|  
|95|PageOut을 종료합니다.|PageOut을 종료합니다.|  
|96|PageIn을 시작합니다.|PageIn을 시작합니다.|  
|97|PageIn을 종료합니다.|PageIn을 종료합니다.|  
  
 **[잠금 이벤트 범주](../../analysis-services/trace-events/lock-events-category.md)**  
  
 잠금 관련 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|50|Deadlock|메타데이터 잠금 교착 상태입니다.|  
|51|Lock Timeout|메타데이터 잠금 제한 시간입니다.|  
|52|Lock Acquired|Lock Acquired|  
|53|Lock Released|Lock Released|  
|54|Lock Waiting|Lock Waiting|  
  
 **[Notification Events 이벤트 범주](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 알림 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|39|알림|알림 이벤트입니다.|  
|40|사용자 정의|사용자 정의 이벤트입니다.|  
  
 **[Progress Reports 이벤트 범주](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 진행률 보고에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|진행률 보고서를 시작합니다.|  
|6|Progress Report End|진행률 보고서가 종료되었습니다.|  
|7|Progress Report Current|진행률 보고서가 현재 처리되고 있습니다.|  
|8|Progress Report Error|진행률 보고서 오류입니다.|  
  
 **[Queries Events 범주](../../analysis-services/trace-events/queries-events-category.md)**  
  
 쿼리에 대한 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|쿼리를 시작합니다.|  
|10|쿼리 끝|쿼리를 종료합니다.|  
  
 **[Query Processing 이벤트 범주](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 쿼리를 실행하는 동안의 키 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|70|Query Cube Begin|쿼리 큐브를 시작합니다.|  
|71|Query Cube End|쿼리 큐브를 종료합니다.|  
|72|Calculate Non Empty Begin|비어 있지 않음 계산을 시작합니다.|  
|73|Calculate Non Empty Current|비어 있지 않음 계산을 현재 실행 중입니다.|  
|74|Calculate Non Empty End|비어 있지 않음 계산을 종료합니다.|  
|75|Serialize Results Begin|결과 직렬화를 시작합니다.|  
|76|Serialize Results Current|결과 직렬화를 현재 실행 중입니다.|  
|77|Serialize Results End|결과 직렬화를 종료합니다.|  
|78|Execute MDX Script Begin|MDX 스크립트 실행을 시작합니다.|  
|79|Execute MDX Script Current|MDX 스크립트를 현재 실행 중입니다. 사용되지 않습니다.|  
|80|Execute MDX Script End|MDX 스크립트 실행을 종료합니다.|  
|81|Query Dimension|쿼리 차원입니다.|  
|11|Query Subcube|사용 빈도 기반 최적화에 대한 쿼리 하위 큐브입니다.|  
|12|Query Subcube Verbose|세부 정보가 포함된 쿼리 하위 큐브입니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|60|Get Data From Aggregation|집계 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|61|Get Data From Cache|캐시 중 하나의 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|82|VertiPaq SE Query Begin|VertiPaq SE 쿼리|  
|83|VertiPaq SE Query End|VertiPaq SE 쿼리|  
|84|Resource Usage|명령 및 쿼리 종료 후에 읽기, 쓰기 및 CPU 사용량을 보고합니다.|  
|85|VertiPaq SE Query Cache Match|VertiPaq SE 쿼리 캐시를 사용합니다.|  
|98|Direct Query Begin|직접 쿼리를 시작합니다.|  
|99|Direct Query End|직접 쿼리를 종료합니다.|  
  
 **[Security Audit 이벤트 범주](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 데이터베이스 감사 이벤트 클래스 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|1.|Audit Login|클라이언트가 SQL Server의 인스턴스를 실행하는 서버에 대한 연결을 요청하는 경우와 같이 추적이 시작된 이후의 새 연결 이벤트를 모두 수집합니다.|  
|2|Audit Logout|클라이언트가 연결 끊기 명령을 보내는 등 추적이 시작된 이후의 새 연결 끊기 이벤트를 모두 수집합니다.|  
|4|Audit Server Starts And Stops|서비스 종료, 시작 및 일시 중지 동작을 기록합니다.|  
|18|Audit Object Permission Event|개체 사용 권한의 변경 내용을 기록합니다.|  
|19|Audit Admin Operations Event|서버 백업, 복원, 동기화, 연결, 분리, 이미지 로드 및 이미지 저장을 기록합니다.|  
  
 [Session Events 이벤트 범주](../../analysis-services/trace-events/session-events-event-category.md)  
  
 세션 이벤트 모음입니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|기존 사용자 연결입니다.|  
|42|Existing Session|기존 세션입니다.|  
|43|Session Initialize|세션을 초기화합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Profiler를 사용하여 Analysis Services 모니터링](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  
