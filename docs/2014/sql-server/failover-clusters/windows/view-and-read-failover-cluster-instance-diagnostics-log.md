---
title: 장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19308ee2838238f0dea6cfdaeb228a250591613b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63049339"
---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기
  SQL Server 리소스 DLL에 대한 모든 오류 및 경고 이벤트는 Windows 이벤트 로그에 기록됩니다. [sp_server_diagnostics&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 시스템 저장 프로시저에서 캡처된 SQL Server 관련 진단 정보의 실행 로그는 SQL Server 장애 조치(failover) 클러스터 진단(*SQLDIAG* 로그라고도 함) 로그 파일에 기록됩니다.  
  
-   **시작하기 전 주의 사항:**  [권장 사항](#Recommendations), [보안](#Security)  
  
-   **진단 로그를 보려면:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **진단 로그 설정을 구성하려면:** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
 기본적으로 SQLDIAG는 SQL Server 인스턴스 디렉터리의 로컬 LOG 폴더에 저장 됩니다 (예: ' C_Files\Microsoft SQL Server\MSSQL12.). \<AlwaysOn Fci (장애 조치 (Failover) 클러스터 인스턴스) 소유 노드의 InstanceName> \mssql\log '입니다. 각 SQLDIAG 로그 파일의 크기는 100MB로 고정됩니다. 새 로그에 재활용하기 전에 이러한 로그 파일이 컴퓨터에 10개 저장됩니다.  
  
 로그는 확장 이벤트 파일 형식을 사용합니다. **sys.fn_xe_file_target_read_file** 시스템 함수를 사용하여 확장 이벤트에서 만든 파일을 읽을 수 있습니다. 행당 하나의 이벤트가 XML 형식으로 반환됩니다. XML 데이터를 결과 집합으로 구문 분석하려면 시스템 뷰를 쿼리합니다. 자세한 내용은 [sys.fn_xe_file_target_read_file&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **fn_xe_file_target_read_file**을 실행하려면 VIEW SERVER STATE 권한이 필요합니다.  
  
 SQL Server Management Studio를 관리자로 열기  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **진단 로그 파일을 보려면:**  
  
1.  **파일** 메뉴에서 **열기**, **파일**을 선택한 다음 보려는 진단 로그 파일을 선택합니다.  
  
2.  이벤트가 왼쪽 창에 행으로 표시되며 기본적으로 **이름**및 **타임스탬프** 라는 두 열만 표시됩니다.  
  
     또한 **ExtendedEvents** 메뉴도 활성화됩니다.  
  
3.  추가 열을 보려면 **ExtendedEvents** 메뉴로 이동하고 **열 선택**을 선택합니다.  
  
     표시할 열을 선택할 수 있는 사용 가능한 열이 포함된 대화 상자가 열립니다.  
  
4.  **ExtendedEvents** 메뉴를 사용하고 **필터** 옵션을 선택하여 이벤트 데이터를 필터링하고 정렬할 수 있습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **진단 로그 파일을 보려면:**  
  
 SQLDIAG 로그 파일의 모든 로그 항목을 보려면 다음 쿼리를 사용합니다.  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  WHERE 절을 사용하여 특정 구성 요소 또는 상태에 대한 결과를 필터링할 수 있습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlConfigure"></a> Transact-SQL 사용  
 **진단 로그 속성을 구성하려면**  
  
> [!NOTE]  
>  이 절차에 대한 예는 이 섹션의 뒷부분에 나오는 [예제(Transact-SQL)](#TsqlExample)을 참조하세요.  
  
 DDL (데이터 정의 언어) 문을 `ALTER SERVER CONFIGURATION`사용 하 여 [sp_server_diagnostics &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 프로시저에서 캡처한 진단 데이터의 로깅을 시작 하거나 중지 하 고 로그 파일 롤오버 수, 로그 파일 크기 및 파일 위치와 같은 SQLDIAG 로그 구성 매개 변수를 설정할 수 있습니다. 구문에 대한 자세한 내용은 [Setting diagnostic log options](/sql/t-sql/statements/alter-server-configuration-transact-sql#Diagnostic)을 참조하세요.  
  
###  <a name="examples-transact-sql"></a><a name="ConfigTsqlExample"></a>예 (Transact-sql)  
  
####  <a name="setting-diagnostic-log-options"></a><a name="TsqlExample"></a>진단 로그 옵션 설정  
 이 섹션의 예에서는 진단 로그 옵션 값을 설정하는 방법을 보여 줍니다.  
  
##### <a name="a-starting-diagnostic-logging"></a>A. 진단 로깅 시작  
 다음 예에서는 진단 데이터의 로깅을 시작합니다.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. 진단 로깅 중지  
 다음 예에서는 진단 데이터의 로깅을 중지합니다.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. 진단 로그의 위치 지정  
 다음 예에서는 진단 로그의 위치를 지정된 파일 경로로 설정합니다.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. 각 진단 로그의 최대 크기 지정  
 다음 예에서는 각 진단 로그의 최대 크기를 10MB로 설정합니다.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>참고 항목  
 [장애 조치 (Failover) 클러스터 인스턴스에 대 한 장애 조치 정책](failover-policy-for-failover-cluster-instances.md)  
  
  
