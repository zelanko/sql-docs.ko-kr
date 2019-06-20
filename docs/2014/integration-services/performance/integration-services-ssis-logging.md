---
title: Integration Services(SSIS) 로깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2478f1605b7fb67d8328be905956cbaae8e3c243
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889815"
---
# <a name="integration-services-ssis-logging"></a>Integration Services(SSIS) 로깅
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지, 컨테이너 및 태스크에서의 로깅 구현을 위해 사용할 수 있는 로그 공급자가 포함됩니다. 로깅을 사용하면 패키지에 대한 런타임 정보를 캡처하여 패키지가 실행될 때마다 패키지를 감사하고 문제를 해결하는 데 활용할 수 있습니다. 예를 들어 로그를 사용하여 패키지를 실행한 운영자의 이름과 패키지가 시작 및 종료된 시간을 캡처할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 패키지 실행 중에 발생하는 로깅 범위를 구성할 수 있습니다. 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../enable-logging-for-package-execution-on-the-ssis-server.md)을 참조하세요.  
  
 **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지 실행할 때도 로깅을 포함할 수 있습니다. 로깅을 지원하는 명령 프롬프트 인수에 대한 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하십시오.  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>SQL Server Data Tools에서 로깅 구성  
 로그는 패키지와 연결되며 패키지 수준에서 구성됩니다. 패키지에 있는 각 태스크나 컨테이너는 패키지 로그에 정보를 로깅할 수 있습니다. 패키지 자체가 로깅을 사용하도록 설정되지 않았더라도 패키지의 태스크 및 컨테이너는 로깅을 사용하도록 설정될 수 있습니다. 예를 들어 부모 패키지가 로깅을 사용하지 않더라도 SQL 실행 태스크는 로깅을 사용할 수 있습니다. 패키지, 컨테이너 또는 태스크는 여러 로그에 쓸 수 있습니다. 패키지에만 로깅을 사용하도록 설정하거나 패키지에 포함된 개별 태스크 또는 컨테이너에 로깅을 사용하도록 설정할 수 있습니다.  
  
 패키지에 로그를 추가할 때는 로그 공급자와 로그 위치를 선택합니다. 로그 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 텍스트 파일 같은 로그 데이터 형식을 지정합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 다음 로그 공급자가 포함됩니다.  
  
-   텍스트 파일 로그 공급자는 로그 항목을 CSV(쉼표로 구분된 값) 형식으로 ASCII 텍스트 파일에 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .log입니다.  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로그 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler를 사용하여 볼 수 있는 추적을 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .trc입니다.  
  
    > [!NOTE]  
    >  64비트 모드로 실행 중인 패키지에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로그 공급자를 사용할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자는 로그 항목을 기록 합니다 `sysssislog` 테이블에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스.  
  
-   Windows 이벤트 로그 공급자는 로컬 컴퓨터의 Windows 이벤트 로그에서 애플리케이션 로그에 항목을 기록합니다.  
  
-   XML 파일 로그 공급자는 로그 파일을 XML 파일로 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .xml입니다.  
  
 패키지에 로그 공급자를 추가하거나 로깅을 프로그래밍 방식으로 구성하는 경우에는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너가 **SSIS 로그 구성** 대화 상자에 표시하는 이름을 사용하는 대신 ProgID 또는 ClassID를 사용하여 로그 공급자를 지정할 수 있습니다.  
  
 다음 표에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 로그 공급자에 대한 ProgID 및 ClassID와 로그 공급자가 작성하는 로그의 위치가 나와 있습니다.  
  
|로그 공급자|ProgID|ClassID|위치|  
|------------------|------------|-------------|--------------|  
|텍스트 파일|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|텍스트 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
|SQL Server 프로파일러|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]가 사용하는 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|로그 항목이 포함된 sysssislog 테이블이 들어 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 로그 공급자가 사용하는 OLE DB 연결 관리자가 지정합니다.|  
|Windows 이벤트 로그|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows 이벤트 뷰어의 애플리케이션 로그에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 애플리케이션 정보가 들어 있습니다.|  
|XML 파일|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|XML 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
  
 사용자 지정 로그 공급자를 만들 수도 있습니다. 자세한 내용은 [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)를 참조하세요.  
  
 패키지의 로그 공급자는 패키지의 로그 공급자 컬렉션의 멤버입니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 만들고 로깅을 구현하는 경우 **디자이너의** 패키지 탐색기 **탭에서** 로그 공급자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 폴더의 컬렉션 멤버 목록을 확인할 수 있습니다.  
  
 로그 공급자에 대한 이름 및 설명을 제공하고 로그 공급자에서 사용되는 연결 관리자를 지정하여 로그 공급자를 구성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자는 OLE DB 연결 관리자를 사용합니다. 텍스트 파일, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]및 XML 파일 로그 공급자는 모두 파일 연결 관리자를 사용합니다. Windows 이벤트 로그 공급자는 Windows 이벤트 로그에 직접 쓰기 때문에 연결 관리자를 사용하지 않습니다. 자세한 내용은 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) 및 [File Connection Manager](../connection-manager/file-connection-manager.md)를 참조하세요.  
  
### <a name="logging-customization"></a>로깅 사용자 지정  
 이벤트 또는 사용자 지정 메시지 로깅을 사용자 지정하기 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 로그 항목에 포함할 자주 로깅되는 정보를 담은 스키마를 제공합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로그 스키마는 로깅할 수 있는 정보를 정의합니다. 로그 스키마에서 요소를 선택하여 각 로그 항목으로 사용할 수 있습니다.  
  
 패키지 및 패키지에 포함된 컨테이너와 태스크는 같은 정보를 로깅할 필요가 없으며 같은 패키지나 컨테이너 내에 있는 태스크가 서로 다른 정보를 로깅할 수 있습니다. 예를 들어 패키지는 시작할 때 작업자 정보를 로깅하고, 한 태스크는 태스크가 실패한 컨테이너 또는 태스크 이름을 로깅하며, 다른 태스크는 오류가 발생한 시각을 로깅할 수 있습니다. 패키지 및 패키지에 포함된 컨테이너와 태스크가 여러 로그를 사용하는 경우 같은 정보가 모든 로그에 기록됩니다.  
  
 필요에 따라 로깅할 이벤트 및 각 이벤트에 대해 로깅할 정보를 지정하여 로깅 수준을 선택할 수 있습니다. 일부 이벤트가 다른 이벤트보다 더 유용한 정보를 제공하는 경우가 있습니다. 예를 들어 이벤트의 중요성에 따라 **PreExecute** 이벤트에 대해서는 컴퓨터 및 작업자 이름만 로깅하고 **Error** 이벤트에 대해서는 모든 사용 가능한 정보를 로깅할 수 있습니다.  
  
 로그 파일이 많은 디스크 공간을 사용하거나 과도한 로깅 작업을 하여 성능이 저하되는 것을 막기 위해 로깅할 특정 이벤트 및 정보 항목을 지정하여 로깅을 제한할 수 있습니다. 예를 들어 각 오류의 날짜 및 컴퓨터 이름만 캡처하도록 로그를 구성할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **SSIS 로그 구성** 대화 상자를 사용하여 로깅 옵션을 정의할 수 있습니다.  
  
#### <a name="log-schema"></a>로그 스키마  
 다음 표에서는 로그 스키마의 요소에 대해 설명합니다.  
  
|요소|Description|  
|-------------|-----------------|  
|Computer|로그 이벤트가 발생한 컴퓨터의 이름입니다.|  
|연산자|패키지를 시작한 사용자의 ID입니다.|  
|SourceName|로그 이벤트가 발생한 컨테이너 또는 태스크의 이름입니다.|  
|SourceID|로그 이벤트가 발생한 패키지, For Loop, Foreach Loop, 시퀀스 컨테이너 또는 태스크의 고유 식별자입니다.|  
|ExecutionID|패키지 실행 인스턴스의 GUID입니다.<br /><br /> 참고: 단일 패키지를 실행하면 ExecutionID 요소에 대한 여러 값이 포함된 로그 항목이 만들어질 수 있습니다. 예를 들어 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 실행하면 유효성 검사 단계에서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에 해당하는 ExecutionID 요소가 포함된 로그 항목이 만들어질 수 있습니다. 그러나 실행 단계에서는 dtshost.exe에 해당하는 ExecutionID 요소가 포함된 로그 항목이 만들어질 수 있습니다. 또 Execute Package 태스크가 포함된 패키지를 실행하면 이러한 각 태스크가 자식 패키지를 실행합니다. 이러한 자식 패키지는 부모 패키지에서 만든 로그 항목과 다른 ExecutionID 요소가 포함된 로그 항목을 만들 수 있습니다.|  
|MessageText|로그 항목과 연결된 메시지입니다.|  
|DataBytes|로그 항목과 관련된 바이트 배열입니다. 이 필드의 의미는 로그 항목에 따라 다릅니다.|  
  
 다음 표에서는 **SSIS 로그 구성** 대화 상자의 **자세히** 탭에서 사용할 수 없는 로그 스키마의 세 가지 추가 요소에 대해 설명합니다.  
  
|요소|Description|  
|-------------|-----------------|  
|StartTime|컨테이너 또는 태스크가 실행되기 시작하는 시간입니다.|  
|EndTime|컨테이너 또는 태스크의 실행이 중지되는 시간입니다.|  
|DataCode|일반적으로 다음과 같이 컨테이너 또는 태스크 실행의 결과를 나타내는 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 열거의 값을 포함하는 선택적 정수 값입니다.<br /><br /> 0 - 성공<br /><br /> 1 - 실패<br /><br /> 2 - 완료<br /><br /> 3 - 취소됨|  
  
##### <a name="log-entries"></a>로그 항목  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 미리 정의된 이벤트에 대한 로그 항목을 지원하고 여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체에 대한 사용자 지정 로그 항목을 제공합니다. **디자이너의** SSIS 로그 구성 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자에 이러한 이벤트와 사용자 지정 로그 항목이 나열됩니다.  
  
 다음 표에서는 런타임 이벤트가 발생했을 때 로그 항목을 쓰도록 설정할 수 있는 미리 정의된 이벤트에 대해 설명합니다. 이러한 로그 항목은 실행 파일과 패키지, 그리고 패키지에 포함된 태스크 및 컨테이너에 적용됩니다. 로그 항목의 이름은 발생한 런타임 이벤트의 이름, 즉 로그 항목을 쓰도록 만든 이벤트의 이름과 같습니다.  
  
|이벤트|Description|  
|------------|-----------------|  
|**OnError**|오류가 발생할 때 로그 항목을 기록합니다.|  
|**OnExecStatusChanged**|태스크(컨테이너가 아님)가 디버깅 중에 일시 중지되거나 재개될 때 로그 항목을 작성합니다.|  
|**OnInformation**|정보 보고를 위한 실행 파일의 유효성 검사 및 실행 중에 로그 항목을 기록합니다.|  
|**OnPostExecute**|실행 파일이 실행을 완료한 직후에 로그 항목을 기록합니다.|  
|**OnPostValidate**|실행 파일의 유효성 검사가 완료될 때 로그 항목을 기록합니다.|  
|**OnPreExecute**|실행 파일이 실행하기 직전에 로그 항목을 기록합니다.|  
|**OnPreValidate**|실행 파일의 유효성 검사가 시작할 때 로그 항목을 기록합니다.|  
|**OnProgress**|실행 파일이 특정 진행 상태에 도달했을 때 로그 항목을 기록합니다.|  
|**OnQueryCancel**|실행을 취소할 수 있는 태스크 처리 과정의 모든 분기 시점에 로그 항목을 기록합니다.|  
|**OnTaskFailed**|태스크가 실패할 때 로그 항목을 기록합니다.|  
|**OnVariableValueChanged**|변수의 값이 변경될 때 로그 항목을 기록합니다.|  
|**OnWarning**|경고가 발생할 때 로그 항목을 기록합니다.|  
|**PipelineComponentTime**|각 데이터 흐름 구성 요소에 대해 유효성 검사 및 실행의 각 단계에 대한 로그 항목을 기록합니다. 로그 항목에서는 각 단계의 처리 시간을 지정합니다.|  
|**진단**|진단 정보를 제공하는 로그 항목을 기록합니다.<br /><br /> 예를 들어 외부 데이터 공급자에 대한 각 호출 전후의 메시지를 기록할 수 있습니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.|  
  
 패키지 및 여러 태스크에는 로깅을 사용하도록 설정할 수 있는 사용자 지정 로그 항목이 있습니다. 예를 들어 메일 보내기 태스크는 태스크가 시작되어 메일 메시지를 보내기 전에 정보를 로깅하는 **SendMailTaskBegin** 사용자 지정 로그 항목을 제공합니다. 자세한 내용은 [Custom Messages for Logging](../custom-messages-for-logging.md)를 참조하세요.  
  
### <a name="differentiating-package-copies"></a>패키지 복사본 구분  
 로그 데이터에는 로그 항목이 속하는 패키지의 이름 및 GUID가 포함됩니다. 기존 패키지를 복사하여 새 패키지를 만들 경우 기존 패키지의 이름 및 GUID도 복사됩니다. 따라서 이름과 GUID가 동일한 두 개의 패키지가 있을 수 있으며 이로 인해 로그 데이터에 있는 패키지를 구분하기가 어려울 수 있습니다.  
  
 이러한 혼동을 피하려면 새 패키지의 이름 및 GUID를 업데이트해야 합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 `ID` 속성에서 GUID를 다시 생성하고 속성 창에서 `Name` 속성 값을 업데이트할 수 있습니다. 또한 GUID 및 이름을 프로그래밍 방식으로 변경하거나 **dtutil** 명령 프롬프트를 사용하여 변경할 수 있습니다. 자세한 내용은 [패키지 속성 설정](../set-package-properties.md) 및 [dtutil 유틸리티](../dtutil-utility.md)를 참조하세요.  
  
### <a name="parent-logging-options"></a>부모 로깅 옵션  
 태스크, For Loop, Foreach Loop 및 시퀀스 컨테이너의 로깅 옵션은 해당하는 패키지 또는 부모 컨테이너와 일치하는 경우가 많습니다. 이러한 경우 부모 컨테이너에서 로깅 옵션을 상속받도록 구성할 수 있습니다. 예를 들어 For Loop 컨테이너에 포함된 SQL 실행 태스크는 For Loop 컨테이너에 설정된 로깅 옵션을 사용할 수 있습니다. 부모 로깅 옵션을 사용하려면 컨테이너의 LoggingMode 속성을 **UseParentSetting**으로 설정합니다. **의** 속성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 창 또는 **디자이너의** SSIS 로그 구성 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 통해 이 속성을 설정할 수 있습니다.  
  
### <a name="logging-templates"></a>로깅 템플릿  
 **SSIS 로그 구성** 대화 상자에서 자주 사용하는 로깅 구성을 템플릿으로 만들어 저장한 다음 여러 패키지에서 사용할 수 있습니다. 이렇게 하면 여러 패키지에 대해 일관된 로깅 정책을 적용할 수 있으며 템플릿을 업데이트한 다음 적용하여 여러 패키지에 대한 로그 설정을 쉽게 수정할 수 있습니다. 템플릿은 XML 파일로 저장됩니다.  
  
 **SSIS 로그 구성 대화 상자를 사용하여 로깅을 구성하려면**  
  
1.  패키지 및 패키지에 속한 태스크에 대해 로깅을 사용하도록 설정합니다. 로깅은 패키지, 컨테이너 및 태스크 수준에서 발생할 수 있습니다. 패키지, 컨테이너 및 태스크에 대해 서로 다른 로그를 지정할 수 있습니다.  
  
2.  로그 공급자를 선택하고 패키지에 대한 로그를 추가합니다. 로그는 패키지 수준에서만 만들 수 있으며 태스크나 컨테이너는 패키지에 대해 만들어진 로그 중 하나를 사용해야 합니다. 각 로그는 텍스트 파일, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Windows 이벤트 로그, XML 파일 중 하나의 로그 공급자와 연결됩니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](../enable-package-logging-in-sql-server-data-tools.md)을 참조하세요.  
  
3.  로그에서 캡처할 각 이벤트 및 해당 이벤트에 대한 로그 스키마 정보를 선택합니다. 자세한 내용은 [저장된 구성 파일을 사용하여 로깅 구성](../configure-logging-by-using-a-saved-configuration-file.md)을 참조하세요.  
  
### <a name="configuration-of-log-provider"></a>로그 공급자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 로그 공급자는 패키지에서 로깅을 구현하는 단계로 생성 및 구성됩니다. 자세한 내용은 [Integration Services 로깅](integration-services-ssis-logging.md)합니다.  
  
 로그 공급자를 만든 다음에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에서 해당 속성을 보고 수정할 수 있습니다.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 클래스에 대한 설명서를 참조하세요.  
  
### <a name="logging-for-data-flow-tasks"></a>데이터 흐름 태스크에 대한 로깅  
 데이터 흐름 태스크에서는 성능을 모니터링하고 조정하는 데 사용할 수 있는 여러 가지 사용자 지정 로그 항목을 제공합니다. 예를 들어 메모리 손실을 유발할 수 있는 구성 요소를 모니터링하거나 특정 구성 요소를 실행하는 데 소요되는 시간을 추적할 수 있습니다. 이러한 사용자 지정 로그 항목의 목록과 예제 로깅 출력은 [Data Flow Task](../control-flow/data-flow-task.md)을 참조하십시오.  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>PipelineComponentTime 이벤트 사용  
 가장 유용한 사용자 지정 로그 항목은 PipelineComponentTime 이벤트일 수 있습니다. 이 로그 항목은 5개의 각 주요 처리 단계에서 데이터 흐름의 각 구성 요소에 소요된 시간(밀리초)을 보고합니다. 다음 표에서는 이러한 처리 단계에 대해 설명합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개발자는 이러한 단계를 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>을 참조하세요.  
  
|단계|Description|  
|----------|-----------------|  
|유효성 검사|구성 요소가 유효한 속성 값 및 구성 설정을 확인합니다.|  
|PreExecute|구성 요소가 데이터 행을 처리하기 전에 일회성 처리를 수행합니다.|  
|PostExecute|구성 요소가 모든 데이터 행을 처리한 후 일회성 처리를 수행합니다.|  
|ProcessInput|변환 또는 대상 구성 요소가 업스트림 원본이나 변환에서 전달한 들어오는 데이터 행을 처리합니다.|  
|PrimeOutput|원본 또는 변환 구성 요소가 다운스트림 변환이나 대상 구성 요소에 전달할 데이터의 버퍼를 채웁니다.|  
  
 PipelineComponentTime 이벤트를 설정하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 각 구성 요소가 수행하는 각 처리 단계에 대해 각각 하나씩의 메시지를 기록합니다. 다음 로그 항목은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CalculatedColumns 패키지 예제가 기록하는 메시지의 일부를 보여 줍니다.  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 이러한 로그 항목은 데이터 흐름 태스크의 대부분의 시간이 아래 나열된(내림차순) 단계에 소요되었음을 나타냅니다.  
  
-   "Extract Data"라는 OLE DB 원본이 데이터를 로드하는 데 688밀리초가 소요되었습니다.  
  
-   "Calculate LineItemTotalCost"라는 파생 열 변환이 들어오는 열을 계산하는 데 356밀리초가 소요되었습니다.  
  
-   "Sum Quantity and LineItemTotalCost"라는 집계 변환이 데이터를 계산하고 다음 변환에 전달하는 데 PrimeOutput과 ProcessInput에서 각각 141밀리초와 79밀리초씩 총 220밀리초가 소요되었습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다음 목록에는 로깅 기능과 관련된 태스크를 수행하는 방법을 보여 주는 항목에 대한 링크가 나와 있습니다.  
  
-   [SSIS 로그 구성 대화 상자](../configure-ssis-logs-dialog-box.md)  
  
-   [SQL Server Data Tools에서 패키지 로깅 사용](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [이벤트 로그 창에서 로그 항목 보기](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>관련 내용  
 [전체 및 세부 정보 로깅을 위한 DTLoggedExec 도구(CodePlex 프로젝트)](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>관련 항목  
 [이벤트 로그 창에서 로그 항목 보기](../view-log-entries-in-the-log-events-window.md)  
  
  
