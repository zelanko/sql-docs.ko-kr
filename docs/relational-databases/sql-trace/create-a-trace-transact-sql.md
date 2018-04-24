---
title: 추적 만들기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], example
- traces [SQL Server], creating
ms.assetid: 79dd4254-e3c6-467a-bb6f-f99e51757e99
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 655bacebe7471bc6df99480850f1fc61c1a591d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-trace-transact-sql"></a>추적 만들기(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 저장 프로시저를 사용하여 추적을 만드는 방법에 대해 설명합니다.  
  
### <a name="to-create-a-trace"></a>추적 만들기  
  
1.  새 추적을 만드는 데 필요한 매개 변수를 사용하여 **sp_trace_create** 를 실행합니다. 새 추적은 중지된 상태(*status* = **0**)입니다.  
  
2.  추적할 이벤트 및 열을 선택하는 데 필요한 매개 변수를 실행하여 **sp_trace_setevent** 를 실행합니다.  
  
3.  또는 **sp_trace_setfilter** 를 실행하여 필터 또는 필터 조합을 설정합니다.  
  
     **sp_trace_setevent** 및 **sp_trace_setfilter** 는 중지된 기존 추적에서만 실행할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  일반적인 저장 프로시저와 달리 모든 SQL Server Profiler 저장 프로시저의 매개 변수(**sp_trace_*xx***)는 정확하게 입력해야 하며 데이터 형식 자동 변환을 지원하지 않습니다. 이러한 매개 변수를 인수 설명에 지정된 올바른 입력 매개 변수 데이터 형식으로 호출하지 않으면 저장 프로시저가 오류를 반환합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 추적을 만드는 방법을 보여 줍니다. 이 코드는 추적 만들기, 추적 파일 채우기 및 추적 중지의 세 가지 섹션으로 구성되어 있습니다. 추적하려는 이벤트를 추가하여 추적을 사용자 지정합니다. 이벤트 및 열 목록에 대한 자세한 내용은 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)을 사용하여 추적을 만드는 방법을 보여 줍니다.  
  
 다음 코드에서는 추적을 만들고 추적에 이벤트를 추가한 다음 추적을 시작합니다.  
  
```  
DECLARE @RC int, @TraceID int, @on BIT  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\SampleTrace'  
  
-- Select the return code to see if the trace creation was successful.  
SELECT RC = @RC, TraceID = @TraceID  
  
-- Set the events and data columns you need to capture.  
SELECT @on = 1  
  
-- 10 is RPC:Completed event. 1 is TextData column.   
EXEC sp_trace_setevent @TraceID, 10, 1, @on   
-- 13 is SQL:BatchStarting, 11 is LoginName  
EXEC sp_trace_setevent @TraceID, 13, 11, @on   
-- 13 is SQL:BatchStarting, 14 is StartTime  
EXEC sp_trace_setevent @TraceID, 13, 14, @on   
-- 12 is SQL:BatchCompleted, 15 is EndTime  
EXEC sp_trace_setevent @TraceID, 12, 15, @on   
-- 13 is SQL:BatchStarting, 1 is TextData  
EXEC sp_trace_setevent @TraceID, 13, 1, @on   
  
-- Set any filter. Not provided in this example  
--EXEC sp_trace_setfilter 1, 10, 0, 6, N'%Profiler%'  
  
-- Start Trace (status 1 = start)  
EXEC @RC = sp_trace_setstatus @TraceID, 1  
GO  
  
```  
  
## <a name="example"></a>예제  
 추적을 만들어 시작했으므로 이제 다음 코드를 실행하여 작업으로 추적을 채웁니다.  
  
```  
SELECT * FROM master.sys.databases  
GO  
SELECT * FROM ::fn_trace_getinfo(default)  
GO  
  
```  
  
## <a name="example"></a>예제  
 추적은 언제든지 중지 및 다시 시작할 수 있습니다. 이 예에서는 다음 코드를 실행하여 추적을 중지하고 추적을 닫고 추적 정의를 삭제합니다.  
  
```  
DECLARE @TraceID int  
-- Populate a variable with the trace_id of the current trace  
SELECT  @TraceID = TraceID FROM ::fn_trace_getinfo(default) WHERE VALUE = N'C:\SampleTrace.trc'  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2  
  
```  
  
## <a name="example"></a>예제  
 추적 파일을 검사하려면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 SampleTrace.trc 파일을 엽니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)   
 [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)  
  
  
