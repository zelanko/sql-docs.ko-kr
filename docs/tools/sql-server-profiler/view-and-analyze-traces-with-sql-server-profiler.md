---
title: SQL Server Profiler를 사용하여 추적 보기 및 분석 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], viewing traces
- SQL Server Profiler, viewing traces
- traces [SQL Server], viewing
- SQL Server Profiler, troubleshooting
- troubleshooting [SQL Server], traces
- events [SQL Server], finding inside trace
- Profiler [SQL Server Profiler], troubleshooting
- traces [SQL Server], events
ms.assetid: 17e821ca-a12e-4192-acc1-96765d9ae266
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 526eb2b2fbe378c542789665ee6f2fb73f14899b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="view-and-analyze-traces-with-sql-server-profiler"></a>SQL Server Profiler를 사용하여 추적 보기 및 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  추적에서 캡처한 이벤트를 보려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 정의된 추적 속성을 기반으로 데이터를 표시합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 분석하는 한 가지 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 같은 다른 프로그램으로 데이터를 복사하는 것입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자는 **Text** 데이터 열이 추적에 포함되어 있는 경우 SQL 일괄 처리와 RPC(원격 프로시저 호출) 이벤트가 있는 추적 파일을 사용할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에 사용할 수 있도록 올바른 이벤트와 열이 캡처되었는지 확인하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 열 때 추적 파일이 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 또는 SQL 추적 시스템 저장 프로시저로 생성된 경우 추적 파일에 .trc 파일 확장명이 없어도 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 SQL 추적 .log 파일 및 일반 SQL 스크립트 파일도 읽을 수 있습니다. trace.txt와 같이 .log 파일 확장명을 가지지 않은 SQL 추적 .log 파일을 열 때는 **SQLTrace_Log** 를 파일 형식으로 지정하세요.  
  
 추적 분석에 유용한 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 날짜 및 시간 표시 형식을 구성하여 추적 분석을 도울 수 있습니다.  
  
## <a name="troubleshooting-data"></a>데이터 문제 해결  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하면 **Duration**, **CPU**, **Reads**또는 **Writes** 데이터 열로 추적 또는 추적 파일을 그룹화하여 데이터의 문제를 해결할 수 있습니다. 예를 들어 잘 수행되지 않는 쿼리 또는 논리적 읽기 작업의 수가 비정상적으로 많은 쿼리 등의 데이터 문제를 해결할 수 있습니다.  
  
 추적을 테이블에 저장하고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 이벤트 데이터를 쿼리하면 추가 정보를 얻을 수 있습니다. 예를 들어 어떤 **SQL:BatchCompleted** 이벤트의 대기 시간이 가장 긴지 확인하려면 다음을 실행하십시오.  
  
```  
SELECT  TextData, Duration, CPU  
FROM    trace_table_name  
WHERE   EventClass = 12 -- SQL:BatchCompleted events  
AND     CPU < (Duration * 1000)  
```  
  
> [!NOTE]  
>  서버는 이벤트 기간을 마이크로초(10^-6초) 단위로 보고하고 이벤트에 사용되는 CPU 시간량을 밀리초(10^-3초) 단위로 보고합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 그래픽 사용자 인터페이스는 기본적으로 **Duration** 열을 밀리초 단위로 표시하지만 추적을 파일이나 데이터베이스 테이블에 저장하면 **Duration** 열 값이 마이크로초 단위로 기록됩니다.  
  
## <a name="displaying-object-names-when-viewing-traces"></a>추적을 볼 때 개체 이름 표시  
 개체 식별자(**개체 ID**)보다는 개체 이름을 표시하려면 **서버 이름** 및 **데이터베이스 ID** 데이터 열을 **개체 이름** 데이터 열과 함께 캡처해야 합니다.  
  
 **개체 ID** 데이터 열로 그룹화하도록 선택한 경우 **서버 이름** 및 **데이터베이스 ID** 데이터 열로 먼저 그룹화하고 **개체 ID** 데이터 열로 그룹화합니다. 마찬가지로 **인덱스 ID** 데이터 열로 그룹화하도록 선택한 경우 **서버 이름**, **데이터베이스 ID**및 **개체 ID** 데이터 열로 그룹화한 다음 **인덱스 ID** 데이터 열로 그룹화합니다. 개체 및 인덱스 ID가 서버와 데이터베이스 간에 그리고 인덱스 ID에 대한 개체 간에 고유하지 않기 때문에 이러한 순서로 그룹화해야 합니다.  
  
## <a name="finding-specific-events-within-a-trace"></a>추적에서 특정 이벤트 찾기  
 추적에서 이벤트를 찾아 그룹화하려면 다음 단계를 수행하십시오.  
  
1.  추적을 만듭니다.  
  
    -   추적을 정의할 때 캡처하려고 하는 다른 데이터 열과 함께 **Event Class**, **ClientProcessID**및 **Start Time** 데이터 열을 캡처하십시오. 자세한 내용은 [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)를 참조하세요.  
  
    -   캡처한 데이터를 **Event Class**데이터 열로 그룹화하고 추적을 파일이나 테이블에 캡처하십시오. 캡처된 데이터를 그룹화하려면 추적 속성 대화 상자의 **이벤트 선택** 탭에서 **열 구성** 을 클릭합니다. 자세한 내용은 [표시된 열 추적으로 구성&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)을 참조하세요.  
  
    -   추적을 시작한 다음 적절한 시간이 경과했거나 적절한 수의 이벤트가 캡처된 후에 중지합니다.  
  
2.  대상 이벤트를 찾습니다.  
  
    -   추적 파일이나 테이블을 열고 **Deadlock Chain**과 같은 원하는 이벤트 클래스의 노드를 확장하십시오. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)에서 제공되는 사전 정의된 튜닝 템플릿을 사용합니다.  
  
    -   확인할 이벤트를 찾을 때까지 추적 데이터를 검색합니다. **에서** 편집 **메뉴의** 찾기 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 명령을 사용하면 추적에서 값을 찾는데 도움이 됩니다. 추적하는 이벤트의 **ClientProcessID** 및 **Start Time** 데이터 열 값을 메모하십시오.  
  
3.  이벤트를 컨텍스트에 표시합니다.  
  
    -   추적 속성을 표시하고 **ClientProcessID**ClientProcessID **Event Class** 데이터 열과 함께 캡처해야 합니다.  
  
    -   보려고 하는 각 연결 ID의 노드를 확장하십시오. 추적을 수동으로 검색하거나 **에서** 를 사용하여 이전에 메모한 대상 이벤트의 **Start Time**값을 찾으십시오. 이벤트는 선택한 각 클라이언트 프로세스 ID에 속하는 다른 이벤트와 함께 시간 순서대로 표시됩니다. 예를 들어 추적에 캡처된 **Deadlock** 및 **Deadlock Chain**이벤트는 확장 클라이언트 프로세스 ID 내의 **SQL:BatchStarting**events within the exp및ed client process ID.  
  
 동일한 방법을 사용하여 그룹화된 이벤트를 찾을 수 있습니다. 찾던 이벤트를 발견하면 **ClientProcessID**, **ApplicationName**또는 다른 이벤트 클래스로 해당 이벤트를 그룹화하여 시간 순서대로 관련 작업을 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장된 추적 보기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)   
 [sys.fn_trace_getinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [필터 정보 보기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)   
 [필터 정보 보기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)   
 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
  
