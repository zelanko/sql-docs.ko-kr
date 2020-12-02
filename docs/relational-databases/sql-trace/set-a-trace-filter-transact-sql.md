---
description: 추적 필터 설정(Transact-SQL)
title: 추적 필터 설정(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 59c44a69bbe994ee7df7337213d26b4a789f5a11
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88455332"
---
# <a name="set-a-trace-filter-transact-sql"></a>추적 필터 설정(Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 추적 중인 이벤트에 필요한 정보만 검색하도록 필터를 만드는 데 저장 프로시저를 사용하는 방법에 대해 설명합니다.  
  
### <a name="to-set-a-trace-filter"></a>추적 필터를 설정하려면  
  
1.  추적이 이미 실행 중이면 `@status = 0`을 지정하고 **sp_trace_setstatus** 를 실행하여 추적을 중지합니다.  
  
2.  **sp_trace_setfilter** 를 실행하여 추적할 이벤트에서 검색할 정보 유형을 구성합니다.  

> [!IMPORTANT]  
>  일반적인 저장 프로시저와 달리 모든 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 저장 프로시저의 매개 변수(**sp_trace\__xx_**)는 정확하게 입력되어야 하며 데이터 형식 자동 변환을 지원하지 않습니다. 이러한 매개 변수가 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 인수 설명에서 지정한 대로 저장 프로시저는 오류를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [추적 필터링](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
