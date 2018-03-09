---
title: "재생 (SQL Server Profiler) 커서에 | Microsoft Docs"
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
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
caps.latest.revision: "22"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 723d3a47736b44dba88a50a2d24ed862c1f30507
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>커서까지 재생(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용 하 여 커서에 도달할 때 일시 중지 된 추적 파일이 나 테이블을 재생 하는 방법에 설명 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]합니다. 커서에서 추적을 일시 중지하면 긴 추적 스크립트 재생을 증분 분석이 가능한 짧은 세그먼트로 나눌 수 있기 때문에 디버깅할 수 있습니다.  
  
### <a name="to-replay-to-the-cursor"></a>커서까지 재생하려면  
  
1.  재생할 추적 파일이나 추적 테이블을 엽니다. 자세한 내용은 [추적 파일 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) 또는 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)를 참조하세요.  
  
     열려는 추적 파일이나 추적 테이블에 재생에 필요한 이벤트 클래스가 포함되어 있는지 확인합니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을 참조하세요.  
  
2.  추적 창에서 이벤트를 클릭합니다.  
  
3.  **재생** 메뉴에서 **커서까지 실행**을 클릭한 다음 추적을 재생할 서버에 연결합니다.  
  
4.  **재생 구성** 대화 상자에서 설정을 확인한 다음 **확인**을 클릭합니다.  
  
     재생이 시작되며 첫 번째 커서에서 일시 중지됩니다.  
  
5.  추적을 다시 시작하려면 F5 키를 누릅니다.  
  
6.  추적이 끝날 때까지 5단계를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중단점 &#40;까지 재생 SQL Server Profiler &#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)   
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
