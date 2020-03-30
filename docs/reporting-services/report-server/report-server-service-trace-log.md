---
title: 보고서 서버 서비스 추적 로그
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 04/23/2019
ms.openlocfilehash: 667f18f449a1f2564c04a03ca593c917a7b46005
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68254863"
---
# <a name="report-server-service-trace-log"></a>보고서 서버 서비스 추적 로그

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 추적 로그는 보고서 서버 서비스 작업에 대한 세부 정보가 들어 있는 ASCII 텍스트 파일입니다.  파일의 정보에는 보고서 서버 웹 서비스, 웹 포털 및 백그라운드 처리가 수행하는 작업이 포함됩니다. 추적 로그 파일에는 다른 로그 파일에 기록되는 중복된 정보와 다른 방법으로는 사용할 수 없는 추가 정보가 들어 있습니다. 추적 로그 정보는 보고서 서버가 포함된 애플리케이션을 디버깅하거나 이벤트 로그 또는 실행 로그에 기록된 특정 문제를 조사하는 경우에 유용합니다. 예를 들어 구독 문제를 해결하는 경우 등입니다.  

## <a name="where-are-the-report-server-log-files"></a><a name="bkmk_view_log"></a> 보고서 서버 로그 파일은 어디에 있나요?

추적 로그 파일은 `ReportServerService_<timestamp>.log` 및 `Microsoft.ReportingServices.Portal.WebHost_<timestamp>.log`이며 다음 폴더에 있습니다.

`C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles` 

추적 로그는 현지 시간으로 자정 후와 서비스가 다시 시작될 때마다 발생하는 첫 번째 항목을 시작으로 매일 만들어집니다. 타임스탬프는 UTC(Coordinated Universal Time)를 기반으로 합니다. 파일은 EN-US 형식이며 기본적으로 추적 로그는 32MB로 제한되며 기본적으로 14일 후 삭제됩니다.  

## <a name="trace-configuration-settings"></a><a name="bkmk_trace_configuration_settings"></a> 추적 구성 설정

추적 로그 동작은 구성 파일 **ReportingServicesService.exe.config**에서 관리됩니다. 구성 파일은 다음 폴더 경로에 있습니다.  
  
 `\Program Files\Microsoft SQL Server\MSRS13.<instance name>\Reporting Services\ReportServer\bin`입니다.  
  
 다음 예에서는 **RStrace** 설정의 XML 구조를 보여 줍니다. **DefaultTraceSwitch** 값에 따라 로그에 추가되는 정보의 종류가 결정됩니다. **Components** 특성을 제외하고 **RStrace** 값은 구성 파일 전반에서 모두 동일합니다.  
  
```
  \<system.diagnostics>
    <switches>
      <add name="DefaultTraceSwitch" value="3" />
    </switches>
  \</system.diagnostics>
  <RStrace>
    <add name="FileName" value="ReportServerService_" />
    <add name="FileSizeLimitMb" value="32" />
    <add name="KeepFilesForDays" value="14" />
    <add name="Prefix" value="appdomain, tid, time" />
    <add name="TraceListeners" value="file" />
    <add name="TraceFileMode" value="unique" />
    <add name="Components" value="all:3" />
  </RStrace>
```  
  
 다음 표에서는 각 설정에 대한 정보를 제공합니다.  
  
|설정|Description|값|  
|-------------|-----------------|------------|  
|**RStrace**|오류 및 추적에 사용되는 네임스페이스를 지정합니다.||  
|**DefaultTraceSwitch**|ReportServerService 추적 로그에 보고되는 정보의 수준을 지정합니다. 각 수준에는 낮은 번호가 매겨진 모든 수준별로 보고된 정보가 들어 있습니다. 추적을 설정하는 것이 좋습니다.|유효한 값은 다음과 같습니다.<br /><br /> <br /><br /> 0= 추적 해제. ReportServerService 로그 파일은 기본적으로 설정됩니다. 해제하려면, 추적 수준을 0으로 설정합니다.<br /><br /> 1= 예외 및 다시 시작<br /><br /> 2= 예외, 다시 시작, 경고<br /><br /> 3= 예외, 다시 시작, 경고, 상태 메시지(기본값)<br /><br /> 4= 세부 정보 표시 모드|  
|**FileName**|로그 파일 이름의 첫 번째 부분을 지정합니다. **Prefix** 에 지정된 값으로 이름의 나머지 부분을 완성합니다.||  
|**FileSizeLimitMb**|추적 로그 크기에 대한 상한값을 지정합니다. 파일은 메가바이트(MB) 단위로 측정됩니다.<br /><br /> 추적 수준(0-4)을 설정하여 파일 크기를 제어하면 기록되는 내용의 양을 제어할 수 있습니다. 추적할 구성 요소를 지정할 수도 있습니다. 만료일 14일 전에 로그 파일 최댓값에 도달하는 경우 이전 항목이 새 항목으로 바뀝니다.|유효한 값은 0에서 최대 정수 사이입니다. 기본값은 32입니다. 0이나 음수를 지정하면 보고서 서버에서 해당 값을 1로 처리합니다.|  
|**KeepFilesForDays**|추적 로그 파일을 몇 일 후에 삭제할지 지정합니다.|유효한 값은 0에서 최대 정수 사이입니다. 기본값은 14입니다. 0이나 음수를 지정하면 보고서 서버에서 해당 값을 1로 처리합니다.|  
|**Prefix**|하나의 로그 인스턴스를 다른 인스턴스와 구분하는 생성된 값을 지정합니다.|기본적으로 타임스탬프 값이 추적 로그 파일 이름에 추가됩니다. 이 값은 "appdomain, tid, time"으로 설정됩니다. 이 설정은 수정하지 마세요.|  
|**TraceListeners**|추적 로그 내용을 출력할 대상을 지정합니다. 대상이 여러 개일 경우 쉼표로 구분하여 지정할 수 있습니다.|유효한 값은 다음과 같습니다.<br /><br /> <br /><br /> DebugWindow<br /><br /> File(기본값)<br /><br /> StdOut|  
|**TraceFileMode**|추적 로그에 24시간 동안의 데이터를 포함할지 여부를 지정합니다. 일별로 각 구성 요소마다 고유한 추적 로그가 하나씩 있어야 합니다.|이 값은 "Unique(기본값)"로 설정됩니다. 이 값은 수정하지 마세요.|  
|**구성 요소 범주**|추적 로그 정보가 생성되는 구성 요소와 추적 수준을 다음 형식으로 지정합니다.<br /><br /> \<구성 요소 범주 >:\<tracelevel ><br /><br /> 구성 요소를 모두 또는 일부 지정할 수 있습니다(**all**, **RunningJobs**, **SemanticQueryEngine**, **SemanticModelGenerator**). 특정 구성 요소에 대해 정보를 생성하지 않으려면 "SemanticModelGenerator:0"과 같이 해당 구성 요소에 대해 추적을 해제합니다. **all**에 대한 추적은 해제하지 마세요.<br /><br /> 각 의미 체계 쿼리에 대해 생성되는 Transact-SQL 문을 보려면 "SemanticQueryEngine:4"를 설정합니다. Transact-SQL 문은 추적 로그에 기록됩니다. 다음 예에서는 로그에 Transact-SQL 문을 추가하는 구성 설정을 보여 줍니다.<br /><br /> \<add name="Components" value="all,SemanticQueryEngine:4" />|구성 요소 범주는 다음과 같이 설정할 수 있습니다.<br /><br /> <br /><br /> 특정 범주로 나눌 수 없는 프로세스의 경우**All** 을 통해 모든 프로세스에 대한 일반적인 보고서 서버 작업이 추적됩니다.<br /><br /> **RunningJobs** 는 진행 중인 보고서나 구독 작업을 추적하는 데 사용됩니다.<br /><br /> **SemanticQueryEngine** 은 사용자가 모델 기반 보고서에서 임시 데이터 탐색을 수행할 때 처리되는 의미 체계 쿼리를 추적하는 데 사용됩니다.<br /><br /> 모델 생성의 경우**SemanticModelGenerator** 를 통해 추적됩니다.<br /><br /> 보고서 서버 HTTP 로그 파일의 경우**http** 를 통해 설정됩니다. 자세한 내용은 [Report Server HTTP Log](../../reporting-services/report-server/report-server-http-log.md)을 참조하세요.|  
|구성 요소 범주에 대한 **추적 수준** 값|\<구성 요소 범주 >:\<tracelevel ><br /><br /> <br /><br /> 구성 요소에 추적 수준을 추가하지 않으면 **DefaultTraceSwitch** 에 대해 지정된 값이 사용됩니다. 예를 들어 "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator"를 지정하면 모든 구성 요소에서 기본 추적 수준을 사용합니다.|유효한 추적 수준 값은 다음과 같습니다.<br /><br /> <br /><br /> 0= 추적 해제<br /><br /> 1= 예외 및 다시 시작<br /><br /> 2= 예외, 다시 시작, 경고<br /><br /> 3= 예외, 다시 시작, 경고, 상태 메시지(기본값)<br /><br /> 4= 세부 정보 표시 모드<br /><br /> 보고서 서버의 기본값은 "all:3"입니다.|  
  
## <a name="adding-custom-configuration-setting-to-specify-a-dump-file-location"></a><a name="bkmk_add_custom"></a> 덤프 파일 위치 지정을 위한 사용자 지정 구성 설정 추가  
Windows용 Dr. Watson 도구에서 덤프 파일 저장에 사용하는 위치를 설정하기 위해 사용자 지정 설정을 추가할 수 있습니다. 사용자 지정 설정은 **Directory**입니다. 다음 예에서는 **RStrace** 섹션에 이 구성 설정을 지정하는 방법을 보여 줍니다.  

```
<add name="Directory" value="U:\logs\" />  
```  
  
자세한 내용은 [웹 사이트의](https://support.microsoft.com/?kbid=913046) 기술 자료 문서 913046 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 을 참조하세요.  
  
##  <a name="log-file-fields"></a><a name="bkmk_log_file_fields"></a> 로그 파일 필드

추적 로그에는 다음과 같은 필드가 있습니다.  
  
- 운영 체제, 버전, 프로세서 수 및 메모리를 포함한 시스템 정보  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소 및 버전 정보  
  
- 애플리케이션 로그에 기록된 이벤트  
  
- 보고서 서버에서 생성한 예외  
  
- 보고서 서버에서 기록한 리소스 부족 경고  
  
- 인바운드 SOAP Envelope 및 요약된 아웃바운드 SOAP Envelope  
  
- HTTP 헤더, 스택 추적 및 디버그 추적 정보  
  
 추적 로그 정보를 검토하여 보고서가 배달되었는지 여부, 보고서를 받은 사용자 및 배달 시도 횟수를 확인할 수 있습니다. 또한 추적 로그는 보고서 실행 작업 및 보고서 처리 중에 적용되는 환경 변수를 기록합니다. 오류와 예외도 추적 로그에 입력됩니다. 예를 들어 **ThreadAbortExceptions** 항목으로 표시되는 보고서 시간 초과 오류를 발견할 수 있습니다.  

## <a name="previous-versions"></a>이전 버전

이전 릴리스의 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]에서는 애플리케이션마다 하나씩, 여러 개의 추적 로그 파일이 있었습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서
+ ReportServerWebApp_ *\<timestamp>* .log
+ ReportServer_ *\<timestamp>* .log
+ ReportServerService_main_ *\<timestamp>* .log
  
## <a name="see-also"></a>참고 항목

- [Reporting Services 로그 파일 및 원본](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
- [오류 및 이벤트 참조&#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  

추가 질문이 있으신가요? [Reporting Services 포럼을 이용해 보세요.](https://go.microsoft.com/fwlink/?LinkId=620231)