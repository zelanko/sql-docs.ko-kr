---
title: 추적 필터 설정(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6e3ecc4b125d226fc2cdf6dbe241e0ce017eae6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245934"
---
# <a name="set-a-trace-filter-transact-sql"></a>추적 필터 설정(Transact-SQL)
  이 항목에서는 추적 중인 이벤트에 필요한 정보만 검색하도록 필터를 만드는 데 저장 프로시저를 사용하는 방법에 대해 설명합니다.  
  
### <a name="to-set-a-trace-filter"></a>추적 필터를 설정하려면  
  
1.  추적이 이미 실행 중이면 **@status = 0**을 지정하고 **sp_trace_setstatus**를 실행하여 추적을 중지합니다.  
  
2.  **sp_trace_setfilter** 를 실행하여 추적할 이벤트에서 검색할 정보 유형을 구성합니다.  
  
> [!IMPORTANT]
>  일반적인 저장 프로시저와 달리 모든 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 저장 프로시저의 매개 변수(<strong>sp_trace_*xx*</strong>)는 정확하게 입력해야 하며 데이터 형식 자동 변환을 지원하지 않습니다. 이러한 매개 변수가 인수 설명에서 지정한대로 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 저장 프로시저는 오류를 반환합니다.  
  
## <a name="see-also"></a>관련 항목  
 [추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
