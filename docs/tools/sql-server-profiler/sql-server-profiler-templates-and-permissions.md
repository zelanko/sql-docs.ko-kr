---
title: SQL Server Profiler 템플릿 및 권한 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47778dc7faf65628484dd30f8905b16646e91063
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704211"
---
# <a name="sql-server-profiler-templates-and-permissions"></a>SQL Server Profiler 템플릿 및 권한
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 내부적으로 쿼리를 해결하는 방법을 보여 줍니다. 이를 통해 관리자는 어떤 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 다차원 식이 서버에 전송되고 해당 서버에서 어떻게 데이터베이스 또는 큐브에 액세스하여 결과 집합을 반환하는지를 정확히 파악할 수 있습니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 다음을 수행할 수 있습니다.  
  
-   재사용 가능한 템플릿을 기반으로 한 추적을 만듭니다.  
  
-   추적이 실행됨에 따라 추적 결과를 감시합니다.  
  
-   추적 결과를 테이블에 저장합니다.  
  
-   필요에 따라 추적 결과를 시작, 중지, 일시 중지 및 수정합니다.  
  
-   추적 결과를 재생합니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 필요한 이벤트만 모니터링할 수 있습니다. 추적 내용이 너무 크면 원하는 정보별로 필터링하여 이벤트 데이터의 하위 집합을 수집할 수 있습니다. 너무 많은 이벤트를 모니터링하면 서버와 모니터링 프로세스에 오버헤드가 추가되어 특히 장기간 동안 모니터링할 때는 추적 파일이나 추적 테이블이 너무 커질 수가 있습니다.  
  
> [!NOTE]  
>  1GB보다 큰 추적 열 값은 오류를 반환하며 추적 출력에서 잘립니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[SQL Server Profiler 템플릿](../../tools/sql-server-profiler/sql-server-profiler-templates.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]와 함께 제공되는 미리 정의된 추적 템플릿에 대해 설명합니다.|  
|[SQL Server 프로파일러 실행에 필요한 권한](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]실행에 필요한 사용 권한에 대해 설명합니다.|  
|[추적 및 추적 템플릿 저장](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|추적 출력을 저장하고 추적 정의를 템플릿에 저장하는 방법에 대한 정보가 포함됩니다.|  
|[추적 템플릿 수정](../../tools/sql-server-profiler/modify-trace-templates.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 추적 템플릿을 수정하는 방법에 대해 설명합니다.|  
|[추적 시작](../../tools/sql-server-profiler/start-a-trace.md)|추적을 시작, 일시 중지 또는 중지할 때 발생하는 사항에 대한 정보가 포함됩니다.|  
|[Windows 성능 로그 데이터와 추적의 상관 관계 지정](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler를 사용하여 Windows 성능 로그 데이터와 추적의 상관 관계를 지정하는 방법에 대한 정보가 포함됩니다.|  
|[SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|추적을 사용하여 데이터의 문제를 해결하고 개체 이름을 추적에 표시하며 추적에서 이벤트를 찾는 방법에 대한 정보가 포함됩니다.|  
|[SQL Server Profiler를 사용하여 교착 상태 분석](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 교착 상태의 원인을 확인하는 방법에 대한 정보가 포함됩니다.|  
|[SQL Server Profiler에서 SHOWPLAN 결과로 쿼리 분석](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 실행 계획 및 실행 계획 통계 결과를 수집하여 표시하는 방법에 대한 정보가 포함됩니다.|  
|[SQL Server Profiler로 추적 필터링](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적 출력을 필터링하도록 데이터 열에 필터를 설정하는 방법에 대한 정보가 포함됩니다.|  
|[추적 재생](../../tools/sql-server-profiler/replay-traces.md)|추적 재생의 의미와 추적 재생에 필요한 사항을 설명하는 정보가 포함됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler 시작](../../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
