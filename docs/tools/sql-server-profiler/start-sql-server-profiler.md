---
title: SQL Server Profiler 실행
titleSuffix: SQL Server Profiler
description: SQL Server Profiler를 시작할 수 있는 프로그램과 메뉴 및 추적 출력에 사용되는 연결 컨텍스트, 템플릿, 필터에 대해 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 07/07/2017
ms.openlocfilehash: 7bfe84350449d1de600699c7bb73348bf5a1b069
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151669"
---
# <a name="run-sql-server-profiler"></a>SQL Server Profiler 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

다양한 시나리오에서 추적 출력 수집을 지원하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 여러 가지 방법으로 실행할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]는 Windows 10 **시작** 메뉴, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 여러 위치에서 시작할 수 있습니다.  
  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 처음 시작하고 **파일** 메뉴에서 **새 추적**을 선택하면 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정할 수 있는 **서버에 연결** 대화 상자가 표시됩니다.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Windows 10 시작 메뉴에서 SQL Server Profiler를 시작하려면  
-  Windows **시작** 아이콘을 클릭하거나 Windows 키를 누른 다음 "SQL Server Profiler 17"을 입력합니다. **SQL Server Profiler 17** 타일이 표시되면 클릭합니다.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자에서 SQL Server Profiler를 시작하려면  
-  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자의 **도구** 메뉴에서 **SQL Server Profiler**를 클릭합니다.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SQL Server Profiler를 시작하려면  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 여러 위치에서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 시작할 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 시작하면 시작 지점의 연결 컨텍스트, 추적 템플릿 및 필터 컨텍스트가 로드됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 각 SQL Server Profiler 세션을 자체 인스턴스에서 시작하므로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 중지해도 이러한 Profiler는 계속 실행됩니다.  
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
