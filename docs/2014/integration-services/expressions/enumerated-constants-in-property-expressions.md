---
title: 속성 식의 열거 상수 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], expressions
- dynamic properties
- updating package properties
- enumerated constants [Integration Services]
- property expressions [Integration Services]
ms.assetid: a4418315-38e2-4ad3-8784-576163b25d6f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b22e25ad9053ed4da0187035cff00ff7e3ca70af
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386571"
---
# <a name="enumerated-constants-in-property-expressions"></a>속성 식의 열거 상수
  속성 식에 열거자 멤버 목록의 값이 포함된 경우 식에 멤버 이름 대신 열거자 멤버의 숫자 값을 사용해야 합니다. 예를 들어 식에 `LoggingMode` 속성을 설정한 경우 이름인 Disabled 대신 숫자 값 2를 사용해야 합니다.  
  
 이 항목에서는 해당 멤버가 속성 식에서 일반적으로 사용되는 열거자의 이름에 해당하는 숫자 값만 나열합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에는 프로그래밍 방식으로 패키지를 작성하거나 태스크 및 데이터 흐름 구성 요소와 같은 사용자 지정 패키지 요소를 코딩하기 위해 개체 모델을 프로그래밍할 때 사용하는 여러 개의 추가 열거자가 포함되어 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 속성 창에는 패키지 및 패키지 개체의 사용자 지정 속성 외에 패키지, 태스크 및 Foreach 루프, For 루프, 시퀀스 컨테이너에 사용할 수 있는 속성 집합이 포함되어 있습니다. 열거자-값으로 설정 된 공용 속성인`ForceExecutionResult`, `LoggingMode`를 `IsolationLevel`, 및 `Transaction Option`-공용 속성 섹션에 나열 됩니다.  
  
 다음 섹션에서는 열거 상수에 대한 정보를 제공합니다.  
  
 [패키지](#Package)  
  
 [Foreach 루프 열거자](#Foreach)  
  
 [작업](#Tasks)  
  
 [유지 관리 계획 태스크](#MaintenancePlanTasks)  
  
 [공용 속성](#CommonProperties)  
  
##  <a name="Package"></a> 패키지  
 다음 표에서는 열거자의 값을 사용하여 설정한 패키지 속성에 해당하는 숫자 값 및 이름을 보여 줍니다.  
  
 `PackageType` 값을 사용 하 여 속성 집합을 `DTSPackageType` 열거형입니다.  
  
|DTSPackageType의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|Default|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 `CheckpointUsage` 값을 사용 하 여 속성 집합을 `DTSCheckpointUsage` 열거형입니다.  
  
|DTSCheckpointUsage의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|안 함|0|  
|IfExists|1|  
|Always|2|  
  
 `PackagePriorityClass` 값을 사용 하 여 속성 집합을 `DTSPriorityClass` 열거형입니다.  
  
|DTSPriorityClass의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|Default|0|  
|AboveNormal|1|  
|보통|2|  
|BelowNormal|3|  
|Idle|4|  
  
 `ProtectionLevel` 값을 사용 하 여 속성 집합을 `DTSProtectionLevel` 열거형입니다.  
  
|DTSProtectionLevel의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="PrecedenceConstraints"></a> 선행 제약 조건  
 `EvalOp` 값을 사용 하 여 속성 집합을 `DTSPrecedenceEvalOp` 열거형입니다.  
  
|DTSPrecedenceEvalOp의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|식|1|  
|제약 조건|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 `Value` 값을 사용 하 여 속성 집합을 `DTSExecResult` 열거형입니다.  
  
|이름|숫자 값|  
|-------------------|-------------------|  
|성공|0|  
|실패|1|  
|Completion|2|  
|취소됨|3|  
  
##  <a name="Foreach"></a> Foreach 루프 열거자  
 Foreach 루프에는 속성 식으로 설정할 수 있는 속성을 가지는 열거자 집합이 포함되어 있습니다.  
  
### <a name="foreach-ado-enumerator"></a>Foreach ADO 열거자  
 `Type` 값을 사용 하 여 속성 집합을 `ADOEnumerationType` 열거형입니다.  
  
|ADOEnumerationType의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Foreach Nodelist 열거자  
 `SourceDocumentType``InnerXPathStringSourceType`, 및 **OuterXPathStringSourceType** 값을 사용 하 여 속성 집합을 `SourceType` 열거형입니다.  
  
|SourceType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
|DirectInput|2|  
  
 `EnumerationType` 값을 사용 하 여 속성 집합을 `EnumerationType` 열거형입니다.  
  
|EnumerationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|Navigator|0|  
|노드|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 `InnerElementType` 값을 사용 하 여 속성 집합을 `InnerElementType` 열거형입니다.  
  
|InnerElementType의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|Navigator|0|  
|노드|1|  
|NodeText|2|  
  
##  <a name="Tasks"></a> 작업  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 속성 식으로 설정할 수 있는 속성을 가지는 여러 태스크가 포함되어 있습니다.  
  
### <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크  
 `SourceType` 값을 사용 하 여 속성 집합을 `DDLSourceType` 열거형입니다.  
  
|DDLSourceType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|변수|2|  
  
### <a name="bulk-insert-task"></a>대량 삽입 태스크  
 `DataFileType` 값을 사용 하 여 속성 집합을 `DTSBulkInsert_DataFileType` 열거형입니다.  
  
|DTSBulkInsert_DataFileType의 이름|숫자 값|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>SQL 실행 태스크  
 `ResultSetType` 값을 사용 하 여 속성 집합을 `ResultSetType` 열거형입니다.  
  
|ResultSetType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 `SqlStatementSourceType` 값을 사용 하 여 속성 집합을 `SqlStatementSourceType` 열거형입니다.  
  
|SqlStatementSourceType의 이름|숫자 값|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|변수|3|  
  
### <a name="file-system-task"></a>파일 시스템 태스크  
 `Operation` 값을 사용 하 여 속성 집합을 `DTSFileSystemOperation` 열거형입니다.  
  
|DTSFileSystemOperation의 이름|숫자 값|  
|---------------------------------------------|-------------------|  
|CopyFile|0|  
|MoveFile|1|  
|DeleteFile|2|  
|RenameFile|3|  
|SetAttributes|4|  
|CreateDirectory|5|  
|CopyDirectory|6|  
|MoveDirectory|7|  
|DeleteDirectory|8|  
|DeleteDirectoryContent|9|  
  
 `Attributes` 값을 사용 하 여 속성 집합을 `DTSFileSystemAttributes` 열거형입니다.  
  
|DTSFileSystemAttributes의 이름|숫자 값|  
|----------------------------------------------|-------------------|  
|보통|0|  
|Archive|1|  
|숨김|2|  
|읽기 전용|4|  
|시스템|8|  
  
### <a name="ftp-task"></a>FTP 태스크  
 `Operation` 값을 사용 하 여 속성 집합을 `DTSFTPOp` 열거형입니다.  
  
|DTSFTPOp의 이름|숫자 값|  
|-------------------------------|-------------------|  
|Send|0|  
|받기|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 `MessageType` 값을 사용 하 여 속성 집합을 `MQMessageType` 열거형입니다.  
  
|MQMessageType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 `StringCompareType` 값을 사용 하 여 속성 집합을 `MQStringMessageCompare` 열거형입니다.  
  
|MQStringMessageCompare의 이름|숫자 값|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 `TaskType` 값을 사용 하 여 속성 집합을 `MQType` 열거형입니다.  
  
|MQType의 이름|숫자 값|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>메일 보내기 태스크  
 `MessageSourceType` 값을 사용 하 여 속성 집합을 `SendMailMessageSourceType` 열거형입니다.  
  
|SendMailMessageSourceType의 이름|숫자 값|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|변수|2|  
  
 `Priority` 값을 사용 하 여 속성 집합을 `MailPriority` 열거형입니다.  
  
|MailPriority의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|높음|1|  
|보통|3|  
|낮음|5|  
  
### <a name="transfer-database-task"></a>데이터베이스 전송 태스크  
 `Action` 값을 사용 하 여 속성 집합을 `TransferAction` 열거형입니다.  
  
|TransferAction의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|복사|0|  
|자세히 보기|1|  
  
 `Method` 값을 사용 하 여 속성 집합을 `TransferMethod` 열거형입니다.  
  
|TransferMethod의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>오류 메시지 전송 태스크  
 `IfObjectExists` 값을 사용 하 여 속성 집합을 `IfObjectExists` 열거형입니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>작업 전송 태스크  
 `IfObjectExists` 값을 사용 하 여 속성 집합을 `IfObjectExists` 열거형입니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>로그인 전송 태스크  
 `IfObjectExists` 값을 사용 하 여 속성 집합을 `IfObjectExists` 열거형입니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 `LoginsToTransfer` 값을 사용 하 여 속성 집합을 `LoginsToTransfer` 열거형입니다.  
  
|LoginsToTransfer의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Master 저장 프로시저 전송 태스크  
 `IfObjectExists` 값을 사용 하 여 속성 집합을 `IfObjectExists` 열거형입니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크  
 `ExistingData` 값을 사용 하 여 속성 집합을 `ExistingData` 열거형입니다.  
  
|ExistingData의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|바꾸기|0|  
|추가|1|  
  
### <a name="web-service-task"></a>웹 서비스 태스크  
 `OutputType` 값을 사용 하 여 속성 집합을 `DTSOutputType` 열거형입니다.  
  
|DTSOutputType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|파일|0|  
|변수|1|  
  
### <a name="wmi-data-reader-task"></a>WMI 데이터 판독기 태스크  
 `OverwriteDestination` 값을 사용 하 여 속성 집합을 `OverwriteDestination` 열거형입니다.  
  
|OverwriteDestination의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 `OutputType` 값을 사용 하 여 속성 집합을 `OutputType` 열거형입니다.  
  
|OutputType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 `DestinationType` 값을 사용 하 여 속성 집합을 `DestinationType` 열거형입니다.  
  
|DestinationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
  
 `WqlQuerySourceType` 값을 사용 하 여 속성 집합을 `QuerySourceType` 열거형입니다.  
  
|QuerySourceType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|변수|2|  
  
 WMI 이벤트 감시자 `ActionAtEvent` 값을 사용 하 여 속성 집합을 `ActionAtEvent` 열거형입니다.  
  
|ActionAtEvent의 이름|숫자 값|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 `ActionAtTimeout` 값을 사용 하 여 속성 집합을 `ActionAtTimeout` 열거형입니다.  
  
|ActionAtTimeout의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 `AfterEvent` 값을 사용 하 여 속성 집합을 `AfterEvent` 열거형입니다.  
  
|AfterEvent의 이름|숫자 값|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `AfterTimeout` 값을 사용 하 여 속성 집합을 `AfterTimeout` 열거형입니다.  
  
|AfterTimeout의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 `WqlQuerySourceType` 값을 사용 하 여 속성 집합을 `QuerySourceType` 열거형입니다.  
  
|QuerySourceType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|변수|2|  
  
### <a name="xml-task"></a>XML 태스크  
 `OperationType` 값을 사용 하 여 속성 집합을 `DTSXMLOperation` 열거형입니다.  
  
|DTSXMLOperation의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|유효성 검사|0|  
|XSLT|1|  
|XPATH|2|  
|병합|3|  
|Diff|4|  
|Patch|5|  
  
 `SourceType``SecondOperandType`, 및 `XPathSourceType` 값을 사용 하 여 속성 집합을 `DTSXMLSourceType` 열거형입니다.  
  
|DTSXMLSourceType의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
|DirectInput|2|  
  
 `DestinationType` 및 **DiffGramDestinationType** 값을 사용 하 여 속성 집합을 `DTSXMLSaveResultTo` 열거형입니다.  
  
|DTSXMLSaveResultTo의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
  
 `ValidationType` 값을 사용 하 여 속성 집합을 `DTSXMLValidationType` 열거형입니다.  
  
|DTSXMLValidationType의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 `XPathOperation` 값을 사용 하 여 속성 집합을 `DTSXMLXPathOperation` 열거형입니다.  
  
|DTSXMLXPathOperation의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|Evaluation|0|  
|값|1|  
|NodeList|2|  
  
 `DiffOptions` 값을 사용 하 여 속성 집합을 `DTSXMLDiffOptions` 열거형입니다. 이 열거자의 옵션은 함께 사용할 수 있습니다. 여러 옵션을 사용하려면 적용할 옵션의 목록을 쉼표로 구분하여 제공합니다.  
  
|DTSXMLDiffOptions의 이름|숫자 값|  
|----------------------------------------|-------------------|  
|없음|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 `DiffAlgorithm` 값을 사용 하 여 속성 집합을 `DTSXMLDiffAlgorithm` 열거형입니다.  
  
|DTSXMLDiffAlgorithm의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|자동|0|  
|빠름|1|  
|정확|2|  
  
##  <a name="MaintenancePlanTasks"></a> 유지 관리 계획 태스크  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 유지 관리 계획 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용할 SQL Server 태스크를 수행하는 태스크 집합이 포함되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이러한 태스크를 프로그래밍 방식으로 수행할 수 없으므로 프로그래밍 참조 설명서에 이러한 태스크 및 해당 열거자에 대한 API 설명서가 포함되지 않습니다.  
  
### <a name="all-maintenance-tasks"></a>모든 유지 관리 태스크  
 모든 유지 관리 태스크에서는 다음 열거를 사용하여 지정된 속성을 설정합니다.  
  
 `DatabaseSelectionType` 값을 사용 하 여 속성 집합을 `DatabaseSelection` 열거형입니다.  
  
|DatabaseSelection의 이름|숫자 값|  
|----------------------------------------|-------------------|  
|없음|0|  
|All|1|  
|시스템|2|  
|사용자|3|  
|Specific|4|  
  
 `TableSelectionType` 값을 사용 하 여 속성 집합을 `TableSelection` 열거형입니다.  
  
|TableSelection의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|없음|0|  
|All|1|  
|Specific|2|  
  
 `ObjectTypeSelection` 값을 사용 하 여 속성 집합을 `ObjectType` 열거형입니다.  
  
|ObjectType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|Table|0|  
|보기|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>데이터베이스 백업 태스크  
 `DestinationCreationType` 값을 사용 하 여 속성 집합을 `DestinationType` 열거형입니다.  
  
|DestinationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|자동|0|  
|수동|1|  
  
 `ExistingBackupsAction` 값을 사용 하 여 속성 집합을 `ActionForExistingBackups` 열거형입니다.  
  
|ActionForExistingBackups의 이름|숫자 값|  
|-----------------------------------------------|-------------------|  
|추가|0|  
|Overwrite|1|  
  
 `BackupAction` 값을 사용 하 여 속성 집합을 `BackupTaskType` 열거형입니다. 이 속성은 `BackupIsIncremental` 속성과 함께 사용하여 태스크가 수행하는 백업 유형을 정의합니다.  
  
|BackupTaskType의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|데이터베이스|0|  
|파일|1|  
|Log|2|  
  
 `BackupDevice` 값을 사용 하 여 속성 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `DeviceType` 열거형입니다.  
  
|DeviceType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Tape|1|  
|파일|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>유지 관리 정리 태스크  
 `FileTypeSelected` 값을 사용 하 여 속성 집합을 `FileType` 열거형입니다.  
  
|FileType의 이름|숫자 값|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 `OlderThanTimeUnitType` 값을 사용 하 여 속성 집합을 `TimeUnitType` 열거형입니다.  
  
|TimeUnitType의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|Day|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>통계 업데이트 태스크  
 `UpdateType` 값을 사용 하 여 속성 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) `StatisticsTarget` 열거형입니다.  
  
|StatisticsTarget의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|Column|1|  
|인덱스|2|  
|All|3|  
  
##  <a name="CommonProperties"></a> 공용 속성  
 패키지, 태스크, Foreach 루프 컨테이너, For 루프 컨테이너, 시퀀스 컨테이너에서는 다음 열거를 사용하여 지정된 속성을 설정할 수 있습니다.  
  
 `ForceExecutionResult` 값을 사용 하 여 속성 집합을 `DTSForcedExecResult` 열거형입니다.  
  
|DTSForcedExecResult의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|없음|-1|  
|성공|0|  
|실패|1|  
|Completion|2|  
  
 `IsolationLevel` .NET Framework에서 속성 집합 `IsolationLevel` 열거형입니다. 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink?LinkId=17313)의 .NET Framework 클래스 라이브러리(.NET Framework Class Library)를 참조하십시오.  
  
 `LoggingMode` 값을 사용 하 여 속성 집합을 `DTSLoggingMode` 열거형입니다.  
  
|DTSLoggingMode의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|설정|1|  
|사용 안 함|2|  
  
 `TransactionOption` 값을 사용 하 여 속성 집합을 `DTSTransactionOption` 열거형입니다.  
  
|DTSTransactionOption의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|지원됨|1|  
|필수|2|  
  
## <a name="related-tasks"></a>관련 작업  
 [속성 식 추가 또는 변경](add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>관련 항목  
 [패키지에서 속성 식 사용](use-property-expressions-in-packages.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)   
 [Integration Services 컨테이너](../control-flow/integration-services-containers.md)   
 [Integration Services 태스크](../control-flow/integration-services-tasks.md)   
 [선행 제약 조건](../control-flow/precedence-constraints.md)  
  
  
