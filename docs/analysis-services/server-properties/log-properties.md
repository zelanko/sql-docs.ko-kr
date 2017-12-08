---
title: "로그 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 773aa4d93c8c6621184f8288964bd80d5efd826c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="log-properties"></a>로그 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 로그 서버 속성을 사용할 수 있습니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
## <a name="general"></a>일반  
 **파일**  
 서버 로그 파일의 이름을 식별하는 문자열 속성입니다. 이 속성은 데이터베이스 테이블과는 달리 디스크 파일이 로깅용으로 사용되는 경우에만 적용됩니다(기본 동작).  
  
 이 속성의 기본값은 msmdsrv.log입니다.  
  
 **FileBufferSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MessageLogs**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="error-log"></a>오류 로그  
 서버 인스턴스 수준에서 이러한 속성을 설정하여 다른 도구 및 디자이너에 나타나는 오류 구성에 대한 기본값을 수정할 수 있습니다. 참조 [큐브, 파티션 및 차원 처리 &#40;에 대 한 오류 구성 SSAS-다차원 데이터 &#41; ](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md) 및 <xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A> 자세한 정보에 대 한 합니다.  
  
 **ErrorLog\ErrorLogFileName**  
 서버가 수행한 작업을 처리하는 동안 속성이 기본값으로 사용되었습니다.  
  
 **ErrorLog\ErrorLogFileSize**  
 서버가 수행한 작업을 처리하는 동안 속성이 기본값으로 사용되었습니다.  
  
 **ErrorLog\KeyErrorAction**  
 **KeyNotFound** 오류가 발생하는 경우 서버에서 수행하는 동작을 지정합니다. 이 오류에 대한 유효한 응답은 다음과 같습니다.  
  
-   **ConvertToUnknown** 은 오류 키 값을 알 수 없는 멤버에 할당하도록 서버에 지시합니다.  
  
-   **DiscardRecord** 는 레코드를 제외하도록 서버에 지시합니다.  
  
 **ErrorLog\KeyErrorLogFile**  
 서비스 계정이 읽기-쓰기 권한을 가지고 있는 폴더에 있는 사용자 정의 파일 이름이며, 이 파일의 확장명은 .log여야 합니다. 이 로그 파일에는 처리 중에 생성된 오류만 포함됩니다. 보다 자세한 정보가 필요한 경우 비행 레코더를 사용하십시오.  
  
 **ErrorLog\KeyErrorLimit**  
 서버에서 처리를 중지하기 전에 허용할 데이터 무결성 오류의 최대 수입니다. -1 값은 제한이 없음을 나타냅니다. 기본값은 0이며 처음 오류가 발생한 후 처리가 중지됨을 의미합니다. 이 값을 정수로 설정할 수도 있습니다.  
  
 **ErrorLog\KeyErrorLimitAction**  
 키 오류 수가 상한에 도달한 경우 서버에서 수행하는 동작을 지정합니다. 이 동작에 대한 유효한 응답은 다음과 같습니다.  
  
-   **StopProcessing** 은 오류 제한에 도달하면 처리를 중지하도록 서버에 지시합니다.  
  
-   **StopLogging** 은 오류 제한에 도달하면 오류 기록을 중지하지만 처리가 계속되게 허용하도록 서버에 지시합니다.  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 **KeyNotFound** 오류가 발생하는 경우 서버에서 수행하는 동작을 지정합니다. 이 오류에 대한 유효한 응답은 다음과 같습니다.  
  
-   **IgnoreError** 는 오류를 기록하거나 키 오류 제한에 대해 오류 개수를 계산하지 않고 처리를 계속하도록 서버에 지시합니다. 오류를 무시하기만 하면 오류 개수에 추가하거나 화면 또는 로그 파일에 기록하지 않고 처리가 계속됩니다. 문제의 레코드에 데이터 무결성 문제가 있어서 데이터베이스에 레코드를 추가할 수 없습니다. 레코드는 **KeyErrorAction** 속성으로 결정된 대로 삭제되거나 알 수 없는 멤버에 집계됩니다.  
  
-   **ReportAndContinue** 는 오류를 기록하고, 키 오류 제한에 대해 오류 개수를 계산하고, 처리를 계속하도록 서버에 지시합니다. 오류를 발생시키는 레코드는 삭제되거나 알 수 없는 멤버로 변환됩니다.  
  
-   **ReportAndStop** 은 오류를 기록하고 키 오류 제한에 관계없이 처리를 즉시 중지하도록 서버에 지시합니다. 오류를 발생시키는 레코드는 삭제되거나 알 수 없는 멤버로 변환됩니다.  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 중복 키가 있을 때 서버가 수행하는 동작을 지정합니다. 유효한 값에는 오류가 발생하지 않은 것처럼 처리를 계속하는 **IgnoreError** , 오류를 기록하고 처리를 계속하는 **ReportAndContinue** , 오류를 기록하고 오류 개수가 오류 제한에 못 미치더라도 처리를 즉시 중지하는 **ReportAndStop** 이 포함됩니다.  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 null 키가 알 수 없는 멤버로 변환된 경우 서버에서 수행하는 동작을 지정합니다. 유효한 값에는 오류가 발생하지 않은 것처럼 처리를 계속하는 **IgnoreError** , 오류를 기록하고 처리를 계속하는 **ReportAndContinue** , 오류를 기록하고 오류 개수가 오류 제한에 못 미치더라도 처리를 즉시 중지하는 **ReportAndStop** 이 포함됩니다.  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 차원 특성에 대해 **NullProcessing** 이 **Error** 로 설정된 경우 서버에서 수행하는 동작을 지정합니다. null 값이 지정된 특성에서 허용되지 않는 경우 오류가 생성됩니다. 이 오류 구성 속성은 오류를 보고하고 오류 제한에 도달할 때까지 처리를 계속하는 다음 단계를 알려줍니다. 유효한 값에는 오류가 발생하지 않은 것처럼 처리를 계속하는 **IgnoreError** , 오류를 기록하고 처리를 계속하는 **ReportAndContinue** , 오류를 기록하고 오류 개수가 오류 제한에 못 미치더라도 처리를 즉시 중지하는 **ReportAndStop** 이 포함됩니다.  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 서버가 수행한 작업을 처리하는 동안 속성이 기본값으로 사용되었습니다.  
  
 **ErrorLog\IgnoreDataTruncation**  
 서버가 수행한 작업을 처리하는 동안 속성이 기본값으로 사용되었습니다.  
  
## <a name="exception"></a>예외  
 **Exception\CreateAndSendCrashReports**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Exception\CrashReportsFolder**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Exception\SQLDumperFlagsOn**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Exception\SQLDumperFlagsOff**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Exception\MiniDumpFlagsOn**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Exception\MinidumpErrorList**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="flight-recorder"></a>비행 레코더  
 **FlightRecorder\Enabled**  
 비행 레코더 기능이 설정되어 있는지 여부를 나타내는 부울 속성입니다.  
  
 **FlightRecorder\FileSizeMB**  
 비행 레코더 디스크 파일의 크기(MB)를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
 **FlightRecorder\LogDurationSec**  
 비행 레코더가 롤오버된 빈도(초)를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 스냅숏을 사용할 때 서버에 실행된 검색 명령을 포함하여 스냅숏 정의 파일의 이름을 정의하는 문자열 속성입니다.  
  
 이 속성의 기본값은 빈 문자열이며 이후 파일 이름 FlightRecorderSnapshotDef.xml이 기본값이 됩니다.  
  
 **FlightRecorder\SnapshotFrequencySec**  
 스냅숏 빈도(초)를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
 **FlightRecorder\TraceDefinitionFile**  
 비행 레코더 추적 정의 파일의 이름을 지정하는 문자열 속성입니다.  
  
 이 속성의 기본값은 빈 문자열이며 이후 FlightRecorderTraceDef.xml이 기본값이 됩니다.  
  
## <a name="query-log"></a>쿼리 로그  
 **적용 대상:** 다차원 서버 모드에만  
  
 **QueryLog\QueryLogFileName**  
 쿼리 로그 파일의 이름을 지정하는 문자열 속성입니다. 이 속성은 데이터베이스 테이블과는 달리 디스크 파일이 로깅용으로 사용되는 경우에만 적용됩니다(기본 동작).  
  
 **QueryLog\QueryLogSampling**  
 쿼리 로그 샘플링 비율을 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 10으로 서버 쿼리 10개마다 1개가 기록됩니다.  
  
 **QueryLog\QueryLogFileSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **QueryLog\QueryLogConnectionString**  
 쿼리 로그 데이터베이스에 대한 연결을 지정하는 문자열 속성입니다.  
  
 **QueryLog\QueryLogTableName**  
 쿼리 로그 테이블의 이름을 지정하는 문자열 속성입니다.  
  
 이 속성의 기본값은 OlapQueryLog입니다.  
  
 **QueryLog\CreateQueryLogTable**  
 쿼리 로그 테이블을 만들지 여부를 지정하는 부울 속성입니다.  
  
 이 속성의 기본값은 False로 서버가 로그 테이블을 자동으로 만들지 않고 쿼리 이벤트를 기록하지 않음을 나타냅니다.  
  
> [!NOTE]  
>  쿼리 로그 구성 방법에 대한 자세한 내용은 [Configuring the Analysis Services Query Log](http://go.microsoft.com/fwlink/?LinkId=81890)(Analysis Services 쿼리 로그 구성)를 참조하세요.  
  
## <a name="trace"></a>추적  
 **Trace\TraceBackgroundDistributionPeriod**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceBackgroundFlushPeriod**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceFileBufferSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceMaxRowsetSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceProtocolTraffic**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceReportFQDN**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceRequestParameters**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
