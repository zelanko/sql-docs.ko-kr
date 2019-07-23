---
title: 추적 테이블 재생 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c35935e7b63faa44c3af1bbe21adb90a7f837883
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031456"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>추적 테이블 재생(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  재생은 저장된 추적을 열고 나중에 재생하는 기능입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 사용자 연결 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 시뮬레이션할 수 있는 다중 스레드 재생 엔진을 갖추고 있습니다. 재생 기능은 애플리케이션이나 프로세스 문제 해결에 유용합니다. 문제를 파악하여 수정할 때 수정된 애플리케이션이나 프로세스에 대해 잠재적인 문제를 발견한 추적을 실행합니다. 원래 추적을 재생한 다음 결과를 비교합니다.  
  
 모니터링하려는 다른 이벤트 클래스 외에도 재생 기능을 사용하려면 특정 이벤트 클래스를 캡처해야 합니다. **TSQL_Replay** 추적 템플릿을 사용할 경우 이러한 이벤트는 기본적으로 캡처됩니다. 자세한 내용은 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)을 참조하세요.  
  
### <a name="to-replay-a-trace-table"></a>추적 테이블을 재생하려면  
  
1.  재생에 필요한 이벤트 클래스가 들어 있는 추적 테이블을 엽니다.  
  
2.  **재생** 메뉴에서 **시작**을 클릭하고 추적을 재생하려는 서버 인스턴스에 연결합니다.  
  
3.  **재생 구성** 대화 상자의 **기본 재생 옵션** 탭에서 **서버 재생**을 지정합니다. **서버 재생** 상자에 표시된 서버를 변경하려면 **변경** 을 클릭합니다.  
  
4.  또는 재생을 저장할 대상으로 다음 중 하나를 선택합니다.  
  
    -   **파일에 저장,** 재생이 저장될 파일을 지정합니다.  
  
    -   **테이블에 저장**- 재생이 저장될 데이터베이스를 지정합니다.  
  
5.  **추적한 순서대로 이벤트를 재생합니다.** 또는 **여러 스레드를 사용하여 이벤트를 재생합니다.** 를 선택합니다. 다음 표에서는 이 두 설정 사이의 차이점을 설명합니다.  
  
    |옵션|설명|  
    |------------|-----------------|  
    |**추적한 순서대로 이벤트를 재생합니다.**|기록된 순서대로 이벤트를 재생합니다. 이 옵션을 사용하면 디버깅할 수 있습니다.|  
    |**여러 스레드를 사용하여 이벤트를 재생합니다.**|이 옵션은 여러 스레드를 사용하여 순서와 관계없이 각 이벤트를 재생합니다. 이 옵션을 사용하면 성능이 최적화됩니다.|  
  
6.  수행되는 재생을 확인하려면 **재생 결과 표시** 를 선택합니다.  
  
7.  필요에 따라 **고급 재생 옵션**탭을 클릭하여 다음 옵션을 지정합니다.  
  
    -   모든 SPID(서버 프로세스 ID)를 재생하려면 **시스템 SPID 재생**을 선택합니다.  
  
    -   재생을 특정 SPID에 속하는 프로세스로 제한하려면 **한 SPID만 재생**을 선택합니다. **재생할 SPID**입력란에 SPID를 입력합니다.  
  
    -   특정 시간 동안 발생된 이벤트를 재생하려면 **날짜 및 시간별 재생 제한**을 선택합니다. **시작 시간**및 **종료 시간**에 날짜와 시간을 선택하여 재생에 포함될 기간을 지정합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 재생 중 프로세스를 관리하는 방법을 제어하려면 **상태 모니터 옵션**을 구성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로파일러 실행에 필요한 권한](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [추적 재생](../../tools/sql-server-profiler/replay-traces.md)   
 [추적 테이블 열기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
