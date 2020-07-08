---
title: Profiler를 사용하여 SQL 추적 컬렉션 세트 만들기
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace collector set
ms.assetid: b6941dc0-50f5-475d-82eb-ce7c68117489
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: fdd751f282f1ba62150d5257dde04798962ecb84
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715533"
---
# <a name="use-sql-server-profiler-to-create-a-sql-trace-collection-set"></a>SQL Server Profiler를 사용하여 SQL 추적 컬렉션 집합 만들기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 의 서버 쪽 추적 기능을 이용하여 일반 SQL 추적 수집기 유형을 사용하는 컬렉션 집합을 만들기 위한 추적 정의를 내보낼 수 있습니다. 이 프로세스는 두 부분으로 구성되어 있습니다.  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적을 만들고 내보냅니다.  
  
2.  내보낸 추적을 기반으로 새 컬렉션 집합을 스크립팅합니다.  

 다음 절차에 대한 시나리오에는 완료하는 데 80밀리초 이상이 걸리는 저장 프로시저에 대한 정보를 수집하는 과정이 포함되어 있습니다. 이 프로시저를 완료하려면 다음을 수행할 수 있어야 합니다.  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 추적을 만들고 구성합니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 쿼리를 열고 편집하며 실행합니다.  
  
### <a name="create-and-export-a-sql-server-profiler-trace"></a>SQL Server Profiler 추적 만들기 및 내보내기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 엽니다. **도구** 메뉴에서 **SQL Server Profiler**를 클릭하면 됩니다.  
  
2.  **서버에 연결** 대화 상자에서 **취소**를 클릭합니다.  
  
3.  이 시나리오에서는 기간 값을 밀리초로 표시(기본 설정)하도록 구성되어 있는지 확인합니다. 이렇게 하려면 다음 단계를 수행하세요.  
  
    1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
    2.  **표시 옵션** 영역에서 기간 열에 값 표시(마이크로초) 확인란이 선택 취소되어 있는지 확인합니다.  
  
    3.  **확인** 을 클릭하여 **일반 옵션** 대화 상자를 닫습니다.  
  
4.  **파일** 메뉴에서 **새 추적**을 클릭합니다.  
  
5.  **서버에 연결** 대화 상자에서 연결할 서버를 선택한 다음 **연결**을 클릭합니다.  
  
     **추적 속성** 대화 상자가 나타납니다.  
  
6.  **일반** 탭에서 다음을 수행합니다.  
  
    1.  **추적 이름** 상자에서 추적에 사용할 이름을 입력합니다. 이 예에서 추적 이름은 **SPgt80**입니다.  
  
    2.  **템플릿 사용**목록에서 추적에 사용할 템플릿을 선택합니다. 이 예에서는 **TSQL_SPs**를 클릭합니다.  
  
7.  **이벤트 선택** 탭에서 다음을 수행합니다.  
  
    1.  추적에 사용할 이벤트를 지정합니다. 이 예에서는 **이벤트** 열에서 **ExistingConnection** 및 **SP:Completed**를 제외한 모든 확인란을 선택 취소합니다.  
  
    2.  오른쪽 아래 모서리에 있는 **모든 열 표시** 확인란을 선택합니다.  
  
    3.  **SP:Completed** 행을 클릭합니다.  
  
    4.  열을 스크롤하여 **기간** 열을 찾은 다음 **기간** 확인란을 선택합니다.  
  
8.  오른쪽 아래 모서리에 있는 **열 필터** 를 클릭하여 **필터 편집** 대화 상자를 엽니다. **필터 편집** 대화 상자에서 다음을 수행합니다.  
  
    1.  필터 목록에서 **기간**을 클릭합니다.  
  
    2.  부울 연산자 창에서 **크거나 같음** 노드를 확장하고 **80** 을 값으로 입력한 다음 **확인**을 클릭합니다.  
  
9. **실행** 을 클릭하여 추적을 시작합니다.  
  
10. 도구 모음에서 **선택한 추적 중지** 또는 **선택한 추적 일시 중지**를 클릭합니다.  
  
11. **파일** 메뉴에서 **내보내기**, **추적 정의 스크립트**를 차례로 가리킨 다음 **SQL 추적 컬렉션 집합**을 클릭합니다.  
  
12. **다른 이름으로 저장** 대화 상자의 **파일 이름** 상자에 추적 정의에 사용할 이름을 입력한 다음 원하는 위치에 파일을 저장합니다. 이 예에서는 파일 이름이 추적 이름(SPgt80)과 동일합니다.  
  
13. 파일이 성공적으로 저장되었다는 메시지가 나타나면 **확인** 을 클릭한 다음 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 닫습니다.  
  
### <a name="script-a-new-collection-set-from-a-sql-server-profiler-trace"></a>SQL Server Profiler 추적에서 새 컬렉션 집합 스크립팅  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **파일** 메뉴에서 **열기** 를 가리킨 다음 **파일**을 클릭합니다.  
  
2.  **파일 열기** 대화 상자에서 이전 절차에서 만든 파일(SPgt80)을 찾아 엽니다.  
  
     저장한 추적 정보는 쿼리 창에서 열리고 새 컬렉션 집합을 만들기 위해 실행할 수 있는 스크립트로 병합됩니다.  
  
3.  스크립트를 스크롤한 다음 스크립트 주석 텍스트에서 설명하는 다음과 같은 대체 작업을 수행합니다.  
  
    -   **SQLTrace Collection Set Name Here** 를 컬렉션 집합에 사용할 이름으로 바꿉니다. 이 예에서는 컬렉션 집합 이름을 **SPROC_CollectionSet**으로 정합니다.  
  
    -   **SQLTrace Collection Item Name Here** 를 컬렉션 항목에 사용할 이름으로 바꿉니다. 이 예에서는 컬렉션 항목 이름을 **SPROC_Collection_Item**으로 정합니다.  
  
4.  **실행** 을 클릭하여 쿼리를 실행하고 컬렉션 집합을 만듭니다.  
  
5.  개체 탐색기에서 컬렉션 집합이 만들어졌는지 확인합니다. 이렇게 하려면 다음 단계를 수행하세요.  
  
    1.  **관리**를 마우스 오른쪽 단추로 클릭한 다음 **새로 고침**을 클릭합니다.  
  
    2.  **관리**와 **데이터 컬렉션**을 차례로 확장합니다.  
  
     **시스템 데이터 컬렉션 집합** 노드와 동일한 수준에서 **SPROC_CollectionSet** 컬렉션 집합이 표시됩니다. 이 컬렉션 집합은 기본적으로 해제되어 있습니다.  
  
6.  개체 탐색기를 사용하여 SPROC_CollectionSet에 대해 컬렉션 모드 및 업로드 일정 등의 속성을 편집합니다. 데이터 수집기와 함께 제공되는 시스템 데이터 컬렉션 집합의 경우와 동일한 절차를 따릅니다.  
  
## <a name="example"></a>예제  
 다음 코드 샘플은 이전 절차에서 설명한 단계의 결과로 생성되는 최종 스크립트입니다.  
  
```sql
/*************************************************************/  
-- SQL Trace collection set generated from SQL Server Profiler  
-- Date: 11/19/2007  12:55:31 AM  
/*************************************************************/  
  
USE msdb;
GO  
  
BEGIN TRANSACTION  
BEGIN TRY  
  
-- Define collection set  
-- ***  
-- *** Replace 'SqlTrace Collection Set Name Here' in the   
-- *** following script with the name you want  
-- *** to use for the collection set.  
-- ***  
DECLARE @collection_set_id int;  
EXEC [dbo].[sp_syscollector_create_collection_set]  
    @name = N'SPROC_CollectionSet',  
    @schedule_name = N'CollectorSchedule_Every_15min',  
    @collection_mode = 0, -- cached mode needed for Trace collections  
    @logging_level = 0, -- minimum logging  
    @days_until_expiration = 5,  
    @description = N'Collection set generated by SQL Server Profiler',  
    @collection_set_id = @collection_set_id output;  
SELECT @collection_set_id;  
  
-- Define input and output variables for the collection item.  
DECLARE @trace_definition xml;  
DECLARE @collection_item_id int;  
  
-- Define the trace parameters as an XML variable  
SELECT @trace_definition = convert(xml,   
N'<ns:SqlTraceCollector xmlns:ns"DataCollectorType" use_default="0">  
<Events>  
  <EventType name="Sessions">  
    <Event id="17" name="ExistingConnection" columnslist="1,2,14,26,3,35,12" />  
  </EventType>  
  <EventType name="Stored Procedures">  
    <Event id="43" name="SP:Completed" columnslist="1,2,26,34,3,35,12,13,14,22" />  
  </EventType>  
</Events>  
<Filters>  
  <Filter columnid="13" columnname="Duration" logical_operator="AND" comparison_operator="GE" value="80000L" />  
</Filters>  
</ns:SqlTraceCollector>  
');  
  
-- Retrieve the collector type GUID for the trace collector type.  
DECLARE @collector_type_GUID uniqueidentifier;  
SELECT @collector_type_GUID = collector_type_uid
  FROM [dbo].[syscollector_collector_types]
  WHERE name = N'Generic SQL Trace Collector Type';  
  
-- Create the trace collection item.  
-- ***  
-- *** Replace 'SqlTrace Collection Item Name Here' in   
-- *** the following script with the name you want to  
-- *** use for the collection item.  
-- ***  
EXEC [dbo].[sp_syscollector_create_collection_item]  
   @collection_set_id = @collection_set_id,  
   @collector_type_uid = @collector_type_GUID,  
   @name = N'SPROC_Collection_Item',  
   @frequency = 900, -- specified the frequency for checking to see if trace is still running  
   @parameters = @trace_definition,  
   @collection_item_id = @collection_item_id output;  
SELECT @collection_item_id;  
  
COMMIT TRANSACTION;  
END TRY  
  
BEGIN CATCH  
ROLLBACK TRANSACTION;  
DECLARE @ErrorMessage nvarchar(4000);  
DECLARE @ErrorSeverity int;  
DECLARE @ErrorState int;  
DECLARE @ErrorNumber int;  
DECLARE @ErrorLine int;  
DECLARE @ErrorProcedure nvarchar(200);  
SELECT @ErrorLine = ERROR_LINE(),  
       @ErrorSeverity = ERROR_SEVERITY(),  
       @ErrorState = ERROR_STATE(),  
       @ErrorNumber = ERROR_NUMBER(),  
       @ErrorMessage = ERROR_MESSAGE(),  
       @ErrorProcedure = ISNULL(ERROR_PROCEDURE(), '-');  
RAISERROR (14684, @ErrorSeverity, 1 , @ErrorNumber,
  @ErrorSeverity, @ErrorState, @ErrorProcedure, @ErrorLine, @ErrorMessage);  
END CATCH;  
GO  
```  
  
  
