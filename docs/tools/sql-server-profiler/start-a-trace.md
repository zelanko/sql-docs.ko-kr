---
title: "추적을 시작 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
caps.latest.revision: "24"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef0d4c1015fa70145f8539a4dd10f4f8f6ffc35b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="start-a-trace"></a>추적 시작
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]새 추적을 정의 하거나 템플릿을 사용 하 여 만든 후 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], 시작, 일시 중지 하거나 새 추적 정의 또는 템플릿을 사용 하 여 데이터 캡처를 중지할 수 있습니다.  
  
## <a name="starting-a-trace"></a>추적 시작  
 추적을 시작하고 정의된 원본이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 캡처된 서버 이벤트의 임시 보유 장소를 제공하는 큐를 만듭니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 SQL 추적에 액세스하는 경우 추적이 시작되면 새 추적 창이 열리면서(창이 열려 있지 않은 경우) 데이터가 즉시 캡처됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용하여 SQL 추적에 액세스하는 경우에는 데이터 캡처를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때마다 추적을 시작해야 합니다. 추적이 시작되면 추적 이름만 수정할 수 있습니다.  
  
> [!NOTE]  
>  기존의 추적으로 작업하면 속성을 볼 수는 있지만 수정할 수는 없습니다. 속성을 수정하려면 추적을 시작하거나 일시 중지하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [서버 &#40; 연결 후 자동으로 추적 시작 SQL Server Profiler &#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [추적 &#40; 일시 중지 SQL Server Profiler &#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   
 [추적 &#40; 중지 SQL Server Profiler &#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   
 [추적 창 &#40;의 선택을 취소합니다 SQL Server Profiler &#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   
 [일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
