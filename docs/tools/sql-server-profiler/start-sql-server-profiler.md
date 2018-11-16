---
title: SQL Server Profiler 실행 | Microsoft Docs
ms.custom: ''
ms.date: 7/7/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 303f97e5a2fb4599bde5c17fee056a3572491ad0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655975"
---
# <a name="run-sql-server-profiler"></a>SQL Server Profiler 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  다양한 시나리오에서 추적 출력 수집을 지원하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 여러 가지 방법으로 실행할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 Windows 10 **시작** 메뉴, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 여러 위치에서 시작할 수 있습니다.  
  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 처음 시작하고 **파일** 메뉴에서 **새 추적**을 선택하면 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정할 수 있는 **서버에 연결** 대화 상자가 표시됩니다.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Windows 10 시작 메뉴에서 SQL Server Profiler를 시작하려면  
-  Windows를 클릭 **시작** 아이콘 또는 키를 눌러는 Windows 키를 "SQL Server Profiler 17"을 입력 하기 시작 합니다. 경우는 **SQL Server Profiler 17** 타일에는 다음이 표시 되 면 클릭 합니다.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자에서 SQL Server Profiler를 시작하려면  
-  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SQL Server Profiler를 시작 하려면  
 시작할 수 있습니다 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 여러 위치에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 시작하면 시작 지점의 연결 컨텍스트, 추적 템플릿 및 필터 컨텍스트가 로드됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 각 SQL Server Profiler 세션 자체 인스턴스를 시작 및 종료 하는 경우 실행을 계속 Profiler [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>도구 메뉴에서 SQL Server Profiler를 시작하려면  
-  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>쿼리 편집기에서 SQL Server Profiler를 시작하려면  
- 쿼리 편집기에서 마우스 오른쪽 단추를 클릭한 다음 **SQL Server Profiler에서 쿼리 추적**을 선택합니다.  

  > [!NOTE]  
  >  연결 컨텍스트는 편집기 연결이고, 추적 템플릿은 TSQL_SP이며, 적용된 필터는 SPID = 쿼리 창 SPID입니다.  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>작업 모니터에서 SQL Server Profiler를 시작하려면  
- 작업 모니터에서 **프로세스** 창을 클릭하고 프로파일링할 프로세스를 마우스 오른쪽 단추로 클릭한 다음, **SQL Server Profiler의 추적 프로세스**를 클릭합니다.  

    > [!NOTE]  
    >  프로세스를 선택하면 작업 모니터가 열릴 당시의 개체 탐색기 연결이 연결 컨텍스트가 됩니다. 추적 템플릿은 서버 유형을 기반으로 하는 기본 템플릿이고 SPID가 선택한 프로세스의 SPID와 같게 됩니다.  
    
## <a name="net-framework-security"></a>.NET Framework 보안  
- Windows 인증 모드를 사용하여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 실행하는 사용자 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는 권한이 있어야 합니다.  
- [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 추적을 수행하려면 또한 ALTER TRACE 권한이 있어야 합니다.  

## <a name="next-steps"></a>다음 단계  
 [SQL Server Profiler 개요](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Management Studio 사용](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
