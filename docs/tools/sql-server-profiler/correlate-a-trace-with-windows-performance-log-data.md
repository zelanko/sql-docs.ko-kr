---
title: "Windows 성능 로그 데이터와 추적의 상관 관계 지정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "로그 데이터와의 추적의 상관 관계"
  - "로그 [SQL Server], 추적"
  - "프로파일러 [SQL Server 프로파일러], 로그 데이터와의 추적의 상관 관계"
  - "추적 [SQL Server], 로그"
  - "SQL Server 프로파일러, 로그 데이터와의 추적의 상관 관계"
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Windows 성능 로그 데이터와 추적의 상관 관계 지정
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 Microsoft Windows 성능 로그를 열고 추적과의 상관 관계를 지정할 카운터를 선택한 다음 선택한 성능 카운터를 추적과 함께 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 그래픽 사용자 인터페이스에 표시할 수 있습니다. 추적 창에서 이벤트를 선택하면 선택한 추적 이벤트와 상관 관계가 있는 성능 로그 데이터가 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]의 시스템 모니터 데이터 창에서 빨간 세로 막대로 표시됩니다.  
  
 추적과 성능 카운터의 상관 관계를 지정하려면 **StartTime** 및 **EndTime** 데이터 열을 포함하는 추적 파일이나 테이블을 연 다음 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **파일** 메뉴에서 **성능 데이터 가져오기**를 클릭합니다. 그러면 성능 로그를 열고 추적과의 상관 관계를 지정할 시스템 모니터 개체와 카운터를 선택할 수 있습니다.  
  
## 참고 항목  
 [추적과 Windows 성능 로그 데이터의 상관 관계 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  