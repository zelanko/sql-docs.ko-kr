---
title: "샘플: WMI 공급자를 사용 하 여 SQL Server 에이전트 경고를 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2c108a7023cb66a82c5613063c039a5f34d6470
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="sample-creating-a-sql-server-agent-alert-with-the-wmi-provider"></a>샘플: WMI 공급자와 SQL Server 에이전트 경고 만들기
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
WMI 이벤트 공급자를 사용하는 일반적인 방법 중 하나는 특정 이벤트에 응답하는 SQL Server 에이전트 경고를 만드는 것입니다. 다음 예제에서는 XML 교착 상태 그래프 이벤트를 나중에 분석할 수 있도록 테이블에 저장하는 간단한 경고를 보여 줍니다. SQL Server 에이전트는 WQL 요청을 전송하고 WMI 이벤트를 수신하고 이벤트에 대한 응답으로 작업을 실행합니다. 알림 메시지 처리와 관련된 Service Broker 개체가 여러 개 있지만 WMI 이벤트 공급자가 이러한 개체의 생성 및 관리 세부 정보를 처리합니다.  
  
## <a name="example"></a>예제  
 먼저 교착 상태 그래프 이벤트를 저장할 `AdventureWorks` 데이터베이스에 테이블을 만듭니다. 테이블에 두 개의 열이:는 `AlertTime` 열 경고가 실행 되는 시간을 저장 및 `DeadlockGraph` 열에는 교착 상태 그래프가 포함 된 XML 문서가 들어 있습니다.  
  
 그런 다음 경고를 만듭니다. 스크립트에서는 경고에서 실행할 작업을 만들어 작업에 작업 단계를 추가하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스를 작업의 대상으로 지정합니다. 그런 후 스크립트에서는 경고를 만듭니다.  
  
 작업 단계를 검색는 **TextData** WMI 이벤트 인스턴스의 속성과 값에 삽입 된 **DeadlockGraph** 의 열은 **DeadlockEvents** 테이블입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 문자열을 XML 형식으로 암시적으로 변환합니다. 작업 단계에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 하위 시스템을 사용하기 때문에 프록시가 지정되지 않습니다.  
  
 경고는 교착 상태 그래프 추적 이벤트가 로깅될 때마다 작업을 실행합니다. WMI 경고에 대해 SQL Server 에이전트는 지정된 네임스페이스와 WQL 문을 사용하여 알림 쿼리를 만듭니다. 이 경고에 대해 SQL Server 에이전트는 로컬 컴퓨터에서 기본 인스턴스를 모니터링합니다. WQL 문은 기본 인스턴스에서 모든 `DEADLOCK_GRAPH` 이벤트를 요청합니다. 경고에서 모니터링하는 대상 인스턴스를 변경하려면 경고의 `MSSQLSERVER`에서 `@wmi_namespace`의 인스턴스 이름을 바꿉니다.  
  
> [!NOTE]  
>  WMI 이벤트를 수신 하도록 SQL Server 에이전트에 대 한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 사용할 수 있어야 **msdb** 및 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]합니다.  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>예제 테스트  
 작업이 실행되는 것을 확인하려면 교착 상태를 발생시켜야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 두 개의 열 **SQL 쿼리** 탭 하 고 두 쿼리 모두 동일한 인스턴스에 연결 합니다. 쿼리 탭 중 하나에서 다음 스크립트를 실행합니다. 이 스크립트는 하나의 결과 집합을 생성한 후 종료됩니다.  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 두 번째 쿼리 탭에서 다음 스크립트를 실행합니다. 이 스크립트는 하나의 결과 집합을 생성한 후 `Production.Product`에 대한 잠금을 얻기 위해 기다리는 동안 차단됩니다.  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 첫 번째 쿼리 탭에서 다음 스크립트를 실행합니다. 이 스크립트도 `Production.Location`에 대한 잠금을 얻기 위해 기다리는 동안 차단됩니다. 지정된 제한 시간이 초과되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 스크립트나 예제의 스크립트를 교착 상태로 처리한 후 트랜잭션을 종료합니다.  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 교착 상태를 발생시킨 후 SQL Server 에이전트가 경고를 활성화하고 작업을 실행할 때까지 잠시 기다립니다. 다음 스크립트를 실행하여 `DeadlockEvents` 테이블의 내용을 검사합니다.  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 `DeadlockGraph` 열에는 교착 상태 그래프 이벤트의 모든 속성을 보여 주는 XML 문서가 포함되어 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [서버 이벤트용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
