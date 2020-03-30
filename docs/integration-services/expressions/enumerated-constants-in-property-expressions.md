---
title: 속성 식의 열거 상수 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38ba2374821505dc3541ea05e76fd8aaecdcb5fc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297633"
---
# <a name="enumerated-constants-in-property-expressions"></a>속성 식의 열거 상수

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  속성 식에 열거자 멤버 목록의 값이 포함된 경우 식에 멤버 이름 대신 열거자 멤버의 숫자 값을 사용해야 합니다. 예를 들어 식에 **LoggingMode** 속성을 설정한 경우 이름인 Disabled 대신 숫자 값 2를 사용해야 합니다.  
  
 이 항목에서는 해당 멤버가 속성 식에서 일반적으로 사용되는 열거자의 이름에 해당하는 숫자 값만 나열합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에는 프로그래밍 방식으로 패키지를 작성하거나 태스크 및 데이터 흐름 구성 요소와 같은 사용자 지정 패키지 요소를 코딩하기 위해 개체 모델을 프로그래밍할 때 사용하는 여러 개의 추가 열거자가 포함되어 있습니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 속성 창에는 패키지 및 패키지 개체의 사용자 지정 속성 외에 패키지, 태스크 및 Foreach 루프, For 루프, 시퀀스 컨테이너에 사용할 수 있는 속성 집합이 포함되어 있습니다. 열거자의 값으로 설정된 공용 속성인 **ForceExecutionResult**, **LoggingMode**, **IsolationLevel** 및 **Transaction Option**은 공용 속성 섹션에 나열됩니다.  
  
 다음 섹션에서는 열거 상수에 대한 정보를 제공합니다.  
  
 [패키지](#Package)  
  
 [Foreach 루프 열거자](#Foreach)  
  
 [작업](#Tasks)  
  
 [유지 관리 계획 태스크](#MaintenancePlanTasks)  
  
 [Common Properties](#CommonProperties)  
  
##  <a name="package"></a><a name="Package"></a> 패키지  
 다음 표에서는 열거자의 값을 사용하여 설정한 패키지 속성에 해당하는 숫자 값 및 이름을 보여 줍니다.  
  
 **PackageType** 속성 - **DTSPackageType** 열거 값을 사용하여 설정합니다.  
  
|DTSPackageType의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|기본값|0|  
|DTSWizard|1|  
|DTSDesigner|2|  
|SQLReplication|3|  
|DTSDesigner100|5|  
|SQLDBMaint|6|  
  
 **CheckpointUsage** 속성 - **DTSCheckpointUsage** 열거 값을 사용하여 설정합니다.  
  
|DTSCheckpointUsage의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|안 함|0|  
|IfExists|1|  
|항상|2|  
  
 **PackagePriorityClass** 속성 - **DTSPriorityClass** 열거 값을 사용하여 설정합니다.  
  
|DTSPriorityClass의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|기본값|0|  
|AboveNormal|1|  
|정상|2|  
|BelowNormal|3|  
|유휴 상태|4|  
  
 **ProtectionLevel** 속성 - **DTSProtectionLevel** 열거 값을 사용하여 설정합니다.  
  
|DTSProtectionLevel의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|DontSaveSensitive|0|  
|EncryptSensitiveWithUserKey|1|  
|EncryptSensitiveWithPassword|2|  
|EncryptAllWithPassword|3|  
|EncryptAllWithUserKey|4|  
|ServerStorage|5|  
  
##  <a name="precedence-constraints"></a><a name="PrecedenceConstraints"></a> 선행 제약 조건  
 **EvalOp** 속성 - **DTSPrecedenceEvalOp** 열거 값을 사용하여 설정합니다.  
  
|DTSPrecedenceEvalOp의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|식|1|  
|제약 조건|2|  
|ExpressionAndConstraint|3|  
|ExpressionOrConstraint|4|  
  
 **Value** 속성 - **DTSExecResult** 열거 값을 사용하여 설정합니다.  
  
|친숙한 이름|숫자 값|  
|-------------------|-------------------|  
|Success|0|  
|실패|1|  
|Completion|2|  
|취소됨|3|  
  
##  <a name="foreach-loop-enumerators"></a><a name="Foreach"></a> Foreach 루프 열거자  
 Foreach 루프에는 속성 식으로 설정할 수 있는 속성을 가지는 열거자 집합이 포함되어 있습니다.  
  
### <a name="foreach-ado-enumerator"></a>Foreach ADO 열거자  
 **Type** 속성 - **ADOEnumerationType** 열거 값을 사용하여 설정합니다.  
  
|ADOEnumerationType의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|EnumerateTables|0|  
|EnumerateAllRows|1|  
|EnumerateRowsInFirstTable|2|  
  
### <a name="foreach-nodelist-enumerator"></a>Foreach Nodelist 열거자  
 **SourceDocumentType**, **InnerXPathStringSourceType** 및 **OuterXPathStringSourceType** 속성 - **SourceType** 열거 값을 사용하여 설정합니다.  
  
|SourceType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
|DirectInput|2|  
  
 **EnumerationType** 속성 - **EnumerationType** 열거 값을 사용하여 설정합니다.  
  
|EnumerationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|탐색기|0|  
|노드|1|  
|NodeText|2|  
|ElementCollection|3|  
  
 **InnerElementType** 속성 - **InnerElementType** 열거 값을 사용하여 설정합니다.  
  
|InnerElementType의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|탐색기|0|  
|노드|1|  
|NodeText|2|  
  
##  <a name="tasks"></a><a name="Tasks"></a> 작업  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 속성 식으로 설정할 수 있는 속성을 가지는 여러 태스크가 포함되어 있습니다.  
  
### <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크  
 **SourceType** 속성 - **DDLSourceType** 열거 값을 사용하여 설정합니다.  
  
|DDLSourceType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|변수|2|  
  
### <a name="bulk-insert-task"></a>대량 삽입 태스크  
 **DataFileType** 속성— **DTSBulkInsert_DataFileType** 열거 값을 사용하여 설정합니다.  
  
|DTSBulkInsert_DataFileType의 이름|숫자 값|  
|--------------------------------------------------|-------------------|  
|DTSBulkInsert_DataFileType_Char|0|  
|DTSBulkInsert_DataFileType_Native|1|  
|DTSBulkInsert_DataFileType_WideChar|2|  
|DTSBulkInsert_DataFileType_WideNative|3|  
  
### <a name="execute-sql-task"></a>SQL 실행 태스크  
 **ResultSetType** 속성 - **ResultSetType** 열거 값을 사용하여 설정합니다.  
  
|ResultSetType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|ResultSetType_None|1|  
|ResultSetType_SingleRow|2|  
|ResultSetType_Rowset|3|  
|ResultSetType_XML|4|  
  
 **SqlStatementSourceType** 속성 - **SqlStatementSourceType** 열거 값을 사용하여 설정합니다.  
  
|SqlStatementSourceType의 이름|숫자 값|  
|---------------------------------------------|-------------------|  
|DirectInput|1|  
|FileConnection|2|  
|변수|3|  
  
### <a name="file-system-task"></a>파일 시스템 태스크  
 **Operation** 속성 - **DTSFileSystemOperation** 열거 값을 사용하여 설정합니다.  
  
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
  
 **Attributes** 속성 - **DTSFileSystemAttributes** 열거 값을 사용하여 설정합니다.  
  
|DTSFileSystemAttributes의 이름|숫자 값|  
|----------------------------------------------|-------------------|  
|정상|0|  
|보관|1|  
|숨김|2|  
|ReadOnly|4|  
|시스템|8|  
  
### <a name="ftp-task"></a>FTP 태스크  
 **Operation** 속성 - **DTSFTPOp** 열거 값을 사용하여 설정합니다.  
  
|DTSFTPOp의 이름|숫자 값|  
|-------------------------------|-------------------|  
|보내기|0|  
|수신|1|  
|DeleteLocal|2|  
|DeleteRemote|3|  
|MakeDirLocal|4|  
|MakeDirRemote|5|  
|RemoveDirLocal|6|  
|RemoveDirRemote|7|  
  
### <a name="message-queue-task"></a>Message Queue Task  
 **MessageType** 속성 - **MQMessageType** 열거 값을 사용하여 설정합니다.  
  
|MQMessageType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|DTSMQMessageType_String|0|  
|DTSMQMessageType_DataFile|1|  
|DTSMQMessageType_Variables|2|  
|DTSMQMessagType_StringMessageToVariable|3|  
  
 **StringCompareType** 속성 - **MQStringMessageCompare** 열거 값을 사용하여 설정합니다.  
  
|MQStringMessageCompare의 이름|숫자 값|  
|---------------------------------------------|-------------------|  
|DTSMQStringMessageCompare_None|0|  
|DTSMQStringMessageCompare_Exact|1|  
|DTSMQStringMessageCompare_IgnoreCase|2|  
|DTSMQStringMessageCompare_Contains|3|  
  
 **TaskType** 속성 - **MQType** 열거 값을 사용하여 설정합니다.  
  
|MQType의 이름|숫자 값|  
|-----------------------------|-------------------|  
|DTSMQType_Sender|0|  
|DTSMQType_Receiver|1|  
  
### <a name="send-mail-task"></a>메일 보내기 태스크  
 **MessageSourceType** 속성 - **SendMailMessageSourceType** 열거 값을 사용하여 설정합니다.  
  
|SendMailMessageSourceType의 이름|숫자 값|  
|------------------------------------------------|-------------------|  
|DirectInput|0|  
|FileConnection|1|  
|변수|2|  
  
 **Priority** 속성 - **MailPriority** 열거 값을 사용하여 설정합니다.  
  
|MailPriority의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|높음|1|  
|정상|3|  
|낮음|5|  
  
### <a name="transfer-database-task"></a>데이터베이스 전송 태스크  
 **Action** 속성 - **TransferAction** 열거 값을 사용하여 설정합니다.  
  
|TransferAction의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|복사|0|  
|이동|1|  
  
 **Method** 속성 - **TransferMethod** 열거 값을 사용하여 설정합니다.  
  
|TransferMethod의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|DatabaseOffline|0|  
|DatabaseOnline|1|  
  
### <a name="transfer-error-messages-task"></a>오류 메시지 전송 태스크  
 **IfObjectExists** 속성 - **IfObjectExists** 열거 값을 사용하여 설정합니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-jobs-task"></a>작업 전송 태스크  
 **IfObjectExists** 속성 - **IfObjectExists** 열거 값을 사용하여 설정합니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-logins-task"></a>로그인 전송 태스크  
 **IfObjectExists** 속성 - **IfObjectExists** 열거 값을 사용하여 설정합니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
 **LoginsToTransfer** 속성 - **LoginsToTransfer** 열거 값을 사용하여 설정합니다.  
  
|LoginsToTransfer의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|AllLogins|0|  
|SelectedLogins|1|  
|AllLoginsFromSelectedDatabases|2|  
  
### <a name="transfer-master-stored-procedures-task"></a>Master 저장 프로시저 전송 태스크  
 **IfObjectExists** 속성 - **IfObjectExists** 열거 값을 사용하여 설정합니다.  
  
|IfObjectExists의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|FailTask|0|  
|Overwrite|1|  
|Skip|2|  
  
### <a name="transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크  
 **ExistingData** 속성 - **ExistingData** 열거 값을 사용하여 설정합니다.  
  
|ExistingData의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|Replace|0|  
|추가|1|  
  
### <a name="web-service-task"></a>웹 서비스 태스크  
 **OutputType** 속성 - **DTSOutputType** 열거 값을 사용하여 설정합니다.  
  
|DTSOutputType의 이름|숫자 값|  
|------------------------------------|-------------------|  
|파일|0|  
|변수|1|  
  
### <a name="wmi-data-reader-task"></a>WMI 데이터 판독기 태스크  
 **OverwriteDestination** 속성 - **OverwriteDestination** 열거 값을 사용하여 설정합니다.  
  
|OverwriteDestination의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|OverwriteDestination|0|  
|AppendToDestination|1|  
|KeepOriginal|2|  
  
 **OutputType** 속성 - **OutputType** 열거 값을 사용하여 설정합니다.  
  
|OutputType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|DataTable|0|  
|PropertyValue|1|  
|PropertyNameAndValue|2|  
  
 **DestinationType** 속성 - **DestinationType** 열거 값을 사용하여 설정합니다.  
  
|DestinationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
  
 **WqlQuerySourceType** 속성 - **QuerySourceType** 열거 값을 사용하여 설정합니다.  
  
|QuerySourceType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|변수|2|  
  
 WMI 이벤트 감시자 **ActionAtEvent** 속성 - **ActionAtEvent** 열거 값을 사용하여 설정합니다.  
  
|ActionAtEvent의 이름|숫자 값|  
|------------------------------------|-------------------|  
|LogTheEventAndFireDTSEvent|0|  
|LogTheEvent|1|  
  
 **ActionAtTimeout** 속성 - **ActionAtTimeout** 열거 값을 사용하여 설정합니다.  
  
|ActionAtTimeout의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|LogTimeoutAndFireDTSEvent|0|  
|LogTimeout|1|  
  
 **AfterEvent** 속성 - **AfterEvent** 열거 값을 사용하여 설정합니다.  
  
|AfterEvent의 이름|숫자 값|  
|---------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 **AfterTimeout** 속성 - **AfterTimeout** 열거 값을 사용하여 설정합니다.  
  
|AfterTimeout의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|ReturnWithSuccess|0|  
|ReturnWithFailure|1|  
|WatchfortheEventAgain|2|  
  
 **WqlQuerySourceType** 속성 - **QuerySourceType** 열거 값을 사용하여 설정합니다.  
  
|QuerySourceType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|FileConnection|0|  
|DirectInput|1|  
|변수|2|  
  
### <a name="xml-task"></a>XML 태스크  
 **OperationType** 속성 - **DTSXMLOperation** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLOperation의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|유효성 검사|0|  
|XSLT|1|  
|XPATH|2|  
|병합|3|  
|Diff|4|  
|패치|5|  
  
 **SourceType**, **SecondOperandType** 및 **XPathSourceType** 속성 - **DTSXMLSourceType** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLSourceType의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
|DirectInput|2|  
  
 **DestinationType** 및 **DiffGramDestinationType** 속성 - **DTSXMLSaveResultTo** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLSaveResultTo의 이름|숫자 값|  
|-----------------------------------------|-------------------|  
|FileConnection|0|  
|변수|1|  
  
 **ValidationType** 속성 - **DTSXMLValidationType** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLValidationType의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|DTD|0|  
|XSD|1|  
  
 **XPathOperation** 속성 - **DTSXMLXPathOperation** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLXPathOperation의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|평가|0|  
|값|1|  
|NodeList|2|  
  
 **DiffOptions** 속성 - **DTSXMLDiffOptions** 열거 값을 사용하여 설정합니다. 이 열거자의 옵션은 함께 사용할 수 있습니다. 여러 옵션을 사용하려면 적용할 옵션의 목록을 쉼표로 구분하여 제공합니다.  
  
|DTSXMLDiffOptions의 이름|숫자 값|  
|----------------------------------------|-------------------|  
|None|0|  
|IgnoreChildOrder|1|  
|IgnoreComments|2|  
|IgnorePI|4|  
|IgnoreWhitespace|8|  
|IgnoreNamespaces|16|  
|IgnorePrefixes|32|  
|IgnoreXmlDecl|64|  
|IgnoreDtd|128|  
  
 **DiffAlgorithm** 속성 - **DTSXMLDiffAlgorithm** 열거 값을 사용하여 설정합니다.  
  
|DTSXMLDiffAlgorithm의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|Auto|0|  
|빠름|1|  
|정확|2|  
  
##  <a name="maintenance-plan-tasks"></a><a name="MaintenancePlanTasks"></a> 유지 관리 계획 태스크  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 유지 관리 계획 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용할 SQL Server 태스크를 수행하는 태스크 집합이 포함되어 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이러한 태스크를 프로그래밍 방식으로 수행할 수 없으므로 프로그래밍 참조 설명서에 이러한 태스크 및 해당 열거자에 대한 API 설명서가 포함되지 않습니다.  
  
### <a name="all-maintenance-tasks"></a>모든 유지 관리 태스크  
 모든 유지 관리 태스크에서는 다음 열거를 사용하여 지정된 속성을 설정합니다.  
  
 **DatabaseSelectionType** 속성 - **DatabaseSelection** 열거 값을 사용하여 설정합니다.  
  
|DatabaseSelection의 이름|숫자 값|  
|----------------------------------------|-------------------|  
|None|0|  
|모두|1|  
|시스템|2|  
|사용자|3|  
|특정|4|  
  
 **TableSelectionType** 속성 - **TableSelection** 열거 값을 사용하여 설정합니다.  
  
|TableSelection의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|None|0|  
|모두|1|  
|특정|2|  
  
 **ObjectTypeSelection** 속성 - **ObjectType** 열거 값을 사용하여 설정합니다.  
  
|ObjectType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|테이블|0|  
|보기|1|  
|TableView|2|  
  
### <a name="back-up-database-task"></a>데이터베이스 백업 태스크  
 **DestinationCreationType** 속성 - **DestinationType** 열거 값을 사용하여 설정합니다.  
  
|DestinationType의 이름|숫자 값|  
|--------------------------------------|-------------------|  
|Auto|0|  
|설명서|1|  
  
 **ExistingBackupsAction** 속성 - **ActionForExistingBackups** 열거 값을 사용하여 설정합니다.  
  
|ActionForExistingBackups의 이름|숫자 값|  
|-----------------------------------------------|-------------------|  
|추가|0|  
|Overwrite|1|  
  
 **BackupAction** 속성 - **BackupTaskType** 열거 값을 사용하여 설정합니다. 이 속성은 **BackupIsIncremental** 속성과 함께 사용하여 태스크가 수행하는 백업 유형을 정의합니다.  
  
|BackupTaskType의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|데이터베이스|0|  
|파일|1|  
|로그|2|  
  
 **BackupDevice** 속성 - SMO([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) **DeviceType** 열거 값을 사용하여 설정합니다.  
  
|DeviceType의 이름|숫자 값|  
|---------------------------------|-------------------|  
|LogicalDevice|0|  
|Tape|1|  
|파일|2|  
|Pipe|3|  
|VirtualDevice|4|  
  
### <a name="maintenance-cleanup-task"></a>유지 관리 정리 태스크  
 **FileTypeSelected** 속성 - **FileType** 열거 값을 사용하여 설정합니다.  
  
|FileType의 이름|숫자 값|  
|-------------------------------|-------------------|  
|FileBackup|0|  
|FileReport|1|  
  
 **OlderThanTimeUnitType** 속성 - **TimeUnitType** 열거 값을 사용하여 설정합니다.  
  
|TimeUnitType의 이름|숫자 값|  
|-----------------------------------|-------------------|  
|일|0|  
|Week|1|  
|Month|2|  
|Year|3|  
  
### <a name="update-statistics-task"></a>통계 업데이트 태스크  
 **UpdateType** 속성 - SMO([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) **StatisticsTarget** 열거 값을 사용하여 설정합니다.  
  
|StatisticsTarget의 이름|숫자 값|  
|---------------------------------------|-------------------|  
|열|1|  
|인덱스|2|  
|모두|3|  
  
##  <a name="common-properties"></a><a name="CommonProperties"></a> 공용 속성  
 패키지, 태스크, Foreach 루프 컨테이너, For 루프 컨테이너, 시퀀스 컨테이너에서는 다음 열거를 사용하여 지정된 속성을 설정할 수 있습니다.  
  
 **ForceExecutionResult** 속성 - **DTSForcedExecResult** 열거 값을 사용하여 설정합니다.  
  
|DTSForcedExecResult의 이름|숫자 값|  
|------------------------------------------|-------------------|  
|None|-1|  
|Success|0|  
|실패|1|  
|Completion|2|  
  
 **IsolationLevel** 속성 - .NET Framework **IsolationLevel** 열거를 사용하여 설정합니다. 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink?LinkId=17313)의 .NET Framework 클래스 라이브러리(.NET Framework Class Library)를 참조하십시오.  
  
 **LoggingMode** 속성 - **DTSLoggingMode** 열거 값을 사용하여 설정합니다.  
  
|DTSLoggingMode의 이름|숫자 값|  
|-------------------------------------|-------------------|  
|UseParentSetting|0|  
|사용|1|  
|사용 안 함|2|  
  
 **TransactionOption** 속성 - **DTSTransactionOption** 열거 값을 사용하여 설정합니다.  
  
|DTSTransactionOption의 이름|숫자 값|  
|-------------------------------------------|-------------------|  
|NotSupported|0|  
|지원됨|1|  
|필수|2|  
  
## <a name="related-tasks"></a>관련 작업  
 [속성 식 추가 또는 변경](../../integration-services/expressions/add-or-change-a-property-expression.md)  
  
## <a name="see-also"></a>참고 항목  
 [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../../integration-services/integration-services-ssis-packages.md)   
 [Integration Services 컨테이너](../../integration-services/control-flow/integration-services-containers.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [선행 제약 조건](../../integration-services/control-flow/precedence-constraints.md)  
  
  
