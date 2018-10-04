---
title: SQL Server Profiler-재생 구성 (고급 재생 옵션) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.advanced.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: b4eb34f7-3af6-4a44-ba7e-2b8430ec3cd7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fff89f4be7953e2eb0cec3ed9a04883052ed6d1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192483"
---
# <a name="sql-server-profiler---replay-configuration-advanced-replay-options"></a>SQL Server 프로파일러 - 재생 구성(고급 재생 옵션)
  **재생 구성** 대화 상자에서 **고급 재생 옵션** 탭을 사용하여 추적 파일 재생 방법을 지정할 수 있습니다.  
  
 이 창을 보려면 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]를 사용하여 재생에 적합한 이벤트가 포함된 추적 파일 또는 테이블을 엽니다. 자세한 내용은 [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md)을 참조하세요. 추적 파일 또는 테이블이 열려 있는 상태로 **재생** 메뉴에서 **시작**을 클릭하고 추적을 재생할 SQL Server의 인스턴스에 연결한 다음 **고급 재생 옵션** 탭을 클릭합니다.  
  
## <a name="options"></a>변수  
 **시스템 SPID 재생**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]에서 SPID(시스템 프로세스 식별자)를 재생할지 여부를 지정합니다.  
  
 **한 SPID만 재생**  
 선택한 SPID와 관련된 원본 추적 파일의 작업만 재생합니다.  
  
 **재생할 SPID**  
 재생할 SPID를 지정합니다.  
  
 **날짜 및 시간별 재생 제한**  
 원본 추적 파일의 일부만 재생하려면 이 옵션을 선택합니다.  
  
 **시작 시간**  
 원본 추적 파일에 지정되어 있는 재생 시작 날짜 및 시간입니다.  
  
 **종료 시간**  
 원본 추적 파일에 지정되어 있는 재생 중지 날짜 및 시간입니다.  
  
 **상태 모니터 대기 간격(초)**  
 재생하기 전에 대기하는 간격(초)을 지정합니다. 기본값은 3600초(1시간)입니다. 이 설정은 상태 모니터에서 프로세스를 종료하기 전의 프로세스 실행 시간에 영향을 줍니다.  
  
 **상태 모니터 폴링 간격(초)**  
 재생 중 상태 모니터 폴링 간격(초)을 지정합니다. 기본값은 60초입니다. 이 값을 사용하면 상태 모니터에서 종료 후보에 대해 폴링하는 주기를 구성할 수 있습니다.  
  
 **SQL Server 차단된 프로세스 모니터 설정**  
 차단된 프로세스 또는 차단 프로세스를 검색하는 프로세스를 설정합니다.  
  
 **차단된 프로세스 모니터 대기 간격(초)**  
 차단된 프로세스 모니터에서 차단된 프로세스 또는 차단 프로세스를 검색하는 간격을 구성합니다.  
  
## <a name="see-also"></a>관련 항목  
 [추적 테이블 재생 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [추적 파일 재생&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [추적 재생](../tools/sql-server-profiler/replay-traces.md)  
  
  
