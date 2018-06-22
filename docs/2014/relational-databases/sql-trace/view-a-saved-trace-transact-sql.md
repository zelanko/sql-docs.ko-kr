---
title: 저장된 추적 보기(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f417eb54eff29631f4a24ebbf48de40937a50c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081518"
---
# <a name="view-a-saved-trace-transact-sql"></a>저장된 추적 보기(Transact-SQL)
  이 항목에서는 기본 제공 함수를 사용하여 저장된 추적을 보는 방법에 대해 설명합니다.  
  
### <a name="to-view-a-specific-trace"></a>특정 추적을 보려면  
  
1.  필요한 정보에 대한 추적 ID를 지정하여 **fn_trace_getinfo** 를 실행합니다. 이 함수는 추적, 추적 속성, 속성 정보가 들어 있는 테이블을 반환합니다.  
  
     다음과 같이 이 함수를 호출하십시오.  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>기존 추적을 모두 보려면  
  
1.  **이나** 를 지정하여 `0` fn_trace_getinfo `default`를 실행합니다. 이 함수는 모든 추적, 추적 속성, 속성 정보가 들어 있는 테이블을 반환합니다.  
  
     다음과 같이 함수를 호출하십시오.  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 기본 제공 함수 **fn_trace_getinfo**를 실행하려면 사용자에게 다음과 같은 사용 권한이 있어야 합니다.  
  
 서버에 대한 ALTER TRACE  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_trace_getinfo&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
