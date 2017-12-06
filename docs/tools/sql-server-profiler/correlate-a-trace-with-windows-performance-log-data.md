---
title: "추적과 Windows 성능 로그 데이터 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef4781a05da3e06bc1d098dacce544dd599d647b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Windows 성능 로그 데이터와 추적 상호 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용 하 여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], Microsoft Windows 성능 로그를 열고, 추적과, 카운터를 선택한 및 다음 선택한 성능 카운터를 추적과 함께 표시는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 그래픽 사용자 인터페이스입니다. 추적 창에서 이벤트를 선택하면 선택한 추적 이벤트와 상관 관계가 있는 성능 로그 데이터가 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 시스템 모니터 데이터 창에서 빨간 세로 막대로 표시됩니다.  
  
 추적과 성능 카운터의 상관 관계를 지정하려면 **StartTime** 및 **EndTime** 데이터 열을 포함하는 추적 파일이나 테이블을 연 다음 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**파일** 메뉴에서 **성능 데이터 가져오기**를 클릭합니다. 그러면 성능 로그를 열고 추적과의 상관 관계를 지정할 시스템 모니터 개체와 카운터를 선택할 수 있습니다.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>추적과 성능 로그 데이터의 상관 관계를 지정하려면  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에서 저장된 추적 파일 또는 추적 테이블을 엽니다. 계속 이벤트 데이터를 수집하고 있는 실행 중인 추적의 경우 상관 관계를 지정할 수 없습니다. 시스템 모니터 데이터와의 정확한 상관 관계를 위해 추적이 **StartTime** 과 **EndTime** 데이터 열을 모두 포함하도록 해야 합니다.  
  
2.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **파일** 메뉴에서 **성능 데이터 가져오기**를 클릭합니다.  
  
3.  **열기** 대화 상자에서 성능 로그가 들어 있는 파일을 선택합니다. 추적 데이터가 캡처되는 기간 동안 성능 로그 데이터 역시 캡처해야 합니다.  
  
4.  **성능 카운터 제한** 대화 상자에서 추적과 함께 표시하려는 시스템 모니터 개체와 카운터에 해당하는 확인란을 선택합니다. **확인.**  
  
5.  추적 이벤트 창에서 이벤트를 선택하거나 화살표 키를 사용하여 추적 이벤트 창의 인접 행으로 이동합니다. **시스템 모니터 데이터** 창의 빨강 세로 막대는 선택한 추적 이벤트와 상관 관계에 있는 성능 로그 데이터를 나타냅니다.  
  
6.  시스템 모니터 그래프에서 자세히 보고 싶은 시점을 클릭합니다. 선택한 시간에 가장 가까운 해당 추적 행이 선택됩니다. 시간 범위를 확대하려면 시스템 모니터 그래프에서 마우스 포인터를 누른 다음 끌어서 범위를 선택합니다.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>다른 버전의 Windows와 공유할 수 있는 성능 로그를 만들려면  
  
1.  제어판에서 **관리 도구**를 연 다음 **성능**을 두 번 클릭합니다.  
  
2.  **성능** 대화 상자에서 **성능 로그 및 경고**를 확장하고 **카운터 로그**를 마우스 오른쪽 단추로 클릭한 다음 **새 로그 설정**을 클릭합니다.  
  
3.  카운터 로그의 이름을 입력한 다음 **확인**을 클릭합니다.  
  
4.  **일반** 탭에서 **카운터 추가**를 클릭합니다.  
  
5.  **성능 개체** 목록에서 모니터링하려는 성능 개체를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능 개체의 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 시작하고 명명된 인스턴스는 MSSQL$*instanceName*으로 시작합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 기타 중요한 값(예: 프로세서 시간, 디스크 시간)에 대해 필요한 만큼의 카운터를 추가합니다.  
  
7.  카운터 추가가 완료되면 **닫기**를 클릭합니다.  
  
8.  **데이터 샘플 간격** 값을 설정합니다. 샘플링 간격은 가장 적절한 간격(예를 들어 5분)에서 시작하여 필요에 따라 간격을 조정합니다.  
  
9. **로그 파일** 탭의 **로그 파일 종류** 목록에서 **텍스트 파일(쉼표 구분 형식)** 을 선택합니다. 쉼표로 구분된 텍스트 로그 파일은 다른 버전의 Windows와 공유할 수 있으며 나중에 Microsoft Excel과 같은 보고서 도구에서 볼 수 있습니다.  
  
10. **일정** 탭에서 모니터링 일정을 지정합니다.  
  
11. **확인** 을 클릭하여 성능 로그를 만듭니다.  
