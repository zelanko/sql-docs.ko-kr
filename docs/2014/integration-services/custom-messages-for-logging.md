---
title: Custom Messages for Logging | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47a14ad3baf1660b2b60cd6b96f2ef51f1e5d727
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060085"
---
# <a name="custom-messages-for-logging"></a>로깅할 메시지 사용자 지정
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 패키지 및 여러 태스크에 대한 로그 항목 기록을 위해 다양한 사용자 지정 이벤트 집합을 제공합니다. 이러한 항목을 사용하면 나중에 분석할 수 있도록 미리 정의된 이벤트나 사용자가 정의한 메시지를 기록하여 실행 진행률, 결과 및 문제에 대한 세부 정보를 저장할 수 있습니다. 예를 들면 대량 삽입이 시작되고 끝나는 시간을 기록하여 패키지 실행 시 성능 문제를 식별할 수 있습니다.  
  
 사용자 지정 로그 항목은 패키지 및 모든 컨테이너와 태스크에 사용할 수 있는 표준 로깅 이벤트 집합과는 다른 항목 집합입니다. 사용자 지정 로그 항목은 패키지의 특정 태스크에 대한 유용한 정보를 캡처하도록 조정되어 있습니다. 예를 들어 SQL 실행 태스크에 대한 사용자 지정 로그 항목 중 하나는 해당 태스크에서 실행한 SQL 문을 로그에 기록합니다.  
  
 모든 로그 항목에는 패키지가 시작되고 끝날 때 자동으로 기록되는 로그 항목을 비롯하여 날짜 및 시간 정보가 포함됩니다. 로그 이벤트는 대부분 여러 항목을 로그에 기록합니다. 일반적으로 이벤트에 여러 단계가 있을 경우 이러한 기록이 수행됩니다. 예를 들어 `ExecuteSQLExecutingQuery` 로그 이벤트는 3개의 항목을 기록합니다. 즉, 태스크에서 데이터베이스에 대한 연결을 설정한 후, 태스크에서 SQL 문 준비를 시작한 후, SQL 문 실행이 완료된 후에 각각 하나씩의 항목을 기록합니다.  
  
 다음 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체에는 사용자 지정 로그 항목이 있습니다.  
  
 [패키지](#Package)  
  
 [대량 삽입 태스크](#BulkInsert)  
  
 [데이터 흐름 태스크](#DataFlow)  
  
 [DTS 2000 실행 태스크](#ExecuteDTS200)  
  
 [프로세스 실행 태스크](#ExecuteProcess)  
  
 [SQL 실행 태스크](#ExecuteSQL)  
  
 [파일 시스템 태스크](#FileSystem)  
  
 [FTP 태스크](#FTP)  
  
 [메시지 큐 태스크](#MessageQueue)  
  
 [스크립트 태스크](#Script)  
  
 [메일 보내기 태스크](#SendMail)  
  
 [데이터베이스 전송 태스크](#TransferDatabase)  
  
 [오류 메시지 전송 태스크](#TransferErrorMessages)  
  
 [작업 전송 태스크](#TransferJobs)  
  
 [로그인 전송 태스크](#TransferLogins)  
  
 [master 저장 프로시저 전송 태스크](#TransferMasterStoredProcedures)  
  
 [SQL Server 개체 전송 태스크](#TransferSQLServerObjects)  
  
 [웹 서비스 태스크](#WebServices)  
  
 [WMI 데이터 판독기 태스크](#WMIDataReader)  
  
 [WMI 이벤트 감시자 태스크](#WMIEventWatcher)  
  
 [XML 태스크](#XML)  
  
## <a name="log-entries"></a>로그 항목  
  
###  <a name="Package"></a> 패키지  
 다음 표에서는 패키지에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`PackageStart`|패키지 실행이 시작되었음을 나타냅니다.<br /><br /> 참고: 이 로그 항목은 로그에 자동으로 기록되며 제외할 수 없습니다.|  
|`PackageEnd`|패키지가 완료되었음을 나타냅니다.<br /><br /> 참고: 이 로그 항목은 로그에 자동으로 기록되며 제외할 수 없습니다.|  
|`Diagnostic`|동시에 실행될 수 있는 실행 파일 수처럼 패키지 실행에 영향을 주는 시스템 구성에 대한 정보를 제공합니다.<br /><br /> `Diagnostic` 로그 항목에는 외부 데이터 공급자에 대한 호출 전후 항목도 포함됩니다. 자세한 내용은 [패키지 연결 문제 해결 도구](troubleshooting/troubleshooting-tools-for-package-connectivity.md)을 참조하세요.|  
  
###  <a name="BulkInsert"></a> 대량 삽입 태스크  
 다음 표에서는 대량 삽입 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|대량 삽입이 시작되었음을 나타냅니다.|  
|`DTSBulkInsertTaskEnd`|대량 삽입이 완료되었음을 나타냅니다.|  
|`DTSBulkInsertTaskInfos`|태스크에 대한 설명 정보를 제공합니다.|  
  
###  <a name="DataFlow"></a> 데이터 흐름 태스크  
 다음 표에서는 데이터 흐름 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`BufferSizeTuning`|데이터 흐름 태스크로 인해 버퍼 크기가 변경되었음을 나타냅니다. 로그 항목은 크기가 변경된 이유를 설명하고 임시 새 버퍼 크기를 나열합니다.|  
|`OnPipelinePostEndOfRowset`|구성 요소에 `ProcessInput` 메서드의 마지막 호출로 설정된 해당 행 집합 끝 신호를 제공했음을 나타냅니다. 입력을 처리하는 데이터 흐름의 각 구성 요소에 대한 항목이 기록됩니다. 이 항목은 구성 요소의 이름을 포함합니다.|  
|`OnPipelinePostPrimeOutput`|구성 요소가 `PrimeOutput` 메서드에 대한 마지막 호출을 완료했음을 나타냅니다. 데이터 흐름에 따라 여러 로그 항목이 기록될 수 있습니다. 구성 요소가 원본일 경우에는 구성 요소가 행 처리를 완료했음을 의미합니다.|  
|`OnPipelinePreEndOfRowset`|구성 요소가 `ProcessInput` 메서드의 마지막 호출로 설정된 해당 행 집합 끝 신호를 수신하려고 함을 나타냅니다. 입력을 처리하는 데이터 흐름의 각 구성 요소에 대한 항목이 기록됩니다. 이 항목은 구성 요소의 이름을 포함합니다.|  
|`OnPipelinePrePrimeOutput`|구성 요소가 `PrimeOutput` 메서드에서 해당 호출을 수신하려고 함을 나타냅니다. 데이터 흐름에 따라 여러 로그 항목이 기록될 수 있습니다.|  
|`OnPipelineRowsSent`|`ProcessInput` 메서드 호출로 구성 요소 입력에 제공한 행 수를 보고합니다. 이 로그 항목은 구성 요소 이름을 포함합니다.|  
|`PipelineBufferLeak`|버퍼 관리자가 없어진 후에 버퍼를 활성 상태로 유지하는 모든 구성 요소에 대한 정보를 제공합니다. 즉, 버퍼 리소스가 릴리스되지 않았기 때문에 메모리 손실이 발생할 수 있음을 나타냅니다. 로그 항목은 구성 요소 이름과 버퍼 ID를 제공합니다.|  
|`PipelineExecutionPlan`|데이터 흐름의 실행 계획을 보고합니다. 버퍼를 구성 요소로 전송하는 방법에 대한 정보를 제공합니다. 이 정보는 PipelineExecutionTrees 항목과 함께 태스크에서 발생하는 사항에 대해 설명합니다.|  
|`PipelineExecutionTrees`|데이터 흐름에서 레이아웃 실행 트리를 보고합니다. 데이터 흐름 엔진 스케줄러는 이 트리를 사용하여 데이터 흐름의 실행 계획을 작성합니다.|  
|`PipelineInitialization`|태스크에 대한 초기화 정보를 제공합니다. 이 정보에 BLOB 데이터의 임시 스토리지에 사용할 디렉터리, 기본 버퍼 크기 및 버퍼의 행 수가 포함됩니다. 데이터 흐름 태스크의 구성에 따라 여러 로그 항목이 기록될 수 있습니다.|  
  
###  <a name="ExecuteDTS200"></a> DTS 2000 실행 태스크  
 다음 표에서는 DTS 2000 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|태스크에서 DTS 2000 패키지 실행을 시작했음을 나타냅니다.|  
|`ExecuteDTS80PackageTaskEnd`|태스크가 완료되었음을 나타냅니다.<br /><br /> 참고: DTS 2000 패키지는 태스크가 끝난 후에도 계속 실행됩니다.|  
|`ExecuteDTS80PackageTaskTaskInfo`|태스크에 대한 설명 정보를 제공합니다.|  
|`ExecuteDTS80PackageTaskTaskResult`|태스크에서 실행한 DTS 2000 패키지의 실행 결과를 보고합니다.|  
  
###  <a name="ExecuteProcess"></a> 프로세스 실행 태스크  
 다음 표에서는 프로세스 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|태스크에서 실행하도록 구성된 실행 파일의 실행 프로세스에 대한 정보를 제공합니다.<br /><br /> 두 개의 로그 항목이 기록됩니다. 한 항목에는 태스크가 실행하는 실행 파일의 이름과 위치에 대한 정보가 들어 있고 다른 항목은 실행 파일의 종료를 기록합니다.|  
|`ExecuteProcessVariableRouting`|실행 파일의 입력 및 출력으로 라우팅되는 변수에 대한 정보를 제공합니다. stdin(입력), stdout(출력) 및 stderr(오류 출력)에 대한 로그 항목이 기록됩니다.|  
  
###  <a name="ExecuteSQL"></a> SQL 실행 태스크  
 다음 표에서는 SQL 실행 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|SQL 문의 실행 단계에 대한 정보를 제공합니다. 로그 항목은 태스크에서 데이터베이스에 대한 연결을 설정할 때, 태스크에서 SQL 문 준비를 시작할 때 또는 SQL 문 실행이 완료된 후에 기록됩니다. 준비 단계에 대한 로그 항목은 태스크에서 사용하는 SQL 문을 포함합니다.|  
  
###  <a name="FileSystem"></a> 파일 시스템 태스크  
 다음 표에서는 파일 시스템 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`FileSystemOperation`|태스크에서 수행하는 작업을 보고합니다. 이 로그 항목은 파일 시스템 작업이 시작될 때 기록되며 원본 및 대상에 대한 정보를 포함합니다.|  
  
###  <a name="FTP"></a> FTP 태스크  
 다음 표에서는 FTP 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`FTPConnectingToServer`|태스크에서 FTP 서버에 대한 연결을 시작했음을 나타냅니다.|  
|`FTPOperation`|태스크에서 수행하는 FTP 작업의 시작 부분과 유형을 보고합니다.|  
  
###  <a name="MessageQueue"></a> 메시지 큐 태스크  
 다음 표에서는 메시지 큐 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`MSMQAfterOpen`|태스크에서 메시지 큐 열기를 완료했음을 나타냅니다.|  
|`MSMQBeforeOpen`|태스크에서 메시지 큐 열기를 시작했음을 나타냅니다.|  
|`MSMQBeginReceive`|태스크에서 메시지 받기를 시작했음을 나타냅니다.|  
|`MSMQBeginSend`|태스크에서 메시지 보내기를 시작했음을 나타냅니다.|  
|`MSMQEndReceive`|태스크에서 메시지 받기를 완료했음을 나타냅니다.|  
|`MSMQEndSend`|태스크에서 메시지 보내기를 완료했음을 나타냅니다.|  
|`MSMQTaskInfo`|태스크에 대한 설명 정보를 제공합니다.|  
|`MSMQTaskTimeOut`|태스크 시간이 초과되었음을 나타냅니다.|  
  
###  <a name="Script"></a> 스크립트 태스크  
 다음 표에서는 스크립트 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|스크립트에서 로깅을 구현한 결과를 보고합니다. `Log` 개체의 `Dts` 메서드 호출에 대해 각각 로그 항목이 기록됩니다. 이 항목은 코드가 실행되면 기록됩니다. 자세한 내용은 [Logging in the Script Task](extending-packages-scripting/task/logging-in-the-script-task.md)을(를) 참조하세요.|  
  
###  <a name="SendMail"></a> 메일 보내기 태스크  
 다음 표에서는 메일 보내기 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`SendMailTaskBegin`|태스크에서 전자 메일 메시지 보내기를 시작했음을 나타냅니다.|  
|`SendMailTaskEnd`|태스크에서 전자 메일 메시지 보내기를 완료했음을 나타냅니다.|  
|`SendMailTaskInfo`|태스크에 대한 설명 정보를 제공합니다.|  
  
###  <a name="TransferDatabase"></a> 데이터베이스 전송 태스크  
 다음 표에서는 데이터베이스 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`SourceDB`|태스크에서 복사한 데이터베이스를 지정합니다.|  
|`SourceSQLServer`|데이터베이스를 복사한 컴퓨터를 지정합니다.|  
  
###  <a name="TransferErrorMessages"></a> 오류 메시지 전송 태스크  
 다음 표에서는 오류 메시지 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|태스크에서 오류 메시지 전송을 완료했음을 나타냅니다.|  
|`TransferErrorMessagesTaskStartTransferringObjects`|태스크에서 오류 메시지 전송을 시작했음을 나타냅니다.|  
  
###  <a name="TransferJobs"></a> 작업 전송 태스크  
 다음 표에서는 작업 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 전송을 완료했음을 나타냅니다.|  
|`TransferJobsTaskStartTransferringObjects`|태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업 전송을 시작했음을 나타냅니다.|  
  
###  <a name="TransferLogins"></a> 로그인 전송 태스크  
 다음 표에서는 로그인 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|태스크에서 로그인 전송을 완료했음을 나타냅니다.|  
|`TransferLoginsTaskStartTransferringObjects`|태스크에서 로그인 전송을 시작했음을 나타냅니다.|  
  
###  <a name="TransferMasterStoredProcedures"></a> Master 저장 프로시저 전송 태스크  
 다음 표에서는 Master 저장 프로시저 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|태스크에서 **master** 데이터베이스에 저장된 사용자 정의 저장 프로시저 전송을 완료했음을 나타냅니다.|  
|`TransferStoredProceduresTaskStartTransferringObjects`|태스크에서 **master** 데이터베이스에 저장된 사용자 정의 저장 프로시저 전송을 시작했음을 나타냅니다.|  
  
###  <a name="TransferSQLServerObjects"></a> SQL Server 개체 전송 태스크  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 개체 전송을 완료했음을 나타냅니다.|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|태스크에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 개체 전송을 시작했음을 나타냅니다.|  
  
###  <a name="WebServices"></a> 웹 서비스 태스크  
 다음 표에서는 웹 서비스 태스크에 사용할 수 있는 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`WSTaskBegin`|태스크에서 웹 서비스 액세스를 시작했습니다.|  
|`WSTaskEnd`|태스크에서 웹 서비스 메서드를 완료했습니다.|  
|`WSTaskInfo`|태스크에 대한 설명 정보입니다.|  
  
###  <a name="WMIDataReader"></a> WMI 데이터 판독기 태스크  
 다음 표에서는 WMI 데이터 판독기 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|태스크에서 WMI 데이터 읽기를 시작했음을 나타냅니다.|  
|`WMIDataReaderOperation`|태스크에서 실행한 WQL 쿼리를 보고합니다.|  
  
###  <a name="WMIEventWatcher"></a> WMI 이벤트 감시자 태스크  
 다음 표에서는 WMI 이벤트 감시자 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|태스크에서 모니터링하고 있는 이벤트가 발생했음을 나타냅니다.|  
|`WMIEventWatcherTimedout`|태스크 시간이 초과되었음을 나타냅니다.|  
|`WMIEventWatcherWatchingForWMIEvents`|태스크에서 WQL 쿼리 실행을 시작했음을 나타냅니다. 이 항목은 해당 쿼리를 포함합니다.|  
  
###  <a name="XML"></a> XML 태스크  
 다음 표에서는 XML 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`XMLOperation`|태스크에서 수행한 작업에 대한 정보를 제공합니다.|  
  
## <a name="related-content"></a>관련 내용  
 dougbert.com의 블로그 항목 - [Integration Services 태스크에 대한 사용자 지정 이벤트 로깅](https://go.microsoft.com/fwlink/?LinkId=150580)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
