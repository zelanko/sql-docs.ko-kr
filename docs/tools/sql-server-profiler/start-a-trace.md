---
title: 추적 시작
titleSuffix: SQL Server Profiler
description: SQL Server Profiler에서 새 추적을 정의하거나 템플릿을 만든 후 추적을 시작하고 해당 데이터를 찾는 방법에 대해 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 261c18ff809bd8a6fb1a7960c753c6fd64bbc462
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753675"
---
# <a name="start-a-trace"></a>추적 시작

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 새 추적을 정의하거나 템플릿을 만든 후 새 추적 정의 또는 템플릿을 사용하여 데이터 캡처를 시작, 일시 중지 또는 중지할 수 있습니다.  
  
## <a name="starting-a-trace"></a>추적 시작

추적을 시작하고 정의된 원본이 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 캡처된 서버 이벤트의 임시 보유 장소를 제공하는 큐를 만듭니다.  
  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 SQL 추적에 액세스하는 경우 추적이 시작되면 새 추적 창이 열리면서(창이 열려 있지 않은 경우) 데이터가 즉시 캡처됩니다.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저를 사용하여 SQL 추적에 액세스하는 경우에는 데이터 캡처를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때마다 추적을 시작해야 합니다. 추적이 시작되면 추적 이름만 수정할 수 있습니다.  
  
> [!NOTE]  
>  기존의 추적으로 작업하면 속성을 볼 수는 있지만 수정할 수는 없습니다. 속성을 수정하려면 추적을 시작하거나 일시 중지하십시오.  
  
## <a name="see-also"></a>참고 항목

[서버 연결 후 자동으로 추적 시작&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   

[추적 일시 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   

[추적 중지&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   

[추적 창 지우기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   

[일시 중지 또는 중지 후 추적 실행&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)