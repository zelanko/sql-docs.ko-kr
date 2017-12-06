---
title: "SQL Server 프로파일러 실행 | Microsoft Docs"
ms.custom: 
ms.date: 7/7/2017
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
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f9327a1cdb70be829701fa0710f5833545f8a0d2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="run-sql-server-profiler"></a>SQL Server Profiler 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]실행할 수 있습니다 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 여러 가지 방법으로 추적 수집을 지원 하기 위해 출력 다양 한 시나리오에서에서 합니다. 시작할 수 있습니다 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] Windows 10에서 **시작** 메뉴에서는 **도구** 메뉴 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 여러 위치에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
처음 시작 하면 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 선택 **새 추적** 에서 **파일** 메뉴, 표시 됩니다는 **서버에 연결** 지정할 수 있는 대화 상자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결할 인스턴스.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Windows 10 시작 메뉴에서 SQL Server Profiler를 시작 하려면  
-  Windows 클릭 **시작** 아이콘 또는 키를 눌러 Windows 키 및 "SQL Server Profiler 17"을 입력 하기 시작 합니다. 경우는 **SQL Server Profiler 17** 타일에는 다음이 표시 되 면 클릭 합니다.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자에서 SQL Server Profiler를 시작하려면  
-  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SQL Server Profiler를 시작 하려면  
 시작할 수 있습니다 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 여러 위치에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 때 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 시작 되 면 연결 컨텍스트, 추적 템플릿 및 시작 지점의 필터 컨텍스트가 로드 됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]각 SQL Server 프로파일러 세션을 자체 인스턴스에서 시작 되며 프로파일러를 종료 하는 경우 실행을 계속 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>도구 메뉴에서 SQL Server Profiler를 시작하려면  
-  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>쿼리 편집기에서 SQL Server Profiler를 시작하려면  
- 쿼리 편집기에서 마우스 오른쪽 단추를 클릭한 다음 **SQL Server Profiler에서 쿼리 추적**을 선택합니다.  

  > [!NOTE]  
  >  연결 컨텍스트는 편집기 연결이고, 추적 템플릿은 TSQL_SP이며, 적용된 필터는 SPID = 쿼리 창 SPID입니다.  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>작업 모니터에서 SQL Server Profiler를 시작하려면  
- 작업 모니터에서 클릭는 **프로세스** 창으로 프로 파일링 하 고 클릭 하려는 프로세스를 마우스 오른쪽 단추로 클릭 **SQL Server Profiler의 추적 프로세스**합니다.  

    > [!NOTE]  
    >  프로세스를 선택하면 작업 모니터가 열릴 당시의 개체 탐색기 연결이 연결 컨텍스트가 됩니다. 추적 템플릿은 서버 유형을 기반으로 하는 기본 템플릿이고 SPID가 선택한 프로세스의 SPID와 같게 됩니다.  
    
## <a name="net-framework-security"></a>.NET Framework 보안  
- Windows 인증 모드에서 사용자는 실행 되는 계정을 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 인스턴스에 연결할 수 있는 권한이 있어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
- [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 수행하려면 또한 ALTER TRACE 권한이 있어야 합니다.  

## <a name="next-steps"></a>다음 단계  
 [SQL Server Profiler 개요](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Management Studio 사용](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
