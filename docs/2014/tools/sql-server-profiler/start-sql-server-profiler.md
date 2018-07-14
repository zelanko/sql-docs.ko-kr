---
title: SQL Server Profiler를 시작 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5b752dfc31fd83530a773370551b88589fc2f4b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246143"
---
# <a name="start-sql-server-profiler"></a>SQL Server Profiler 시작
  다양한 시나리오에서 추적 출력 수집을 지원하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 여러 다른 방법으로 시작할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 **시작** 메뉴, **튜닝 관리자의** 도구 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 메뉴 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 여러 위치에서 시작할 수 있습니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 처음 시작하고 **파일** 메뉴에서 **새 추적** 을 선택하면 연결할 **인스턴스를 지정할 수 있는** 서버에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대화 상자가 표시됩니다.  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>시작 메뉴에서 SQL Server Profiler를 시작하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **성능 도구**를 차례로 가리킨 다음 **SQL Server Profiler**를 클릭합니다.  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자에서 SQL Server Profiler를 시작하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>Management Studio에서 SQL Server Profiler 시작  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 각 프로파일러 세션을 자체 인스턴스에서 시작하므로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 중지해도 이러한 프로파일러 세션은 계속 실행됩니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 다음 절차에서처럼 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 여러 위치에서 시작할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 시작하면 시작 지점의 연결 컨텍스트, 추적 템플릿 및 필터 컨텍스트가 로드됩니다.  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>도구 메뉴에서 SQL Server Profiler를 시작하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>쿼리 편집기에서 SQL Server Profiler를 시작하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 메뉴에서 **새 쿼리**를 클릭합니다.  
  
2.  쿼리 편집기에서 마우스 오른쪽 단추를 클릭한 다음 **SQL Server Profiler에서 쿼리 추적**을 선택합니다.  
  
    > [!NOTE]  
    >  연결 컨텍스트는 편집기 연결이고, 추적 템플릿은 TSQL_SP이며, 적용된 필터는 SPID = 쿼리 창 SPID입니다.  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>작업 모니터에서 SQL Server Profiler를 시작하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **작업 모니터**를 클릭합니다.  
  
2.  **프로세스** 창을 클릭하고 프로파일링할 프로세스를 마우스 오른쪽 단추로 클릭한 다음 **SQL Server Profiler의 추적 프로세스**를 클릭합니다.  
  
    > [!NOTE]  
    >  프로세스를 선택하면 작업 모니터가 열릴 당시의 개체 탐색기 연결이 연결 컨텍스트가 됩니다. 추적 템플릿은 서버 유형을 기반으로 하는 기본 템플릿이고 SPID가 선택한 프로세스의 SPID와 같게 됩니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 Windows 인증 모드를 사용하여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 실행하는 사용자 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 수 있는 사용 권한이 있어야 합니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 수행하려면 또한 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 프로파일러](sql-server-profiler.md)   
 [SQL Server Management Studio 사용](../../database-engine/use-sql-server-management-studio.md)  
  
  
