---
title: SQL Server Profiler-도구-옵션 (일반 옵션 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9da36f49927acd2a313bcb9f8647655731006d2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089616"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler - Tools-Options (General Options Page)
  **일반 옵션** 대화 상자를 사용하여 다음 옵션을 확인하거나 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
  
### <a name="display-options"></a>표시 옵션  
 **글꼴 이름**  
 추적하는 동안 추적 결과 표에 사용되는 글꼴 이름을 표시합니다.  
  
 **글꼴 크기**  
 추적하는 동안 추적 결과 표에 사용되는 글꼴 크기를 표시합니다.  
  
 **글꼴 선택**  
 글꼴 설정을 변경할 수 있는 대화 상자를 엽니다.  
  
 **날짜 및 시간 값 표시에 국가별 설정 사용**  
 컴퓨터에 구성된 국가별 설정에 따라 날짜 및 시간 값을 표시합니다. 이 옵션을 선택하지 않으면 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용하는 밀리초 단위까지 포함된 고정 형식으로 날짜 및 시간이 표시됩니다.  
  
> [!NOTE]  
>  이 확인란을 선택/선택 해제하면 **StartTime** 및 **EndTime**과 같은 시간 열 표시 형식이 변경됩니다. 하지만 언어 이벤트 또는 원격 프로시저 호출(RPC) 내의 **DateTime** 값 매개 변수는 변경되지 않습니다.  
  
 **기간 열에 마이크로초 단위로 값 표시**  
 추적에 대한 **기간** 데이터 열의 값을 마이크로초 단위로 표시합니다. 기본적으로 **기간** 열의 값은 밀리초 단위로 표시됩니다.  
  
### <a name="tracing-options"></a>추적 옵션  
 **연결한 후 즉시 추적 시작**  
 연결되면 기본 템플릿을 사용하여 즉시 추적을 시작합니다.  
  
 **공급자 버전 변경 시 추적 정의 업데이트**  
 공급자가 업데이트된 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 최신 추적 정의를 적용합니다. 이 옵션은 기본적으로 선택되지 않습니다. 이 옵션을 선택하면 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]가 서버에서 추적 정의를 쿼리하여 정의가 있으면 디스크에 파일을 다시 만듭니다.  
  
### <a name="file-rollover-options"></a>파일 롤오버 옵션  
 **확인하지 않고 모든 롤오버 파일을 순서대로 로드**  
 추적 파일이 열리면 롤오버 파일을 자동으로 로드합니다. 이 옵션을 선택하면 추적하는 동안 두 개 이상의 파일이 생성된 경우 자동으로 모든 롤오버 파일이 로드됩니다.  
  
 **롤오버 파일 로드 전에 확인**  
 추적 파일을 열면 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 가 롤오버 파일을 추가하기 전에 사용자에게 확인 메시지를 표시합니다.  
  
 **다음 롤오버 파일 로드 안 함**  
 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 에서 다음 롤오버 파일을 로드하지 않습니다.  
  
### <a name="replay-options"></a>재생 옵션  
 **기본 재생 스레드 수**  
 동시에 사용할 재생 스레드 수를 지정합니다. 이 값을 높게 설정할수록 재생하는 동안 리소스가 더 많이 사용되지만 재생 동시성은 향상됩니다.  
  
 **기본 상태 모니터 대기 간격(초)**  
 재생하기 전에 대기하는 간격(초)을 지정합니다. 기본값은 3600초(1시간)입니다. 이 설정은 상태 모니터에서 스레드를 종료하기 전까지 스레드가 실행되는 시간을 결정합니다.  
  
 **기본 상태 모니터 폴링 간격(초)**  
 재생 중 상태 모니터 폴링 간격(초)을 지정합니다. 기본값은 60초입니다. 이 값을 사용하면 상태 모니터에서 종료 후보에 대해 폴링하는 주기를 구성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [서버 연결 후 자동으로 추적 시작&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [추적 표시 기본값 설정&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [추적 테이블 재생&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [추적 파일 재생&#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [추적 재생](../tools/sql-server-profiler/replay-traces.md)   
 [전역 추적 옵션 설정 &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [SQL Server Profiler 템플릿 및 권한](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 프로파일러](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
