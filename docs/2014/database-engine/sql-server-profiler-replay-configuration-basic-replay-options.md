---
title: SQL Server Profiler 재생 구성 (기본 재생 옵션) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: 85a1dec6-9bbc-477a-86c5-b463db9ebb31
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ea9517047321f54734b3ccd8d072ba8f3f23152
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089714"
---
# <a name="sql-server-profiler---replay-configuration-basic-replay-options"></a>SQL Server 프로파일러 - 재생 구성(기본 재생 옵션)
  
  **재생 구성** 대화 상자에서 **기본 재생 옵션** 페이지를 사용하여 추적 파일 또는 테이블을 재생하는 방법을 지정할 수 있습니다.  
  
 이 창을 보려면 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]를 사용하여 재생에 적합한 이벤트가 포함된 추적 파일 또는 테이블을 엽니다. 자세한 내용은 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)을 참조하세요. 추적 파일이나 테이블을 연 상태에서 **재생** 메뉴의 **시작**을 클릭한 다음 추적을 재생할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
## <a name="options"></a>옵션  
 **서버 재생**  
 재생을 위해 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 표시합니다.  
  
 **변경 ...**  
 다른 서버에 연결하려면 **서버에 연결** 대화 상자를 시작합니다.  
  
 **파일에 저장**  
 재생 결과를 파일에 저장합니다. 
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 에서 위치를 지정하여 파일을 저장할 수 있는 표준 파일 대화 상자가 표시됩니다.  
  
 **테이블에 저장**  
 재생 결과를 테이블에 저장합니다. 
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 에서 위치를 지정하여 테이블을 저장할 수 있는 테이블 선택 대화 상자가 표시됩니다.  
  
 **재생 스레드 수**  
 동시에 사용할 재생 스레드 수를 지정합니다. 숫자가 높을수록 재생 중 소비되는 리소스가 늘어나지만 재생 속도가 빨라지고 동시성이 향상됩니다.  
  
 **추적한 순서대로 이벤트를 재생합니다.**  
 순차적으로 이벤트를 재생합니다. 디버깅을 위해 추적을 재생할 경우 이 옵션을 사용합니다.  
  
 **여러 스레드를 사용하여 이벤트를 재생합니다.**  
 동시에 이벤트를 재생합니다. 이 옵션을 사용하면 순차적으로 이벤트를 재생하는 것보다 속도가 빨라지지만 디버깅이 해제됩니다. 이벤트는 해당 SPID(시스템 프로세스 ID) 내에서 정렬됩니다.  
  
 **재생 결과 표시**  
 
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]에 재생 결과를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler &#40;추적 테이블 재생&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler &#40;추적 파일 재생&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [추적 재생](../tools/sql-server-profiler/replay-traces.md)  
  
  
