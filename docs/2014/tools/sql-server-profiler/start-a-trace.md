---
title: 추적 시작 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, stopping traces
- pausing traces
- Profiler [SQL Server Profiler], stopping traces
- Profiler [SQL Server Profiler], starting traces
- traces [SQL Server], starting
- SQL Server Profiler, pausing traces
- traces [SQL Server], stopping
- Profiler [SQL Server Profiler], pausing traces
- traces [SQL Server], pausing
- SQL Server Profiler, starting traces
- stopping traces
- starting traces
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b32b1d1d6416c6a8c6097a79dcba18eb62a89d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140260"
---
# <a name="start-a-trace"></a>추적 시작
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 새 추적을 정의하거나 템플릿을 만든 후 새 추적 정의 또는 템플릿을 사용하여 데이터 캡처를 시작, 일시 중지 또는 중지할 수 있습니다.  
  
## <a name="starting-a-trace"></a>추적 시작  
 추적을 시작하고 정의된 원본이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 캡처된 서버 이벤트의 임시 보유 장소를 제공하는 큐를 만듭니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 SQL 추적에 액세스하는 경우 추적이 시작되면 새 추적 창이 열리면서(창이 열려 있지 않은 경우) 데이터가 즉시 캡처됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용하여 SQL 추적에 액세스하는 경우에는 데이터 캡처를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때마다 추적을 시작해야 합니다. 추적이 시작되면 추적 이름만 수정할 수 있습니다.  
  
> [!NOTE]  
>  기존의 추적으로 작업하면 속성을 볼 수는 있지만 수정할 수는 없습니다. 속성을 수정하려면 추적을 시작하거나 일시 중지하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [서버 연결 후 자동으로 추적 시작 &#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [추적 일시 중지&#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)   
 [추적 중지&#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)   
 [추적 창 지우기&#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)   
 [일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
