---
title: ReportingServicesService 구성 파일| Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- traces [Reporting Services]
- Report Server Windows service, ReportingServicesService configuration file
- ReportingServicesService configuration file
ms.assetid: 40f4a401-cb61-4c42-b1ec-01acdacdacd1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dfb0f48bb35e6341e2b2a9a72007ef4eb09c2b9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506627"
---
# <a name="reportingservicesservice-configuration-file"></a>ReportingServicesService 구성 파일

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)]
  
ReportingServicesService.exe.config 파일에는 추적을 구성하는 설정이 들어 있습니다.  
  
## <a name="file-location"></a>파일 위치  
아래 경로 중 하나에서이 파일을 찾을 수 없습니다.  

``` Paths  
\Reporting Services\Report Server\Bin  
\Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin  
```  
 
## <a name="editing-guidelines"></a>편집 지침  
 로그 파일 이름을 바꾸거나 추적 수준을 올리거나 내리기 위해 이 파일을 수정할 수 있습니다. 다른 설정은 수정하지 마십시오. 자세한 내용은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요. 추적 로그에 대한 자세한 내용은 [보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)를 참조하세요.  
  
## <a name="example-configuration"></a>구성 예  
 다음 예에서는 ReportingServicesService.exe.config 파일에 나오는 설정 및 기본값을 보여 줍니다.  
  
```  
<configSections>  
      <section name="RStrace" type="Microsoft.ReportingServices.Diagnostics.RSTraceSectionHandler,Microsoft.ReportingServices.Diagnostics" />  
</configSections>  
\<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
\</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="debugwindow, file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
<runtime>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
             <dependentAssembly>  
                    <assemblyIdentity name="Microsoft.ReportingServices.Interfaces"  
                        publicKeyToken="89845dcd8080cc91"  
                        culture="neutral" />  
                    <bindingRedirect oldVersion="8.0.242.0"  
                                     newVersion="10.0.0.0"/>  
                    <bindingRedirect oldVersion="9.0.242.0"  
                                     newVersion="10.0.0.0"/>  
             </dependentAssembly>  
      </assemblyBinding>  
      <gcServer enabled="true" />  
</runtime>  
```  
  
## <a name="configuration-settings"></a>구성 설정  
 다음 표는 특정 설정에 대한 정보를 제공합니다. 설정은 구성 파일에 나타나는 순서로 표시됩니다.  
  
|설정|설명|  
|-------------|-----------------|  
|**RStrace**|오류 및 추적에 사용되는 네임스페이스를 지정합니다.|  
|**DefaultTraceSwitch**|ReportServerService 추적 로그에 보고되는 정보의 수준을 지정합니다. 각 수준에는 낮은 번호가 매겨진 모든 수준별로 보고된 정보가 들어 있습니다. 추적을 설정하는 것이 좋습니다. 유효한 값은 다음과 같습니다.<br /><br /> 0= 추적 해제<br /><br /> 1= 예외 및 다시 시작<br /><br /> 2= 예외, 다시 시작, 경고<br /><br /> 3= 예외, 다시 시작, 경고, 상태 메시지(기본값)<br /><br /> 4= 세부 정보 표시 모드|  
|**FileName**|로그 파일 이름의 첫 번째 부분을 지정합니다. **Prefix** 에 지정된 값으로 이름의 나머지 부분을 완성합니다. 기본적으로 이름은 ReportServerService_가 됩니다.|  
|**FileSizeLimitMb**|추적 로그 크기에 대한 상한값을 지정합니다. 파일은 메가바이트(MB) 단위로 측정됩니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 32입니다.|  
|**KeepFilesForDays**|추적 로그 파일을 몇 일 후에 삭제할지 지정합니다. 유효한 값은 0에서 최대 정수 사이입니다. 기본값은 14입니다.|  
|**Prefix**|로그 인스턴스를 구분하는 생성 값을 지정합니다. 기본적으로 타임스탬프 값이 추적 로그 파일 이름에 추가됩니다. 이 값은 " tid, time"으로 설정됩니다. 이 설정은 수정하지 마세요.|  
|**TraceListeners**|추적 로그 내용을 출력할 대상을 지정합니다. 대상이 여러 개일 경우 쉼표로 구분하여 지정할 수 있습니다. 유효한 값은 다음과 같습니다.<br /><br /> DebugWindow(기본값)<br /><br /> File(기본값)<br /><br /> StdOut|  
|**TraceFileMode**|추적 로그에 24시간 동안의 데이터를 포함할지 여부를 지정합니다. 일별로 각 구성 요소마다 고유한 추적 로그가 하나씩 있어야 합니다. 이 값은 "Unique(기본값)"로 설정됩니다. 이 값은 수정하지 마세요.|  
|**Components**|추적 로그를 생성할 구성 요소를 지정합니다. 기본값은 **all**입니다. 이 설정에 대한 기타 유효한 값에는 내부 구성 요소의 이름이 포함됩니다. 이 값은 수정하지 마세요.|  
|**런타임**|이전 버전과의 호환성을 지원하는 구성 설정을 지정합니다. 런타임 설정은 이전 버전의 Microsoft.ReportingServices.Interfaces를 대상으로 하는 요청을 새 버전으로 리디렉션하는 데 사용됩니다.<br /><br /> 이 섹션의 모든 구성 설정은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 제품 설명서에 설명되어 있습니다. 자세한 내용을 보려면 MSDN 웹 사이트 또는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 설명서에서 "Runtime Schema Settings"를 검색하십시오.|  
  
## <a name="see-also"></a>관련 항목:  
[Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)  
[보고서 서버 서비스 추적 로그](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
