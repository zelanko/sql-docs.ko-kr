---
title: "재생 (SQL Server Profiler) 중단점을 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
caps.latest.revision: "25"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2383eb3a226beb02c7a2060af5f07b8f97011dcd
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>중단점까지 재생(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]이 항목에서는 추적 파일이 나 테이블을 사용 하 여 재생에 중단점을 설정 하는 방법을 설명 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]합니다. 추적 재생을 시작하기 전에 추적 파일이나 테이블에 중단점을 설정하면 특정 이벤트에서 추적 재생을 일시 중지할 수 있습니다. 추적을 재생하는 동안 중단점을 사용하면 긴 추적 스크립트 재생을 증분 방식으로 분석할 수 있는 짧은 세그먼트로 나눌 수 있으므로 디버깅이 지원됩니다.  
  
### <a name="to-replay-to-a-breakpoint"></a>중단점까지 재생하려면  
  
1.  재생할 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)를 참조하세요.  
  
     열려는 추적 파일이나 추적 테이블에 재생에 필요한 이벤트 클래스가 포함되어 있는지 확인합니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을(를) 참조하세요.  
  
2.  추적 창에서 중단점으로 사용할 이벤트를 클릭합니다. 다음 세 가지 방법 중 하나를 사용하여 중단점을 설정합니다.  
  
    -   F9 키를 누릅니다.  
  
    -   **재생** 메뉴에서 **중단점 설정/해제**를 클릭합니다.  
  
    -   이벤트를 마우스 오른쪽 단추로 클릭한 다음 **중단점 설정/해제**를 클릭합니다.  
  
     선택한 추적 이벤트 옆에 빨간색 글머리 기호가 나타나 이 이벤트가 추적 중단점임을 나타냅니다.  
  
     중단점을 여러 개 설정하려면 이 단계를 반복합니다.  
  
3.  **재생** 메뉴에서 **시작**을 클릭하고 추적을 재생하려는 서버에 연결합니다.  
  
4.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다.  
  
     재생이 시작되고 중단점에 도달하면 재생이 일시 중지됩니다.  
  
5.  F5 키를 눌러 재생을 재개하고 다음 중단점으로 진행합니다.  
  
6.  추적이 끝날 때까지 5단계를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [커서 &#40;까지 재생 SQL Server Profiler &#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)   
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
