---
title: 데이터베이스 엔진 튜닝 관리자 시작 및 사용 | Microsoft 문서
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.dta.workload.f1
- sql13.dta.general.f1
- sql13.dta.advancedtuningoptions.f1
- sql13.dta.tuningoptions.f1
- sql13.dta.progress.f1
- sql13.dta.options.f1
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: a4e3226a-3917-4ec8-bdf0-472879d231c9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6cc9fbc190645b2f517758b129e92f458dcef316
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846601"
---
# <a name="start-and-use-the-database-engine-tuning-advisor"></a>데이터베이스 엔진 튜닝 관리자 시작 및 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 데이터베이스 엔진 튜닝 관리자를 시작 및 사용하는 방법에 대해 설명합니다. 데이터베이스 튜닝 후 결과를 보고 작업하는 방법은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
##  <a name="Initialize"></a> 데이터베이스 엔진 튜닝 관리자 초기화  
 처음 사용할 때는 **sysadmin** 고정 서버 역할의 멤버인 사용자가 데이터베이스 엔진 튜닝 관리자를 초기화해야 합니다. 튜닝 작업을 지원하려면 **msdb** 데이터베이스에서 여러 시스템 테이블을 만들어야 하기 때문입니다. **db_owner** 고정 데이터베이스 역할의 멤버인 사용자는 초기화를 통해 자신이 소유한 데이터베이스의 테이블에 대한 작업을 튜닝할 수 있습니다.  
  
 시스템 관리자 권한을 가진 사용자가 다음 동작 중 하나를 수행해야 합니다.  
  
-   데이터베이스 엔진 튜닝 관리자 그래픽 사용자 인터페이스를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 인스턴스에 연결합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 엔진 튜닝 관리자 시작](#Start) 을 참조하세요.  
  
-   **dta** 유틸리티를 사용하여 첫 번째 작업을 튜닝합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [dta 유틸리티 사용](#dta) 을 참조하세요.  
  
##  <a name="Start"></a> 데이터베이스 엔진 튜닝 관리자 시작  
 여러 다른 방법으로 데이터베이스 엔진 튜닝 관리자 GUI(그래픽 사용자 인터페이스)를 시작하여 다양한 시나리오에서 데이터베이스 튜닝을 지원할 수 있습니다. 데이터베이스 엔진 튜닝 관리자는 **시작** 메뉴, **의** 도구 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]메뉴, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 쿼리 편집기, **의** 도구 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]메뉴 등과 같은 다양한 방법으로 시작할 수 있습니다. 데이터베이스 엔진 튜닝 관리자를 처음 시작하면 연결할 **인스턴스를 지정할 수 있는** 서버에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대화 상자가 표시됩니다.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 단일 사용자 모드에서 실행 중이면 데이터베이스 엔진 튜닝 관리자를 시작하지 마십시오. 서버가 단일 사용자 모드일 때 데이터베이스 엔진 튜닝 관리자를 시작하려고 시도하면 오류가 반환되고 데이터베이스 엔진 튜닝 관리자가 시작되지 않습니다. 단일 사용자 모드에 대한 자세한 내용은 [단일 사용자 모드로 SQL Server 시작](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)을 참조하세요.  
  
#### <a name="to-start-database-engine-tuning-advisor-from-the-windows-start-menu"></a>Windows 시작 메뉴에서 데이터베이스 엔진 튜닝 관리자를 시작하려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **성능 도구**를 차례로 가리킨 다음 **데이터베이스 엔진 튜닝 관리자**를 클릭합니다.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-management-studio"></a>SQL Server Management Studio에서 데이터베이스 엔진 튜닝 관리자를 시작하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **도구** 메뉴에서 **데이터베이스 엔진 튜닝 관리자**를 클릭합니다.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-from-the-sql-server-management-studio-query-editor"></a>SQL Server Management Studio 쿼리 편집기에서 데이터베이스 엔진 튜닝 관리자를 시작하려면  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스크립트 파일을 엽니다. 자세한 내용은 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)를 참조하세요.  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에서 쿼리를 선택하거나 전체 스크립트를 선택하고 선택 영역을 마우스 오른쪽 단추를 클릭한 다음 **데이터베이스 엔진 튜닝 관리자의 쿼리 분석**을 선택합니다. 데이터베이스 엔진 튜닝 관리자 GUI가 열리고 스크립트를 XML 파일 작업으로 가져옵니다. 세션 이름과 튜닝 옵션을 지정하여 선택한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 작업으로 튜닝할 수 있습니다.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-profiler"></a>SQL Server Profiler에서 데이터베이스 엔진 튜닝 관리자를 시작하려면  
  
1.  SQL Server Profiler **도구** 메뉴에서 **데이터베이스 엔진 튜닝 관리자**를 클릭합니다.  
  
##  <a name="Create"></a> 작업 만들기  
 작업은 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 데이터베이스 엔진 튜닝 관리자는 이러한 작업을 분석하여 서버의 쿼리 성능을 향상시키는 인덱스 또는 분할 전략을 권장합니다.  
  
 다음 방법 중 하나를 사용하여 작업을 만들 수 있습니다.  
  
-   [쿼리 저장소](../../relational-databases/performance/how-query-store-collects-data.md)를 작업으로 사용합니다. 이렇게 하면 작업을 수동으로 만들 필요가 없습니다. 자세한 내용은 [쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md)을 참조하세요.  

      ||  
      |-|  
      |**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  

  
-   계획 캐시를 작업으로 사용합니다. 이렇게 하면 작업을 수동으로 만들 필요가 없습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 튜닝](#Tune) 을 참조하세요.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 쿼리 편집기나 선호하는 텍스트 편집기를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 작업을 수동으로 만들 수 있습니다.  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 추적 파일이나 추적 테이블 작업을 만들 수 있습니다.  
  
    > [!NOTE]  
    >  추적 테이블을 작업 테이블로 사용하는 경우 해당 테이블은 데이터베이스 엔진 튜닝 관리자가 튜닝 중인 서버와 동일한 서버에 있어야 합니다. 다른 서버에 추적 테이블을 만든 경우에는 해당 테이블을 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버로 이동하세요.  
  
-   작업은 각 이벤트에 대한 가중치를 지정할 수 있는 XML 입력 파일에도 포함될 수 있습니다. 포함된 작업을 지정하는 방법은 이 항목의 뒷부분에 나오는 [XML 입력 파일 만들기](#XMLInput) 를 참조하세요.  
  
###  <a name="SSMS"></a> Transact-SQL 스크립트 작업을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 쿼리 편집기를 시작합니다. 자세한 내용은 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)를 참조하세요.  
  
2.  쿼리 편집기에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 입력합니다. 이 스크립트는 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함해야 합니다.  
  
3.  파일을 **.sql** 확장명으로 저장합니다. 데이터베이스 엔진 튜닝 관리자 GUI 및 명령줄 **dta** 유틸리티에서 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 작업으로 사용할 수 있습니다.  
  
###  <a name="Profiler"></a> 추적 파일 및 추적 테이블 작업을 만들려면  
  
1.  다음 중 한 가지 방법을 사용하여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 시작합니다.  
  
    -   **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**, **성능 도구**를 차례로 가리킨 다음 **SQL Server Profiler**를 클릭합니다.  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **도구** 메뉴를 클릭한 다음 **SQL Server Profiler**를 클릭합니다.  
  
2.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Tuning** 템플릿을 사용하는 다음 절차에 따라 추적 파일 또는 테이블을 만듭니다.  
  
    -   [추적 만들기&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
    -   [추적 결과를 파일에 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
         데이터베이스 엔진 튜닝 관리자에서는 작업 추적 파일이 롤오버 파일이라고 가정합니다. 롤오버 파일에 대한 자세한 내용은 [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)을 참조하세요.  
  
    -   [테이블에 추적 결과 저장&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
         추적 테이블을 작업 테이블로 사용하기 전에 추적이 중지되어 있는지 확인하세요.  
  
 SQL Server Profiler Tuning 템플릿을 사용하여 데이터베이스 엔진 튜닝 관리자의 작업을 캡처하는 것이 좋습니다.  
  
 사용자 고유의 템플릿을 사용하려면 다음 추적 이벤트가 캡처되는지 확인하세요.  
  
-   **RPC:Completed**  
  
-   **SQL:BatchCompleted**  
  
-   **SP:StmtCompleted**  
  
 이러한 추적 이벤트의 **Starting** 버전을 사용할 수도 있습니다. **SQL:BatchStarting**을 예로 들 수 있습니다. 한편 이러한 추적 이벤트의 **Completed** 버전에는 데이터베이스 엔진 튜닝 관리자의 작업 튜닝 효율을 높일 수 있도록 **Duration** 열이 포함됩니다. 데이터베이스 엔진 튜닝 관리자는 다른 유형의 추적 이벤트는 튜닝하지 않습니다. 이러한 추적 이벤트에 대한 자세한 내용은 [Stored Procedures Event Category](../../relational-databases/event-classes/stored-procedures-event-category.md) 및 [TSQL Event Category](../../relational-databases/event-classes/tsql-event-category.md)를 참조하세요. SQL 추적 저장 프로시저를 사용하여 추적 파일 작업을 만드는 방법은 [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)를 참조하세요.  
  
### <a name="trace-file-or-trace-table-workloads-that-contain-the-loginname-data-column"></a>LoginName 데이터 열이 포함된 추적 파일 또는 추적 테이블 작업  
 데이터베이스 엔진 튜닝 관리자는 튜닝 프로세스의 일부로 실행 계획 요청을 제출합니다. **LoginName** 데이터 열이 포함된 추적 테이블이나 파일이 작업으로 사용되면 데이터베이스 엔진 튜닝 관리자는 **LoginName**에 지정된 사용자를 가장합니다. 이 사용자에게 추적에 포함된 문의 실행 계획을 실행하고 생성할 수 있는 SHOWPLAN 권한이 없으면 데이터베이스 엔진 튜닝 관리자는 해당 문을 튜닝하지 않습니다.  
  
##### <a name="to-avoid-granting-the-showplan-permission-to-each-user-specified-in-the-loginname-column-of-the-trace"></a>추적의 LoginName 열에 지정된 각 사용자에게 SHOWPLAN 권한을 부여하지 않으려면  
  
1.  추적 파일 또는 테이블 작업을 튜닝합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [데이터베이스 튜닝](#Tune) 을 참조하세요.  
  
2.  튜닝 로그에서 부적절한 권한 때문에 튜닝되지 않은 문을 확인합니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요.  
  
3.  튜닝되지 않은 이벤트에서 **LoginName** 열을 삭제하여 새 작업을 만든 다음 튜닝되지 않은 이벤트만 새 추적 파일이나 테이블에 저장합니다. 추적에서 데이터 열을 삭제하는 방법은 [추적 파일에 대해 이벤트 및 데이터 열 지정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md) 또는 [기존 추적 수정&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)을 참조하세요.  
  
4.  **LoginName** 열이 없는 새 작업을 데이터베이스 엔진 튜닝 관리자에 다시 제출합니다.  
  
 추적에 로그인 정보가 지정되어 있지 않으므로 데이터베이스 엔진 튜닝 관리자에서 새 작업을 튜닝합니다. 문에 대한 **LoginName** 이 없으면 데이터베이스 엔진 튜닝 관리자는 튜닝 세션을 시작한 사용자( **sysadmin** 고정 서버 역할이나 **db_owner** 고정 데이터베이스 역할의 멤버)를 가장하여 해당 문을 튜닝합니다.  
  
##  <a name="Tune"></a> 데이터베이스 튜닝  
 데이터베이스를 튜닝하기 위해서는 데이터베이스 엔진 튜닝 관리자 GUI 또는 **dta** 명령줄 유틸리티를 사용할 수 있습니다.  
  
> [!NOTE]  
>  추적 테이블을 데이터베이스 엔진 튜닝 관리자의 작업으로 사용하기 전에 추적이 중지되었는지 확인합니다. 데이터베이스 엔진 튜닝 관리자에서는 추적 이벤트가 계속 작업으로 기록되는 추적 테이블을 사용할 수 없습니다.  
  
### <a name="use-the-database-engine-tuning-advisor-graphical-user-interface"></a>데이터베이스 엔진 튜닝 관리자 그래픽 사용자 인터페이스 사용  
 데이터베이스 엔진 튜닝 관리자 GUI에서 계획 캐시, 작업 파일 또는 작업 테이블을 사용하여 데이터베이스를 튜닝할 수 있습니다. 데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 현재 튜닝 세션의 결과와 이전 튜닝 세션의 결과를 쉽게 확인할 수 있습니다. 사용자 인터페이스 옵션에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 [사용자 인터페이스 설명](#UI) 을 참조하세요. 데이터베이스 튜닝 후 출력 작업에 대한 자세한 내용은 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)을 참조하세요.  

####  <a name="PlanCache"></a> 쿼리 저장소를 사용하여 데이터베이스를 튜닝하려면
자세한 내용은 [쿼리 저장소의 작업을 사용하여 데이터베이스 튜닝](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md)을 참조하세요.
  
####  <a name="PlanCache"></a> 계획 캐시를 사용하여 데이터베이스를 튜닝하려면  
  
1.  데이터베이스 엔진 튜닝 관리자를 실행한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 로그인합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [데이터베이스 엔진 튜닝 관리자 시작](#Start) 을 참조하세요.  
  
2.  **일반** 탭의 **세션 이름** 에 이름을 입력하여 새 튜닝 세션을 만듭니다. 튜닝 세션을 시작하려면 먼저 **일반** 탭에서 필드를 구성해야 합니다. 튜닝 세션을 시작하기 전에 **튜닝 옵션** 탭의 설정을 수정할 필요는 없습니다.  
  
3.  **계획 캐시** 를 작업 옵션으로 선택합니다. 데이터베이스 엔진 튜닝 관리자가 계획 캐시에서 분석에 사용할 상위 1,000개의 이벤트를 선택합니다.  
  
4.  튜닝할 데이터베이스를 선택하고 필요에 따라 **선택한 테이블**의 각 데이터베이스에서 하나 이상의 테이블을 선택합니다. 모든 데이터베이스에 대한 캐시 항목을 포함하려면 **튜닝 옵션**에서 **고급 옵션** 을 클릭한 다음 **모든 데이터베이스의 계획 캐시 이벤트 포함**을 선택합니다.  
  
5.  **튜닝 로그 저장** 을 선택하여 튜닝 로그 복사본을 저장합니다. 튜닝 로그 복사본을 저장하지 않으려면 이 확인란의 선택을 해제합니다.  
  
     세션을 열고 **진행률** 탭을 선택하여 분석한 후의 튜닝 로그를 확인할 수 있습니다.  
  
6.  **튜닝 옵션** 탭을 클릭한 다음 나열된 옵션 중에서 선택합니다.  
  
7.  **분석 시작**을 클릭합니다.  
  
     튜닝 세션이 시작된 후에 이를 중지하려면 **동작** 메뉴에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **분석 중지(권장 구성)** 는 튜닝 세션을 중지하고 데이터베이스 엔진 튜닝 관리자에서 중지 전 시점까지 수행된 분석을 기반하여 권장 구성을 생성할지 여부를 묻는 메시지를 표시합니다.  
  
    -   **분석 중지** 는 권장 구성을 생성하지 않고 튜닝 세션을 중지합니다.  
  
> [!NOTE]  
>  데이터베이스 엔진 튜닝 관리자의 일시 중지 기능은 지원되지 않습니다. **분석 중지** 또는 **분석 중지(권장 구성)** 도구 모음 단추를 클릭한 후 **분석 시작** 도구 모음 단추를 클릭하면 데이터베이스 엔진 튜닝 관리자가 새 튜닝 세션을 시작합니다.  
  
##### <a name="to-tune-a-database-using-a-workload-file-or-table-as-input"></a>작업 파일이나 테이블을 입력으로 사용하여 데이터베이스를 튜닝하려면  
  
1.  데이터베이스 엔진 튜닝 관리자가 분석 중에 추가, 제거 또는 유지해야 할 데이터베이스 기능(인덱스, 인덱싱된 뷰, 분할)을 결정합니다.  
  
2.  작업을 만듭니다. 자세한 내용은 이 항목의 앞부분에 나오는 [작업 만들기](#Create) 를 참조하세요.  
  
3.  데이터베이스 엔진 튜닝 관리자를 실행한 다음 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 로그인합니다. 자세한 내용은 이 항목의 앞부분에 나오는 [데이터베이스 엔진 튜닝 관리자 시작](#Start) 을 참조하세요.  
  
4.  **일반** 탭의 **세션 이름** 에 이름을 입력하여 새 튜닝 세션을 만듭니다.  
  
5.  **작업 파일** 또는 **테이블** 을 선택하고 파일 경로 또는 인접한 입력란에 테이블 이름을 입력합니다.  
  
     테이블을 지정하는 형식  
  
    ```  
  
    database_name.schema_name.table_name  
    ```  
  
     작업 파일이나 테이블을 검색하려면 **찾아보기**를 클릭합니다. 데이터베이스 엔진 튜닝 관리자는 작업 파일을 롤오버 파일로 가정합니다. 롤오버 파일에 대한 자세한 내용은 [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)을 참조하세요.  
  
     추적 테이블을 작업으로 사용하는 경우 데이터베이스 엔진 튜닝 관리자가 튜닝 중인 서버와 같은 서버에 해당 테이블이 있어야 합니다. 다른 서버에 추적 테이블을 만든 경우에는 이 테이블을 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버로 이동한 다음 작업으로 사용합니다.  
  
6.  5단계에서 선택한 작업을 실행할 데이터베이스 및 테이블을 선택합니다. 테이블을 선택하려면 **선택한 테이블** 화살표를 클릭합니다.  
  
7.  **튜닝 로그 저장** 을 선택하여 튜닝 로그 복사본을 저장합니다. 튜닝 로그 복사본을 저장하지 않으려면 이 확인란의 선택을 해제합니다.  
  
     세션을 열고 **진행률** 탭을 선택하여 분석한 후의 튜닝 로그를 확인할 수 있습니다.  
  
8.  **튜닝 옵션** 탭을 클릭한 다음 나열된 옵션 중에서 선택합니다.  
  
9. 도구 모음에서 **분석 시작** 단추를 클릭합니다.  
  
     튜닝 세션이 시작된 후에 이를 중지하려면 **동작** 메뉴에서 다음 옵션 중 하나를 선택합니다.  
  
    -   **분석 중지(권장 구성)** 는 튜닝 세션을 중지하고 데이터베이스 엔진 튜닝 관리자에서 중지 전 시점까지 수행된 분석을 기반하여 권장 구성을 생성할지 여부를 묻는 메시지를 표시합니다.  
  
    -   **분석 중지** 는 권장 구성을 생성하지 않고 튜닝 세션을 중지합니다.  
  
> [!NOTE]  
>  데이터베이스 엔진 튜닝 관리자의 일시 중지 기능은 지원되지 않습니다. **분석 중지** 또는 **분석 중지(권장 구성)** 도구 모음 단추를 클릭한 후 **분석 시작** 도구 모음 단추를 클릭하면 데이터베이스 엔진 튜닝 관리자가 새 튜닝 세션을 시작합니다.  
  
###  <a name="dta"></a> dta 유틸리티 사용  
 [dta 유틸리티](../../tools/dta/dta-utility.md) 는 데이터베이스를 튜닝하기 위해 사용할 수 있는 명령 프롬프트 실행 파일을 제공합니다. 이 유틸리티를 사용하면 일괄 처리 파일이나 스크립트에 데이터베이스 엔진 튜닝 관리자를 사용할 수 있습니다. **dta** 유틸리티는 계획 캐시 항목, 추적 파일, 추적 테이블 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 작업으로 가져옵니다. 또한 다음 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?linkid=43100)에서 사용 가능한 데이터베이스 엔진 튜닝 관리자 XML 스키마를 따르는 XML 입력을 가져옵니다.  
  
 **dta** 유틸리티에서 작업을 튜닝하기 전에 다음 사항을 고려하세요.  
  
-   추적 테이블을 작업으로 사용하는 경우 데이터베이스 엔진 튜닝 관리자가 튜닝 중인 서버와 같은 서버에 해당 테이블이 있어야 합니다. 다른 서버에 추적 테이블을 만든 경우에는 이 테이블을 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버로 이동합니다.  
  
-   추적 테이블을 데이터베이스 엔진 튜닝 관리자의 작업으로 사용하기 전에 추적이 중지되었는지 확인합니다. 데이터베이스 엔진 튜닝 관리자에서는 추적 이벤트가 계속 작업으로 기록되는 추적 테이블을 사용할 수 없습니다.  
  
-   튜닝 세션이 예상보다 오랜 시간 계속 실행되는 경우 Ctrl+C를 눌러 튜닝 세션을 중지하고 **dta** 에서 현재까지 완료한 분석에 따라 권장 사항을 생성할 수 있습니다. 권장 구성을 생성할지 여부를 결정하라는 메시지가 표시됩니다. Ctrl+C를 다시 누르면 권장 구성을 생성하지 않고 튜닝 세션이 중지됩니다.  
  
 **dta** 유틸리티 구문에 대한 자세한 내용 및 예제는 [dta Utility](../../tools/dta/dta-utility.md)를 참조하세요.  
  
##### <a name="to-tune-a-database-by-using-the-plan-cache"></a>계획 캐시를 사용하여 데이터베이스를 튜닝하려면  
  
1.  **-ip** 옵션을 지정합니다. 선택한 데이터베이스에 대한 상위 1,000개의 계획 캐시 이벤트가 분석됩니다.  
  
     명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    dta -E -D DatabaseName -ip -s SessionName  
    ```  
  
2.  분석에 사용할 이벤트 수를 수정하려면 **–n** 옵션을 지정합니다. 다음 예에서는 캐시 항목 수를 2,000개로 증가시킵니다.  
  
    ```  
    dta -E -D DatabaseName -ip –n 2000-s SessionName1  
    ```  
  
3.  인스턴스에 있는 모든 데이터베이스의 이벤트를 분석하려면 **-ipf** 옵션을 지정합니다.  
  
    ```  
    dta -E -D DatabaseName -ip –ipf –n 2000 -s SessionName2  
    ```  
  
##### <a name="to-tune-a-database-by-using-a-workload-and-dta-utility-default-settings"></a>작업 및 dta 유틸리티 기본 설정을 사용하여 데이터베이스를 튜닝하려면  
  
1.  데이터베이스 엔진 튜닝 관리자가 분석 중에 추가, 제거 또는 유지해야 할 데이터베이스 기능(인덱스, 인덱싱된 뷰, 분할)을 결정합니다.  
  
2.  작업을 만듭니다. 자세한 내용은 이 항목의 앞부분에 나오는 [작업 만들기](#Create) 를 참조하세요.  
  
3.  명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName  
    ```  
  
     여기에서 `-E` 는 튜닝 세션이 로그인 ID와 암호 대신에 트러스트된 연결을 사용하도록 지정하고 `-D` 는 튜닝할 데이터베이스의 이름을 지정합니다. 기본적으로 이 유틸리티는 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결합니다. 다음 절차에 표시된 대로 원격 데이터베이스를 지정하거나 명명된 인스턴스를 지정하려면 `-S` 옵션을 사용합니다. `-if` 옵션은 작업 파일([!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 추적 파일)의 이름과 경로를 지정하고 `-s` 옵션은 튜닝 세션의 이름을 지정합니다.  
  
     여기에 표시된 네 가지 옵션(데이터베이스 이름, 작업, 연결 유형, 세션 이름)은 필수 항목입니다.  
  
##### <a name="to-tune-a-remote-database-or-a-named-instance-for-a-specific-duration"></a>원격 데이터베이스 또는 특정 기간 동안 명명된 인스턴스를 튜닝하려면  
  
1.  데이터베이스 엔진 튜닝 관리자가 분석 중에 추가, 제거 또는 유지해야 할 데이터베이스 기능(인덱스, 인덱싱된 뷰, 분할)을 결정합니다.  
  
2.  작업을 만듭니다. 자세한 내용은 이 항목의 앞부분에 나오는 [작업 만들기](#Create) 를 참조하세요.  
  
3.  명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    dta -S ServerName\Instance -D DatabaseName -it WorkloadTableName   
    -U LoginID -P Password -s SessionName -A TuningTimeInMinutes  
    ```  
  
     여기에서 `-S` 는 원격 서버 이름과 인스턴스(또는 로컬 서버에서 명명된 인스턴스)를 지정하고 `-D` 는 튜닝할 데이터베이스의 이름을 지정합니다. `-it` 옵션은 작업 테이블의 이름을 지정하고, `-U` 및 `-P` 는 원격 데이터베이스에 대한 로그인 ID와 암호를 지정하고, `-s` 는 튜닝 세션 이름을 지정하고, `-A` 는 튜닝 세션 기간(단위 분)을 지정합니다. 기본적으로 **dta** 유틸리티는 8시간 튜닝 기간을 사용합니다. 데이터베이스 엔진 튜닝 관리자가 시간 제한 없이 작업을 튜닝하도록 하려면 **옵션에** 0 `-A` (영)을 지정합니다.  
  
##### <a name="to-tune-a-database-using-an-xml-input-file"></a>XML 입력 파일로 데이터베이스를 튜닝하려면  
  
1.  데이터베이스 엔진 튜닝 관리자가 분석 중에 추가, 제거 또는 유지해야 할 데이터베이스 기능(인덱스, 인덱싱된 뷰, 분할)을 결정합니다.  
  
2.  작업을 만듭니다. 자세한 내용은 이 항목의 앞부분에 나오는 [작업 만들기](#Create) 를 참조하세요.  
  
3.  XML 입력 파일을 만듭니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [XML 입력 파일 만들기](#XMLInput) 를 참조하세요.  
  
4.  명령 프롬프트에서 다음을 입력합니다.  
  
    ```  
    dta -E -S ServerName\Instance -s SessionName -ix PathToXMLInputFile  
    ```  
  
     여기에서 `-E` 는 트러스트된 연결을 지정하고, `-S` 는 원격 서버와 인스턴스 또는 로컬 서버에서 명명된 인스턴스를 지정하고, `-s` 는 튜닝 세션 이름을 지정하고, `-ix` 는 튜닝 세션에 사용할 XML 입력 파일을 지정합니다.  
  
5.  유틸리티가 작업 튜닝을 마친 후에는 데이터베이스 엔진 튜닝 관리자 GUI를 사용하여 튜닝 세션의 결과를 볼 수 있습니다. 다른 방법으로 **-ox** 옵션을 사용하여 튜닝 권장 구성이 XML 파일에 기록되도록 지정할 수도 있습니다. 자세한 내용은 [dta Utility](../../tools/dta/dta-utility.md)을 참조하세요.  
  
##  <a name="XMLInput"></a> XML 입력 파일 만들기  
 숙련된 XML 개발자인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 작업을 튜닝할 때 사용하는 XML 형식의 파일을 만들 수 있습니다. 이러한 XML 파일을 만들려면 선호하는 XML 도구를 사용하여 예제 파일을 편집하거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 XML 스키마에서 인스턴스를 생성합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 XML 스키마는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치의 다음 위치에 저장됩니다.  
  
 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 XML 스키마는 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)에서 온라인으로도 제공됩니다.  
  
 이 페이지에서는 많은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 스키마를 제공합니다. 페이지 아래로 스크롤하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 행을 찾으세요.  
  
#### <a name="to-create-an-xml-input-file-to-tune-workloads"></a>작업을 튜닝할 XML 입력 파일을 만들려면  
  
1.  작업을 만듭니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]의 튜닝 템플릿으로 추적 파일 또는 테이블을 사용하거나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 만들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 대표적인 작업을 재현할 수 있습니다. 자세한 내용은 이 항목의 앞부분에 나오는 [작업 만들기](#Create) 를 참조하세요.  
  
2.  다음 중 한 가지 방법으로 XML 입력 파일을 만듭니다.  
  
    -   [XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md) 중 하나를 복사하여 선호하는 XML 편집기에 붙여넣습니다. 값을 변경하여 사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 적절한 인수를 지정한 다음 XML 파일을 저장합니다.  
  
    -   선호하는 XML 도구를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자 XML 스키마에서 인스턴스를 생성합니다.  
  
3.  만든 XML 입력 파일을 **dta** 명령줄 유틸리티의 입력으로 사용하여 작업을 튜닝합니다. 이 유틸리티에서 XML 입력 파일을 사용하는 방법은 이 항목의 앞부분에 나오는 [dta 유틸리티 사용](#dta) 섹션을 참조하세요.  
  
> [!NOTE]  
>  XML 입력 파일에 직접 지정되는 작업인 인라인 작업을 사용하려면 [인라인 작업이 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md) 샘플을 사용하세요.  
  
##  <a name="UI"></a> 사용자 인터페이스 설명  
  
### <a name="tools-menuoptions-page"></a>도구 메뉴/옵션 페이지  
 이 대화 상자를 사용하여 데이터베이스 엔진 튜닝 관리자에 대한 일반 구성 매개 변수를 지정할 수 있습니다.  
  
 **시작 시**  
 데이터베이스 엔진 튜닝 관리자 시작 시 수행할 작업을 데이터베이스 연결 없이 열기, **새 연결** 대화 상자 표시, 새 세션 표시 또는 마지막으로 로드된 세션 로드 중에서 지정합니다.  
  
 **글꼴 변경**  
 데이터베이스 엔진 튜닝 관리자 테이블에 사용되는 글꼴을 지정합니다.  
  
 **가장 최근에 사용한 목록의 항목 수**  
 **파일** 메뉴의 **최근에 사용한 세션** 또는 **최근에 사용한 파일** 에 표시될 세션 또는 파일의 수를 지정합니다.  
  
 **마지막 튜닝 옵션 저장**  
 여러 세션에서 튜닝 옵션을 유지합니다. 기본적으로 선택되어 있습니다. 항상 데이터베이스 엔진 튜닝 관리자 기본값으로 시작하려면 이 확인란의 선택을 취소합니다.  
  
 **세션을 영구적으로 삭제하기 전에 확인**  
 세션을 삭제하기 전에 확인 대화 상자를 표시합니다.  
  
 **세션 분석을 중지하기 전에 확인**  
 작업 분석을 중지하기 전에 확인 대화 상자를 표시합니다.  
  
#### <a name="general-tab-options"></a>일반 탭 옵션  
 튜닝 세션을 시작하려면 먼저 **일반** 탭에서 필드를 구성해야 합니다. 튜닝 세션을 시작하기 전에 **튜닝 옵션** 탭의 설정을 수정할 필요는 없습니다.  
  
 **세션 이름**  
 세션의 이름을 지정합니다. 세션 이름 옵션은 세션의 이름을 튜닝 세션과 연결합니다. 이 이름을 참조하여 나중에 튜닝 세션을 검토할 수 있습니다.  
  
 **최근에 사용한 파일**  
 작업에 사용할 .sql 스크립트 또는 추적 파일을 지정합니다. 이 입력란에 경로와 파일 이름을 지정합니다. 데이터베이스 엔진 튜닝 관리자에서는 작업 추적 파일이 롤오버 파일이라고 가정합니다. 롤오버 파일에 대한 자세한 내용은 [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)을 참조하세요.  
  
 **테이블**  
 작업에 사용할 추적 테이블을 지정합니다. 해당 입력란에 다음과 같이 추적 테이블의 정규화된 이름을 지정합니다.  
  
```  
database_name.owner_name.table_name  
```  
  
-   추적 테이블을 작업 테이블로 사용하기 전에 추적이 중지되어 있는지 확인하세요.  
  
-   추적 테이블은 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버와 같은 서버에 있어야 합니다. 다른 서버에 추적 테이블을 만든 경우에는 이 테이블을 데이터베이스 엔진 튜닝 관리자가 튜닝하는 서버로 이동합니다.  
  
 **계획 캐시**  
 계획 캐시를 작업으로 지정합니다. 이렇게 하면 작업을 수동으로 만들 필요가 없습니다. 데이터베이스 엔진 튜닝 관리자는 분석에 사용할 상위 1,000개의 이벤트를 선택합니다.  
  
 **Xml**  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 작업 쿼리를 가져오지 않은 경우에는 이 옵션이 나타나지 않습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 작업 쿼리를 가져오려면  
  
1.  쿼리 편집기에 쿼리를 입력한 다음 선택합니다.  
  
2.  선택한 쿼리를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 엔진 튜닝 관리자의 쿼리 분석**을 클릭합니다.  
  
 **작업 파일(또는 테이블)을 찾습니다.**  
 작업 원본으로 **파일** 이나 **테이블** 을 선택한 경우 대상을 선택하려면 이 찾아보기 단추를 사용합니다.  
  
 **XML 작업을 미리 봅니다.**  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 가져온 XML 형식 작업을 봅니다.  
  
 **작업 분석용 데이터베이스**  
 작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결하는 첫 번째 데이터베이스를 지정합니다. 튜닝이 시작된 후 데이터베이스 엔진 튜닝 관리자는 작업에 포함된 `USE DATABASE` 문으로 지정한 데이터베이스에 연결합니다.  
  
 **튜닝할 데이터베이스 및 테이블 선택**  
 튜닝할 데이터베이스와 테이블을 지정합니다. 모든 데이터베이스를 지정하려면 **이름** 열 머리글의 확인란을 선택합니다. 특정 데이터베이스를 지정하려면 데이터베이스 이름 옆의 확인란을 선택합니다. 기본적으로 선택한 데이터베이스에 있는 모든 테이블이 자동으로 튜닝 세션에 포함됩니다. 특정 테이블을 제외하려면 **선택한 테이블** 열의 화살표를 클릭한 다음 튜닝하지 않을 테이블 옆에 있는 확인란의 선택을 취소합니다.  
  
 **선택한 테이블** 아래쪽 화살표  
 테이블 목록을 확장하여 튜닝할 테이블을 선택할 수 있도록 해 줍니다.  
  
 **튜닝 로그 저장**  
 로그를 만들어 세션 중 발생한 오류를 기록합니다.  
  
> [!NOTE]  
>  데이터베이스 엔진 튜닝 관리자는 **일반** 탭에 표시되는 테이블의 행 정보를 자동으로 업데이트하지 않습니다. 대신 데이터베이스의 메타데이터를 참조합니다. 행 정보가 최신 정보가 아니라고 생각되는 경우에는 관련 개체에 대해 DBCC UPDATEUSAGE 명령을 실행하세요.  
  
##### <a name="tuning-tab-options"></a>튜닝 탭 옵션  
 **튜닝 옵션** 탭을 사용하여 일반 튜닝 옵션의 기본 설정을 수정할 수 있습니다. 튜닝 세션을 시작하기 전에 **튜닝 옵션** 탭의 설정을 수정할 필요는 없습니다.  
  
 **튜닝 시간 제한**  
 현재 튜닝 세션의 시간을 제한합니다. 이 시간을 늘일수록 보다 정확한 권장 구성이 생성됩니다. 최적의 권장 구성을 생성하려면 이 옵션을 선택하지 않도록 해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 사용하면 분석하는 동안 시스템 리소스가 사용됩니다. 튜닝 중인 서버에서 작업량이 많을 것으로 예상되는 기간 전에 튜닝을 중지하려면 **튜닝 시간 제한** 을 사용합니다.  
  
 **고급 옵션**  
 **고급 튜닝 옵션** 대화 상자를 사용하여 최대 공간, 최대 키 열 수, 온라인 인덱스 등에 대한 권장 설정을 구성할 수 있습니다.  
  
 **권장 구성에 필요한 최대 공간 정의(MB)**  
 데이터베이스 엔진 튜닝 관리자에서 권장하는 물리적 디자인 구조에 사용할 최대 공간의 크기를 입력합니다.  
  
 값을 입력하지 않으면 데이터베이스 엔진 튜닝 관리자에서 다음 공간 값 중에 작은 값을 사용합니다.  
  
-   현재 원시 데이터 크기의 3배이며 데이터베이스의 테이블에 있는 힙과 클러스터형 인덱스의 전체 크기를 포함합니다.  
  
-   연결된 모든 디스크 드라이브의 여유 공간과 원시 데이터 크기를 더한 것입니다.  
  
 **모든 데이터베이스의 계획 캐시 이벤트 포함**  
 모든 데이터베이스의 계획 캐시 이벤트를 분석하도록 지정합니다.  
  
 **인덱스당 최대 열 개수**  
 인덱스에 포함할 최대 열 개수를 지정합니다. 기본값은 1023입니다.  
  
 **모든 권장 구성이 오프라인임**  
 최적의 권장 구성을 생성하지만 온라인에서 물리적 디자인 구조를 생성하는 것은 권장하지 않습니다.  
  
 **가능한 경우 온라인 권장 구성 생성**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 만들어 권장 구성을 구현하는 경우 오프라인으로 더 빨리 구현할 수 있는 방법이 있더라도 서버에서 온라인으로 구현할 수 있는 방법을 선택합니다.  
  
 **온라인 권장 구성만 생성**  
 서버를 온라인 상태로 유지할 수 있는 권장 구성만 생성합니다.  
  
 **중지 시간**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 중지할 날짜 및 시간을 입력합니다.  
  
 **인덱스와 인덱싱된 뷰**  
 클러스터형 인덱스, 비클러스터형 인덱스 및 인덱싱된 뷰 추가에 대한 권장 구성을 포함하려면 이 확인란을 선택합니다.  
  
 **인덱싱된 뷰**  
 인덱싱된 뷰 추가에 대한 권장 구성만 포함됩니다. 클러스터형 인덱스와 비클러스터형 인덱스에 대한 권장 구성은 생성되지 않습니다.  
  
 **필터링된 인덱스 포함**  
 필터링된 인덱스 추가에 대한 권장 구성을 포함합니다. **인덱스와 인덱싱된 뷰**, **인덱스**, **비클러스터형 인덱스**중 하나를 선택한 경우 이 옵션을 사용할 수 있습니다.  
  
 **인덱스**  
 클러스터형 인덱스 및 비클러스터형 인덱스 추가에 대한 권장 구성만 포함됩니다. 인덱싱된 뷰에 대한 권장 구성은 생성되지 않습니다.  
  
 **비클러스터형 인덱스**  
 비클러스터형 인덱스에 대한 권장 구성만 포함됩니다. 클러스터형 인덱스와 인덱싱된 뷰에 대한 권장 구성은 생성되지 않습니다.  
  
 **기존 PDS의 사용률만 평가**  
 현재 인덱스의 효율성만 평가되며 추가 인덱스 또는 인덱싱된 뷰에 대한 권장 구성은 생성되지 않습니다.  
  
 **분할 안 함**  
 분할에 대한 권장 구성이 생성되지 않습니다.  
  
 **전체 분할**  
 분할에 대한 권장 구성이 포함됩니다.  
  
 **정렬된 분할**  
 파티션을 쉽게 관리할 수 있도록 새로운 권장 파티션이 정렬됩니다.  
  
 **기존 PDS 유지 안 함**  
 불필요한 기존 인덱스, 뷰 및 분할 삭제에 대한 권장 구성이 생성됩니다. 기존 PDS(실제 디자인 구조)가 작업을 처리하는 데 효율적인 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 PDS 삭제가 권장되지 않습니다.  
  
 **인덱스만 유지**  
 기존 인덱스가 모두 유지되지만 불필요한 인덱싱된 뷰 및 분할의 삭제에 대한 권장 구성이 생성됩니다.  
  
 **기존 PDS 모두 유지**  
 기존 인덱스, 인덱싱된 뷰 및 분할이 모두 유지됩니다.  
  
 **클러스터형 인덱스만 유지**  
 기존 클러스터형 인덱스가 모두 유지되지만 불필요한 인덱싱된 뷰, 분할 및 비클러스터형 인덱스의 삭제에 대한 권장 구성이 생성됩니다.  
  
 **정렬된 분할 유지**  
 현재 정렬된 상태로 분할 구조가 유지되지만 불필요한 인덱싱된 뷰, 인덱스 및 정렬되지 않은 분할의 삭제에 대한 권장 구성이 생성됩니다. 권장 구성에 따른 모든 추가 분할은 현재 파티션 구성표에 맞춰 정렬됩니다.  
  
###### <a name="progress-tab-options"></a>진행률 탭 옵션  
 데이터베이스 엔진 튜닝 관리자에서 작업 분석이 시작되면 데이터베이스 엔진 튜닝 관리자의 **진행** 탭이 표시됩니다.  
  
 튜닝 세션이 시작된 후에 이를 중지하려면 **동작** 메뉴에서 다음 옵션 중 하나를 선택합니다.  
  
-   **분석 중지(권장 구성)** 는 튜닝 세션을 중지하고 데이터베이스 엔진 튜닝 관리자에서 중지 전 시점까지 수행된 분석을 기반하여 권장 구성을 생성할지 여부를 묻는 메시지를 표시합니다.  
  
-   **분석 중지** 는 권장 구성을 생성하지 않고 튜닝 세션을 중지합니다.  
  
 **튜닝 진행률**  
 현재 진행 상태를 나타냅니다. 완료한 동작 수와 수신된 오류, 성공 및 경고 메시지 수를 표시합니다.  
  
 **세부 정보**  
 상태를 나타내는 아이콘이 포함되어 있습니다.  
  
 **작업**  
 수행 중인 단계를 표시합니다.  
  
 **상태**  
 동작 단계의 상태를 표시합니다.  
  
 **메시지**  
 동작 단계에서 반환된 모든 메시지가 포함되어 있습니다.  
  
 **튜닝 로그**  
 이 튜닝 세션에 관한 정보가 포함되어 있습니다. 이 로그를 인쇄하려면 로그를 마우스 오른쪽 단추로 클릭한 다음 **인쇄**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [dta Utility](../../tools/dta/dta-utility.md)  
  
  
