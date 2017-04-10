---
title: "저장된 추적 보기(Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "추적 [SQL Server], 보기"
  - "추적 표시"
  - "추적 보기"
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# 저장된 추적 보기(Transact-SQL)
  이 항목에서는 기본 제공 함수를 사용하여 저장된 추적을 보는 방법에 대해 설명합니다.  
  
### 특정 추적을 보려면  
  
1.  필요한 정보에 대한 추적 ID를 지정하여 **fn_trace_getinfo**를 실행합니다. 이 함수는 추적, 추적 속성, 속성 정보가 들어 있는 테이블을 반환합니다.  
  
     다음과 같이 이 함수를 호출하십시오.  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### 기존 추적을 모두 보려면  
  
1.  `0`이나 `default`를 지정하여 **fn_trace_getinfo**를 실행합니다. 이 함수는 모든 추적, 추적 속성, 속성 정보가 들어 있는 테이블을 반환합니다.  
  
     다음과 같이 함수를 호출하십시오.  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## .NET Framework 보안  
 기본 제공 함수 **fn_trace_getinfo**를 실행하려면 사용자에게 다음과 같은 사용 권한이 있어야 합니다.  
  
 서버에 대한 ALTER TRACE  
  
## 참고 항목  
 [sys.fn_trace_getinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL Server Profiler를 사용하여 추적 보기 및 분석](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  