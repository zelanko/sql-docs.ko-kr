---
title: Integration Services(SSIS) 로깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.configuredtslogs.containers.f1
- sql13.dts.designer.configuredtslogs.loggingdetails.f1
- sql13.dts.designer.configuredtslogs.providersandlogs.f1
- SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1
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
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd0e92f62d99f30d244b9fc14bbf0ebb42f15269
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-ssis-logging"></a>Integration Services(SSIS) 로깅
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 패키지, 컨테이너 및 태스크에서의 로깅 구현을 위해 사용할 수 있는 로그 공급자가 포함됩니다. 로깅을 사용하면 패키지에 대한 런타임 정보를 캡처하여 패키지가 실행될 때마다 패키지를 감사하고 문제를 해결하는 데 활용할 수 있습니다. 예를 들어 로그를 사용하여 패키지를 실행한 운영자의 이름과 패키지가 시작 및 종료된 시간을 캡처할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 패키지 실행 중에 발생하는 로깅 범위를 구성할 수 있습니다. 자세한 내용은 [Enable Logging for Package Execution on the SSIS Server](#server_logging)을 참조하세요.  
  
 **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지 실행할 때도 로깅을 포함할 수 있습니다. 로깅을 지원하는 명령 프롬프트 인수에 대한 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하십시오.  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>SQL Server Data Tools에서 로깅 구성  
 로그는 패키지와 연결되며 패키지 수준에서 구성됩니다. 패키지에 있는 각 태스크나 컨테이너는 패키지 로그에 정보를 로깅할 수 있습니다. 패키지 자체가 로깅을 사용하도록 설정되지 않았더라도 패키지의 태스크 및 컨테이너는 로깅을 사용하도록 설정될 수 있습니다. 예를 들어 부모 패키지가 로깅을 사용하지 않더라도 SQL 실행 태스크는 로깅을 사용할 수 있습니다. 패키지, 컨테이너 또는 태스크는 여러 로그에 쓸 수 있습니다. 패키지에만 로깅을 사용하도록 설정하거나 패키지에 포함된 개별 태스크 또는 컨테이너에 로깅을 사용하도록 설정할 수 있습니다.  
  
 패키지에 로그를 추가할 때는 로그 공급자와 로그 위치를 선택합니다. 로그 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 텍스트 파일 같은 로그 데이터 형식을 지정합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 다음 로그 공급자가 포함됩니다.  
  
-   텍스트 파일 로그 공급자는 로그 항목을 CSV(쉼표로 구분된 값) 형식으로 ASCII 텍스트 파일에 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .log입니다.  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로그 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler를 사용하여 볼 수 있는 추적을 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .trc입니다.  
  
    > [!NOTE]  
    >  64비트 모드로 실행 중인 패키지에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 로그 공급자를 사용할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자는 **데이터베이스의** sysssislog [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 로그 항목을 기록합니다.  
  
-   Windows 이벤트 로그 공급자는 로컬 컴퓨터의 Windows 이벤트 로그에서 응용 프로그램 로그에 항목을 기록합니다.  
  
-   XML 파일 로그 공급자는 로그 파일을 XML 파일로 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .xml입니다.  
  
 패키지에 로그 공급자를 추가하거나 로깅을 프로그래밍 방식으로 구성하는 경우에는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너가 **SSIS 로그 구성** 대화 상자에 표시하는 이름을 사용하는 대신 ProgID 또는 ClassID를 사용하여 로그 공급자를 지정할 수 있습니다.  
  
 다음 표에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함된 로그 공급자에 대한 ProgID 및 ClassID와 로그 공급자가 작성하는 로그의 위치가 나와 있습니다.  
  
|로그 공급자|ProgID|ClassID|위치|  
|------------------|------------|-------------|--------------|  
|텍스트 파일|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|텍스트 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
|SQL Server 프로파일러|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]가 사용하는 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|로그 항목이 포함된 sysssislog 테이블이 들어 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스는 로그 공급자가 사용하는 OLE DB 연결 관리자가 지정합니다.|  
|Windows 이벤트 로그|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows 이벤트 뷰어의 응용 프로그램 로그에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 응용 프로그램 정보가 들어 있습니다.|  
|XML 파일|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|XML 파일의 경로는 로그 공급자가 사용하는 파일 연결 관리자가 지정합니다.|  
  
 사용자 지정 로그 공급자를 만들 수도 있습니다. 자세한 내용은 [Creating a Custom Log Provider](../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)를 참조하세요.  
  
 패키지의 로그 공급자는 패키지의 로그 공급자 컬렉션의 멤버입니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 패키지를 만들고 로깅을 구현하는 경우 **디자이너의** 패키지 탐색기 **탭에서** 로그 공급자 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 폴더의 컬렉션 멤버 목록을 확인할 수 있습니다.  
  
 로그 공급자에 대한 이름 및 설명을 제공하고 로그 공급자에서 사용되는 연결 관리자를 지정하여 로그 공급자를 구성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자는 OLE DB 연결 관리자를 사용합니다. 텍스트 파일, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]및 XML 파일 로그 공급자는 모두 파일 연결 관리자를 사용합니다. Windows 이벤트 로그 공급자는 Windows 이벤트 로그에 직접 쓰기 때문에 연결 관리자를 사용하지 않습니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) 및 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)를 참조하세요.  
  
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
  
#### <a name="log-entries"></a>로그 항목  
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
|**진단**<br /><br /> **DiagnosticEx**|진단 정보를 제공하는 로그 항목을 기록합니다.<br /><br /> 예를 들어 외부 데이터 공급자에 대한 각 호출 전후의 메시지를 기록할 수 있습니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.<br /><br /> 데이터 흐름에서 오류가 발생한 열의 열 이름을 찾으려면 **DiagnosticEx** 이벤트를 기록합니다. 이 이벤트는 로그에 데이터 흐름 계보 지도를 작성합니다. 그런 다음 오류 출력에 의해 캡처된 열 식별자를 사용하여 이 계보 맵에서 열 이름을 조회할 수 있습니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.<br /><br /> **DiagnosticEx** 이벤트는 로그의 크기를 줄이기 위해 해당 XML 출력에서 공백을 유지하지 않습니다. 가독성을 높이기 위해 XML 서식 지정 및 구문 강조를 지원하는 XML 편집기(예: Visual Studio)로 로그를 복사합니다.<br /><br /> 참고: SQL Server 로그 공급자를 사용하여 **DiagnosticEx** 이벤트를 기록하는 경우에는 출력이 잘릴 수 있습니다. SQL Server 로그 공급자의 **message** 필드는 nvarchar(2048) 형식입니다. 로그가 잘리지 않도록 하려면 **DiagnosticEx** 이벤트를 기록할 때 다른 로그 공급자를 사용하세요.|  
  
 패키지 및 여러 태스크에는 로깅을 사용하도록 설정할 수 있는 사용자 지정 로그 항목이 있습니다. 예를 들어 메일 보내기 태스크는 태스크가 시작되어 메일 메시지를 보내기 전에 정보를 로깅하는 **SendMailTaskBegin** 사용자 지정 로그 항목을 제공합니다. 자세한 내용은 [Custom Messages for Logging](#custom_messages)를 참조하세요.  
  
### <a name="differentiating-package-copies"></a>패키지 복사본 구분  
 로그 데이터에는 로그 항목이 속하는 패키지의 이름 및 GUID가 포함됩니다. 기존 패키지를 복사하여 새 패키지를 만들 경우 기존 패키지의 이름 및 GUID도 복사됩니다. 따라서 이름과 GUID가 동일한 두 개의 패키지가 있을 수 있으며 이로 인해 로그 데이터에 있는 패키지를 구분하기가 어려울 수 있습니다.  
  
 이러한 혼동을 피하려면 새 패키지의 이름 및 GUID를 업데이트해야 합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **ID** 속성에서 GUID를 다시 생성하고 속성 창에서 **Name** 속성 값을 업데이트할 수 있습니다. 또한 GUID 및 이름을 프로그래밍 방식으로 변경하거나 **dtutil** 명령 프롬프트를 사용하여 변경할 수 있습니다. 자세한 내용은 [패키지 속성 설정](../../integration-services/set-package-properties.md) 및 [dtutil 유틸리티](../../integration-services/dtutil-utility.md)를 참조하세요.  
  
### <a name="parent-logging-options"></a>부모 로깅 옵션  
 태스크, For Loop, Foreach Loop 및 시퀀스 컨테이너의 로깅 옵션은 해당하는 패키지 또는 부모 컨테이너와 일치하는 경우가 많습니다. 이러한 경우 부모 컨테이너에서 로깅 옵션을 상속받도록 구성할 수 있습니다. 예를 들어 For Loop 컨테이너에 포함된 SQL 실행 태스크는 For Loop 컨테이너에 설정된 로깅 옵션을 사용할 수 있습니다. 부모 로깅 옵션을 사용하려면 컨테이너의 LoggingMode 속성을 **UseParentSetting**으로 설정합니다. **의** 속성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 창 또는 **디자이너의** SSIS 로그 구성 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 통해 이 속성을 설정할 수 있습니다.  
  
### <a name="logging-templates"></a>로깅 템플릿  
 **SSIS 로그 구성** 대화 상자에서 자주 사용하는 로깅 구성을 템플릿으로 만들어 저장한 다음 여러 패키지에서 사용할 수 있습니다. 이렇게 하면 여러 패키지에 대해 일관된 로깅 정책을 적용할 수 있으며 템플릿을 업데이트한 다음 적용하여 여러 패키지에 대한 로그 설정을 쉽게 수정할 수 있습니다. 템플릿은 XML 파일로 저장됩니다.  
  
 **SSIS 로그 구성 대화 상자를 사용하여 로깅을 구성하려면**  
  
1.  패키지 및 패키지에 속한 태스크에 대해 로깅을 사용하도록 설정합니다. 로깅은 패키지, 컨테이너 및 태스크 수준에서 발생할 수 있습니다. 패키지, 컨테이너 및 태스크에 대해 서로 다른 로그를 지정할 수 있습니다.  
  
2.  로그 공급자를 선택하고 패키지에 대한 로그를 추가합니다. 로그는 패키지 수준에서만 만들 수 있으며 태스크나 컨테이너는 패키지에 대해 만들어진 로그 중 하나를 사용해야 합니다. 각 로그는 텍스트 파일, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Windows 이벤트 로그, XML 파일 중 하나의 로그 공급자와 연결됩니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](#ssdt)을 참조하세요.  
  
3.  로그에서 캡처할 각 이벤트 및 해당 이벤트에 대한 로그 스키마 정보를 선택합니다. 자세한 내용은 [저장된 구성 파일을 사용하여 로깅 구성](#saved_config)을 참조하세요.  
  
### <a name="configuration-of-log-provider"></a>로그 공급자 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 로그 공급자는 패키지에서 로깅을 구현하는 단계로 생성 및 구성됩니다.  
  
 로그 공급자를 만든 다음에는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 속성 창에서 해당 속성을 보고 수정할 수 있습니다.  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 클래스에 대한 설명서를 참조하세요.  
  
### <a name="logging-for-data-flow-tasks"></a>데이터 흐름 태스크에 대한 로깅  
 데이터 흐름 태스크에서는 성능을 모니터링하고 조정하는 데 사용할 수 있는 여러 가지 사용자 지정 로그 항목을 제공합니다. 예를 들어 메모리 손실을 유발할 수 있는 구성 요소를 모니터링하거나 특정 구성 요소를 실행하는 데 소요되는 시간을 추적할 수 있습니다. 이러한 사용자 지정 로그 항목의 목록과 예제 로깅 출력은 [Data Flow Task](../../integration-services/control-flow/data-flow-task.md)을 참조하십시오.  
  
#### <a name="capture-the-names-of-columns-in-which-errors-occur"></a>오류가 발생하는 열의 이름 캡처  
 데이터 흐름에서 오류 출력을 구성할 때 오류 출력에서는 기본적으로 오류가 발생한 열의 숫자 식별자만 제공됩니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
 로깅을 사용하도록 설정하고 **DiagnosticEx** 이벤트를 선택하여 열 이름을 찾을 수 있습니다. 이 이벤트는 로그에 데이터 흐름 계보 지도를 작성합니다. 그런 다음 이 계보 맵의 식별자를 통해 열 이름을 조회할 수 있습니다. **DiagnosticEx** 이벤트는 로그의 크기를 줄이기 위해 해당 XML 출력에서 공백을 유지하지 않습니다. 가독성을 높이기 위해 XML 서식 지정 및 구문 강조를 지원하는 XML 편집기(예: Visual Studio)로 로그를 복사합니다.  
  
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

## <a name="ssdt"></a> SQL Server Data Tools에서 패키지 로깅 사용
  이 절차에서는 패키지에 로그를 추가하는 방법, 패키지 수준 로깅을 구성하는 방법 및 로깅 구성을 XML 파일에 저장하는 방법을 설명합니다. 로그는 패키지 수준에서만 추가할 수 있지만 패키지에 포함되는 컨테이너에서 로깅을 활성화하기 위해 패키지가 로깅을 수행할 필요는 없습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 배포하는 경우 패키지 실행에 대해 설정한 로깅 수준에 따라 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 구성하는 패키지 로깅이 재정의됩니다.  
  
 기본적으로 패키지 내의 컨테이너는 부모 컨테이너와 동일한 로깅 구성을 사용합니다. 개별 컨테이너에 대한 로깅 옵션을 설정하는 방법은 [저장된 구성 파일을 사용하여 로깅 구성](#saved_config)을 참조하세요.  
  
### <a name="to-enable-logging-in-a-package"></a>패키지에 로깅을 활성화하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **SSIS** 메뉴에서 **로깅**을 클릭합니다.  
  
3.  **공급자 유형** 목록에서 로그 공급자를 선택한 다음 **추가**를 클릭합니다.  
  
4.  **구성** 열에서 연결 관리자를 선택하거나 **\<새 연결>** 을 클릭하여 로그 공급자에 대한 적절한 유형의 연결 관리자를 만듭니다. 선택한 공급자에 따라 다음 연결 관리자 중 하나를 사용합니다.  
  
    -   텍스트 파일에는 파일 연결 관리자를 사용합니다. 자세한 내용은 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)를 참조하세요.  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에는 파일 연결 관리자를 사용합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 OLE DB 연결 관리자를 사용합니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)을 참조하세요.  
  
    -   Windows 이벤트 로그에는 아무 것도 선택하지 마십시오. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 에서 자동으로 로그를 만듭니다.  
  
    -   XML 파일에는 파일 연결 관리자를 사용합니다.  
  
5.  패키지에서 사용할 각 로그에 대해 3단계 및 4단계를 반복합니다.  
  
    > [!NOTE]  
    >  패키지는 각 유형의 로그를 두 개 이상 사용할 수 있습니다.  
  
6.  필요에 따라 패키지 수준 확인란을 선택하고 패키지 수준 로깅에서 사용할 로그를 선택한 다음 **세부 정보** 탭을 클릭합니다.  
  
7.  **자세히** 탭에서 **이벤트** 를 선택하여 모든 로그 항목을 로깅하거나 **이벤트** 선택을 취소하여 개별 이벤트를 선택합니다.  
  
8.  필요에 따라 **고급** 을 클릭하여 로깅할 정보를 지정합니다.  
  
    > [!NOTE]  
    >  기본적으로 모든 정보가 로깅됩니다.  
  
9. **세부 정보** 탭에서 **저장**을 클릭합니다. **다른 이름으로 저장** 대화 상자가 나타납니다. 로깅 구성을 저장할 폴더를 찾고 새 로그 구성의 파일 이름을 입력한 다음 **저장**을 클릭합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="configure_logs"></a> SSIS 로그 구성 대화 상자
  **SSIS 로그 구성** 대화 상자를 사용하여 패키지에 대한 로깅 옵션을 정의할 수 있습니다.  
  
 **수행 작업**  
  
1.  [SSIS 로그 구성 대화 상자 열기](#open_dialog)  
  
2.  [컨테이너 창의 옵션 구성](#container)  
  
3.  [공급자 및 로그 탭의 옵션 구성](#provider)  
  
4.  [자세히 탭의 옵션 구성](#detail)  
  
###  <a name="open_dialog"></a> SSIS 로그 구성 대화 상자 열기  
 **SSIS 로그 구성 대화 상자를 열려면**  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 **SSIS** 메뉴에서 **로깅** 을 클릭합니다.  
  
###  <a name="container"></a> 컨테이너 창의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **컨테이너** 창을 사용하여 패키지 및 해당 컨테이너에 대해 로깅을 활성화할 수 있습니다.  
  
#### <a name="options"></a>변수  
 **SSIS 로그 구성**  
 패키지 및 해당 컨테이너에 대해 로깅을 활성화하려면 계층 뷰의 확인란을 선택합니다.  
  
-   확인란의 선택을 취소하면 해당 컨테이너에 대해 로깅이 활성화되지 않습니다. 로깅을 활성화하려면 선택합니다.  
  
-   확인란이 흐리게 표시된 경우에는 해당 컨테이너에서 부모의 로깅 옵션을 사용하는 것입니다. 패키지에 대해서는 이 옵션을 사용할 수 없습니다.  
  
-   확인란을 선택하면 컨테이너에서 자체 로깅 옵션을 정의합니다.  
  
 컨테이너가 흐리게 표시되어 있는 경우 해당 컨테이너에 대해 로깅 옵션을 설정하려면 확인란을 두 번 클릭합니다. 첫 번째 클릭은 확인란의 선택을 취소하고 두 번째 클릭은 확인란을 선택하여 사용할 로그 공급자 및 기록할 정보를 선택할 수 있습니다.  
  
###  <a name="provider"></a> 공급자 및 로그 탭의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **공급자 및 로그** 탭을 사용하여 런타임 이벤트를 캡처하기 위한 로그를 생성 및 구성할 수 있습니다.  
  
#### <a name="options"></a>변수  
 **공급자 유형**  
 목록에서 로그 공급자 유형을 선택합니다.  
  
 **추가**  
 지정한 유형의 로그를 패키지의 로그 공급자 모음에 추가합니다.  
  
 **이름**  
 **SSIS 로그 구성** 대화 상자의 **컨테이너** 창에서 선택한 컨테이너 또는 태스크에 대한 로그를 확인란을 사용하여 설정하거나 해제합니다. 이름 필드는 편집할 수 있습니다. 공급자의 기본 이름을 사용하거나 설명이 포함된 고유 이름을 입력합니다.  
  
 **설명**  
 설명 필드는 편집할 수 있습니다. 클릭한 다음 로그의 기본 설명을 수정합니다.  
  
 **Configuration**  
 목록에서 기존 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다. 로그 공급자의 유형에 따라 OLE DB 연결 관리자 또는 파일 연결 관리자를 구성할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 이벤트 로그의 로그 공급자에는 연결이 필요하지 않습니다.  
  
 관련 항목: [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) , [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
 **Delete**  
 로그 공급자를 선택한 다음 **삭제**를 클릭합니다.  
  
###  <a name="detail"></a> 자세히 탭의 옵션 구성  
 **SSIS 로그 구성** 대화 상자의 **자세히** 탭을 사용하여 로깅에 사용할 이벤트와 로깅할 세부 정보를 지정할 수 있습니다. 선택한 정보는 패키지의 모든 로그 공급자에 적용됩니다. 예를 들어 일부 정보는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 쓰고 다른 정보는 텍스트 파일에 쓰는 것은 불가능합니다.  
  
#### <a name="options"></a>변수  
 **이벤트**  
 로깅할 이벤트를 설정 또는 해제합니다.  
  
 **설명**  
 이벤트에 대한 설명을 표시합니다.  
  
 **고급**  
 로깅할 이벤트를 선택하거나 선택을 취소하고, 각 이벤트에 대해 로깅할 정보를 선택하거나 선택을 취소합니다. 이벤트 목록을 제외한 모든 로깅 세부 정보를 숨기려면 **기본** 을 클릭합니다. 다음은 로깅에 사용할 수 있는 정보입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Computer**|로깅된 이벤트가 발생한 컴퓨터의 이름입니다.|  
|**같음**|패키지를 시작한 사람의 사용자 이름입니다.|  
|**SourceName**|로깅된 이벤트가 발생한 패키지, 컨테이너 및 태스크의 이름입니다.|  
|**SourceID**|로깅된 이벤트가 발생한 패키지, 컨테이너 또는 태스크의 GUID(Global Unique Identifier)입니다.|  
|**ExecutionID**|패키지 실행 인스턴스의 GUID(Global Unique Identifier)입니다.|  
|**MessageText**|로그 항목과 연결된 메시지입니다.|  
|**DataBytes**|나중에 사용하도록 예약되어 있습니다.|  
  
 **기본**  
 로깅할 이벤트를 선택하거나 선택을 취소합니다. 이 옵션은 이벤트 목록을 제외한 로깅 세부 정보를 숨깁니다. 이벤트를 선택한 경우 해당 이벤트에 대한 모든 로깅 세부 정보가 기본적으로 선택됩니다. 로깅 세부 정보를 모두 표시하려면 **고급** 을 클릭합니다.  
  
 **로드**  
 로깅 옵션을 설정하기 위한 템플릿으로 사용할 기존 XML 파일을 지정합니다.  
  
 **저장**  
 구성 세부 정보를 XML 파일에 템플릿으로 저장합니다.  

## <a name="saved_config"></a> 저장된 구성 파일을 사용하여 로깅 구성
  이 절차에서는 이전에 저장된 로깅 구성 파일을 로드하여 패키지 내의 새 컨테이너를 위한 로깅을 구성하는 방법을 설명합니다.  
  
 기본적으로 패키지의 모든 컨테이너는 부모 컨테이너와 동일한 로깅 구성을 사용합니다. 예를 들어 Foreach 루프 내의 태스크는 Foreach 루프와 동일한 로깅 구성을 사용합니다.  
  
### <a name="to-configure-logging-for-a-container"></a>컨테이너에 대한 로깅을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **SSIS** 메뉴에서 **로깅**을 클릭합니다.  
  
3.  패키지 트리 뷰를 확장하고 구성할 컨테이너를 선택합니다.  
  
4.  **공급자 및 로그** 탭에서 컨테이너로 사용할 로그를 선택합니다.  
  
    > [!NOTE]  
    >  패키지 수준에서만 로그를 만들 수 있습니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](#ssdt)을 참조하세요.  
  
5.  **자세히** 탭을 클릭하고 **로드**를 클릭합니다.  
  
6.  사용할 로깅 구성 파일을 찾고 **열기**를 클릭합니다.  
  
7.  필요에 따라 **이벤트** 열에서 해당 확인란을 선택하여 기록할 다른 로그 항목을 선택합니다. **고급** 을 클릭하여 이 항목에 대해 기록할 정보 유형을 선택합니다.  
  
    > [!NOTE]  
    >  새 컨테이너는 원래 로깅 구성을 만드는 데 사용된 컨테이너에는 사용할 수 없는 추가 로그 항목을 포함할 수 있습니다. 이러한 추가 로그 항목을 로그하려면 수동으로 선택해야 합니다.  
  
8.  로깅 구성의 업데이트된 버전을 저장하려면 **저장**을 클릭합니다.  
  
9. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="server_logging"></a> Enable Logging for Package Execution on the SSIS Server
  이 항목에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 패키지를 실행할 때 패키지의 로깅 수준을 설정하거나 변경하는 방법에 대해 설명합니다. 패키지를 실행할 때 설정하는 로깅 수준에 따라 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 디자인 타임 시 구성하는 패키지 로깅이 재정의됩니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](#ssdt) 을 참조하세요.  
  
 SQL Server **서버 속성**의 **서버 로깅 수준** 속성에서 기본 서버 차원의 로깅 수준을 선택할 수 있습니다. 이 항목에서 설명하는 기본 제공 로깅 수준 중 하나에서 선택하거나 기존 사용자 지정된 로깅 수준을 선택할 수 있습니다. 선택한 로깅 수준은 기본적으로 SSIS 카탈로그에 배포되는 모든 패키지에 적용됩니다. 또한 SSIS 패키지를 실행하는 SQL 에이전트 작업 단계에 기본적으로 적용됩니다.  
  
 다음 방법 중 하나를 사용하여 개별 패키지에 대한 로깅 수준을 지정할 수도 있습니다. 이 항목에는 첫 번째 방법에 대해 설명합니다.  
  
-   패키지 실행 대화 상자를 사용하여 패키지 실행 인스턴스 구성  
  
-   [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)를 사용하여 실행 인스턴스에 대한 매개 변수 설정  
  
-   새 작업 단계 대화 상자를 사용하여 패키지 실행에 대한 SQL Server 에이전트 작업 구성  
  
### <a name="set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>패키지 실행 대화 상자를 사용하여 패키지의 로깅 수준 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 패키지로 이동합니다.  
  
2.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 선택합니다.  
  
3.  **패키지 실행** 대화 상자에서 **고급** 탭을 선택합니다.  
  
4.  **로깅 수준**에서 로깅 수준을 선택합니다. 이 항목은 사용 가능한 값에 대한 설명을 포함합니다.  
  
5.  다른 모든 패키지 구성을 완료한 다음 **확인** 을 클릭하여 패키지를 실행합니다.  
  
### <a name="select-a-logging-level"></a>로깅 수준 선택  
 다음 기본 제공 로깅 수준을 사용할 수 있습니다. 또한 기존 사용자 지정된 로깅 수준을 선택할 수 있습니다. 이 항목은 사용자 지정된 로깅 수준에 대한 설명을 포함합니다.  
  
|로깅 수준|Description|  
|-------------------|-----------------|  
|InclusionThresholdSetting|로깅이 해제됩니다. 패키지 실행 상태에만 기록됩니다.|  
|Basic|사용자 지정 이벤트 및 진단 이벤트 외의 모든 이벤트가 기록됩니다. 이것은 기본값입니다.|  
|RuntimeLineage|데이터 흐름에서 계보 정보를 추적하는 데 필요한 데이터를 수집합니다. 이 계보 정보를 구문 분석하여 작업 간의 계보 관계를 매핑할 수 있습니다. ISV 및 개발자는 이 정보를 사용하여 사용자 지정 계보 매핑 도구를 빌드할 수 있습니다.|  
|성능|성능 통계와 OnError 및 OnWarning 이벤트만 기록됩니다.<br /><br /> **실행 성능** 보고서에는 패키지 데이터 흐름 구성 요소의 활성 시간 및 총 시간이 표시됩니다. 이 정보는 마지막 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에 사용할 수 있습니다. 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)을(를) 참조하세요.<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) 뷰에는 각 실행 단계의 데이터 흐름 구성 요소에 대한 시작 시간과 종료 시간이 표시됩니다. 이 뷰에서는 패키지 실행의 로깅 수준이 **성능** 또는 **자세히**로 설정된 경우에만 해당 구성 요소에 대해 이 정보를 표시합니다.|  
|자세히|사용자 지정 이벤트 및 진단 이벤트를 포함한 모든 이벤트가 기록됩니다.<br /><br /> 사용자 지정 이벤트로는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 태스크에 의해 기록되는 이벤트가 있습니다. 사용자 지정 이벤트에 대한 자세한 내용은 [Custom Messages for Logging](#custom_messages)을(를) 참조하세요.<br /><br /> 진단 이벤트의 한 예로 **DiagnosticEx** 이벤트가 있습니다. 패키지 실행 태스크가 자식 패키지를 실행할 때마다 이 이벤트는 자식 패키지에 전달된 매개 변수 값을 캡처합니다.<br /><br /> 또한 **DiagnosticEx** 이벤트는 행 수준 오류가 발생하는 열의 이름을 가져올 수 있습니다. 이 이벤트는 로그에 데이터 흐름 계보 지도를 작성합니다. 그런 다음 오류 출력에 의해 캡처된 열 식별자를 사용하여 이 계보 맵에서 열 이름을 조회할 수 있습니다.  자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.<br /><br /> **DiagnosticEx** 에 대한 메시지 열 값은 XML 텍스트입니다. 패키지 실행에 대한 메시지 텍스트를 보려면 [catalog.operation_messages&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) 뷰를 쿼리합니다. **DiagnosticEx** 이벤트는 로그의 크기를 줄이기 위해 해당 XML 출력에서 공백을 유지하지 않습니다. 가독성을 높이기 위해 XML 서식 지정 및 구문 강조를 지원하는 XML 편집기(예: Visual Studio)로 로그를 복사합니다.<br /><br /> [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) 뷰는 패키지 실행에 대해 데이터 흐름 구성 요소가 다운스트림 구성 요소에 데이터를 전송할 때마다 행을 표시합니다. 뷰에서 이 정보를 캡처하려면 로깅 수준을 **자세히** 로 설정해야 합니다.|  
  
### <a name="create-and-manage-customized-logging-levels-by-using-the-customized-logging-level-management-dialog-box"></a>사용자 지정된 로깅 수준 관리 대화 상자를 사용하여 사용자 지정된 로깅 수준 만들기 및 관리  
 원하는 통계 및 이벤트를 수집하는 사용자 지정된 로깅 수준을 만들 수 있습니다. 필요에 따라 변수 값, 연결 문자열 및 구성 요소 속성을 포함하는 이벤트의 컨텍스트를 캡처할 수도 있습니다. 패키지를 실행하는 경우 기본 제공 로깅 수준을 선택할 수 있을 때마다 사용자 지정된 로깅 수준을 선택할 수 있습니다.  
  
> [!TIP]  
>  패키지 변수 값을 캡처하려면 변수의 **IncludeInDebugDump** 속성을 **True**로 설정해야 합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용자 지정된 로깅 수준을 만들고 관리하려면 SSISDB 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **사용자 지정된 로깅 수준** 을 선택하여 **사용자 지정된 로깅 수준 관리** 대화 상자를 엽니다. **사용자 지정된 로깅 수준** 목록은 모든 기존 사용자 지정된 로깅 수준을 포함합니다.  
  
2.  새 사용자 지정된 로깅 수준을 **만들려면** **만들기**를 클릭한 다음 이름 및 설명을 제공합니다. **통계** 및 **이벤트** 탭에서 수집하려는 통계 및 이벤트를 선택합니다. **이벤트** 탭에서 필요에 따라 개별 이벤트에 **컨텍스트 포함** 을 선택합니다. 그런 다음 **저장**을 클릭합니다.  
  
3.  기존 사용자 지정된 로깅 수준을 **업데이트** 하려면 목록에서 선택하고 다시 구성한 다음 **저장**을 클릭합니다.  
  
4.  기존 사용자 지정된 로깅 수준을 **삭제** 하려면 목록에서 선택한 다음 **삭제**를 클릭합니다.  
  
 **사용자 지정된 로깅 수준에 대한 권한.**  
  
-   SSISDB 데이터베이스의 모든 사용자는 사용자 지정된 로깅 수준을 보고 패키지를 실행할 때 사용자 지정된 로깅 수준을 선택할 수 있습니다.  
  
-   ssis_admin 또는 sysadmin 역할의 사용자만 사용자 지정된 로깅 수준을 만들고 업데이트 또는 삭제할 수 있습니다.  

## <a name="custom_messages"></a> Custom Messages for Logging
SQL Server Integration Services는 패키지 및 여러 태스크에 대한 로그 항목 기록을 위해 다양한 사용자 지정 이벤트 집합을 제공합니다. 이러한 항목을 사용하면 나중에 분석할 수 있도록 미리 정의된 이벤트나 사용자가 정의한 메시지를 기록하여 실행 진행률, 결과 및 문제에 대한 세부 정보를 저장할 수 있습니다. 예를 들면 대량 삽입이 시작되고 끝나는 시간을 기록하여 패키지 실행 시 성능 문제를 식별할 수 있습니다.  
  
 사용자 지정 로그 항목은 패키지 및 모든 컨테이너와 태스크에 사용할 수 있는 표준 로깅 이벤트 집합과는 다른 항목 집합입니다. 사용자 지정 로그 항목은 패키지의 특정 태스크에 대한 유용한 정보를 캡처하도록 조정되어 있습니다. 예를 들어 SQL 실행 태스크에 대한 사용자 지정 로그 항목 중 하나는 해당 태스크에서 실행한 SQL 문을 로그에 기록합니다.  
  
 모든 로그 항목에는 패키지가 시작되고 끝날 때 자동으로 기록되는 로그 항목을 비롯하여 날짜 및 시간 정보가 포함됩니다. 로그 이벤트는 대부분 여러 항목을 로그에 기록합니다. 일반적으로 이벤트에 여러 단계가 있을 경우 이러한 기록이 수행됩니다. 예를 들어 **ExecuteSQLExecutingQuery** 로그 이벤트는 3개의 항목을 기록합니다. 즉, 태스크에서 데이터베이스에 대한 연결을 설정한 후, 태스크에서 SQL 문 준비를 시작한 후, SQL 문 실행이 완료된 후에 각각 하나씩의 항목을 기록합니다.  
  
 다음 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체에는 사용자 지정 로그 항목이 있습니다.  
  
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
  
### <a name="log-entries"></a>로그 항목  
  
####  <a name="Package"></a> 패키지  
 다음 표에서는 패키지에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**PackageStart**|패키지 실행이 시작되었음을 나타냅니다. 이 로그 항목은 로그에 자동으로 기록되며 제외할 수 없습니다.|  
|**PackageEnd**|패키지가 완료되었음을 나타냅니다. 이 로그 항목은 로그에 자동으로 기록되며 제외할 수 없습니다.|  
|**진단**|동시에 실행될 수 있는 실행 파일 수처럼 패키지 실행에 영향을 주는 시스템 구성에 대한 정보를 제공합니다.<br /><br /> **Diagnostic** 로그 항목에는 외부 데이터 공급자에 대한 호출 전후 항목도 포함됩니다.|  
  
####  <a name="BulkInsert"></a> 대량 삽입 태스크  
 다음 표에서는 대량 삽입 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**DTSBulkInsertTaskBegin**|대량 삽입이 시작되었음을 나타냅니다.|  
|**DTSBulkInsertTaskEnd**|대량 삽입이 완료되었음을 나타냅니다.|  
|**DTSBulkInsertTaskInfos**|태스크에 대한 설명 정보를 제공합니다.|  
  
####  <a name="DataFlow"></a> 데이터 흐름 태스크  
 다음 표에서는 데이터 흐름 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**BufferSizeTuning**|데이터 흐름 태스크로 인해 버퍼 크기가 변경되었음을 나타냅니다. 로그 항목은 크기가 변경된 이유를 설명하고 임시 새 버퍼 크기를 나열합니다.|  
|**OnPipelinePostEndOfRowset**|구성 요소에 **ProcessInput** 메서드의 마지막 호출로 설정된 해당 행 집합 끝 신호를 제공했음을 나타냅니다. 입력을 처리하는 데이터 흐름의 각 구성 요소에 대한 항목이 기록됩니다. 이 항목은 구성 요소의 이름을 포함합니다.|  
|**OnPipelinePostPrimeOutput**|구성 요소가 **PrimeOutput** 메서드에 대한 마지막 호출을 완료했음을 나타냅니다. 데이터 흐름에 따라 여러 로그 항목이 기록될 수 있습니다. 구성 요소가 원본일 경우에는 구성 요소가 행 처리를 완료했음을 의미합니다.|  
|**OnPipelinePreEndOfRowset**|구성 요소가 **ProcessInput** 메서드의 마지막 호출로 설정된 해당 행 집합 끝 신호를 수신하려고 함을 나타냅니다. 입력을 처리하는 데이터 흐름의 각 구성 요소에 대한 항목이 기록됩니다. 이 항목은 구성 요소의 이름을 포함합니다.|  
|**OnPipelinePrePrimeOutput**|구성 요소가 **PrimeOutput** 메서드에서 해당 호출을 수신하려고 함을 나타냅니다. 데이터 흐름에 따라 여러 로그 항목이 기록될 수 있습니다.|  
|**OnPipelineRowsSent**|**ProcessInput** 메서드 호출로 구성 요소 입력에 제공한 행 수를 보고합니다. 이 로그 항목은 구성 요소 이름을 포함합니다.|  
|**PipelineBufferLeak**|버퍼 관리자가 없어진 후에 버퍼를 활성 상태로 유지하는 모든 구성 요소에 대한 정보를 제공합니다. 즉, 버퍼 리소스가 릴리스되지 않았기 때문에 메모리 손실이 발생할 수 있음을 나타냅니다. 로그 항목은 구성 요소 이름과 버퍼 ID를 제공합니다.|  
|**PipelineExecutionPlan**|데이터 흐름의 실행 계획을 보고합니다. 버퍼를 구성 요소로 전송하는 방법에 대한 정보를 제공합니다. 이 정보는 PipelineExecutionTrees 항목과 함께 태스크에서 발생하는 사항에 대해 설명합니다.|  
|**PipelineExecutionTrees**|데이터 흐름에서 레이아웃 실행 트리를 보고합니다. 데이터 흐름 엔진 스케줄러는 이 트리를 사용하여 데이터 흐름의 실행 계획을 작성합니다.|  
|**PipelineInitialization**|태스크에 대한 초기화 정보를 제공합니다. 이 정보에 BLOB 데이터의 임시 저장소에 사용할 디렉터리, 기본 버퍼 크기 및 버퍼의 행 수가 포함됩니다. 데이터 흐름 태스크의 구성에 따라 여러 로그 항목이 기록될 수 있습니다.|  
  
####  <a name="ExecuteDTS200"></a> DTS 2000 실행 태스크  
 다음 표에서는 DTS 2000 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ExecuteDTS80PackageTaskBegin**|태스크에서 DTS 2000 패키지 실행을 시작했음을 나타냅니다.|  
|**ExecuteDTS80PackageTaskEnd**|태스크가 완료되었음을 나타냅니다.<br /><br /> 참고: DTS 2000 패키지는 태스크가 끝난 후에도 계속 실행됩니다.|  
|**ExecuteDTS80PackageTaskTaskInfo**|태스크에 대한 설명 정보를 제공합니다.|  
|**ExecuteDTS80PackageTaskTaskResult**|태스크에서 실행한 DTS 2000 패키지의 실행 결과를 보고합니다.|  
  
####  <a name="ExecuteProcess"></a> 프로세스 실행 태스크  
 다음 표에서는 프로세스 실행 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|태스크에서 실행하도록 구성된 실행 파일의 실행 프로세스에 대한 정보를 제공합니다.<br /><br /> 두 개의 로그 항목이 기록됩니다. 한 항목에는 태스크가 실행하는 실행 파일의 이름과 위치에 대한 정보가 들어 있고 다른 항목은 실행 파일의 종료를 기록합니다.|  
|**ExecuteProcessVariableRouting**|실행 파일의 입력 및 출력으로 라우팅되는 변수에 대한 정보를 제공합니다. stdin(입력), stdout(출력) 및 stderr(오류 출력)에 대한 로그 항목이 기록됩니다.|  
  
####  <a name="ExecuteSQL"></a> SQL 실행 태스크  
 다음 표에서는 SQL 실행 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|SQL 문의 실행 단계에 대한 정보를 제공합니다. 로그 항목은 태스크에서 데이터베이스에 대한 연결을 설정할 때, 태스크에서 SQL 문 준비를 시작할 때 또는 SQL 문 실행이 완료된 후에 기록됩니다. 준비 단계에 대한 로그 항목은 태스크에서 사용하는 SQL 문을 포함합니다.|  
  
####  <a name="FileSystem"></a> 파일 시스템 태스크  
 다음 표에서는 파일 시스템 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|태스크에서 수행하는 작업을 보고합니다. 이 로그 항목은 파일 시스템 작업이 시작될 때 기록되며 원본 및 대상에 대한 정보를 포함합니다.|  
  
####  <a name="FTP"></a> FTP 태스크  
 다음 표에서는 FTP 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**FTPConnectingToServer**|태스크에서 FTP 서버에 대한 연결을 시작했음을 나타냅니다.|  
|**FTPOperation**|태스크에서 수행하는 FTP 작업의 시작 부분과 유형을 보고합니다.|  
  
####  <a name="MessageQueue"></a> 메시지 큐 태스크  
 다음 표에서는 메시지 큐 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**MSMQAfterOpen**|태스크에서 메시지 큐 열기를 완료했음을 나타냅니다.|  
|**MSMQBeforeOpen**|태스크에서 메시지 큐 열기를 시작했음을 나타냅니다.|  
|**MSMQBeginReceive**|태스크에서 메시지 받기를 시작했음을 나타냅니다.|  
|**MSMQBeginSend**|태스크에서 메시지 보내기를 시작했음을 나타냅니다.|  
|**MSMQEndReceive**|태스크에서 메시지 받기를 완료했음을 나타냅니다.|  
|**MSMQEndSend**|태스크에서 메시지 보내기를 완료했음을 나타냅니다.|  
|**MSMQTaskInfo**|태스크에 대한 설명 정보를 제공합니다.|  
|**MSMQTaskTimeOut**|태스크 시간이 초과되었음을 나타냅니다.|  
  
####  <a name="Script"></a> 스크립트 태스크  
 다음 표에서는 스크립트 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|스크립트에서 로깅을 구현한 결과를 보고합니다. **Log** 개체의 **Dts** 메서드 호출에 대해 각각 로그 항목이 기록됩니다. 이 항목은 코드가 실행되면 기록됩니다. 자세한 내용은 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)을(를) 참조하세요.|  
  
####  <a name="SendMail"></a> 메일 보내기 태스크  
 다음 표에서는 메일 보내기 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|태스크에서 전자 메일 메시지 보내기를 시작했음을 나타냅니다.|  
|**SendMailTaskEnd**|태스크에서 전자 메일 메시지 보내기를 완료했음을 나타냅니다.|  
|**SendMailTaskInfo**|태스크에 대한 설명 정보를 제공합니다.|  
  
####  <a name="TransferDatabase"></a> 데이터베이스 전송 태스크  
 다음 표에서는 데이터베이스 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**SourceDB**|태스크에서 복사한 데이터베이스를 지정합니다.|  
|**SourceSQLServer**|데이터베이스를 복사한 컴퓨터를 지정합니다.|  
  
####  <a name="TransferErrorMessages"></a> 오류 메시지 전송 태스크  
 다음 표에서는 오류 메시지 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**TransferErrorMessagesTaskFinishedTransferringObjects**|태스크에서 오류 메시지 전송을 완료했음을 나타냅니다.|  
|**TransferErrorMessagesTaskStartTransferringObjects**|태스크에서 오류 메시지 전송을 시작했음을 나타냅니다.|  
  
####  <a name="TransferJobs"></a> 작업 전송 태스크  
 다음 표에서는 작업 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**TransferJobsTaskFinishedTransferringObjects**|태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 전송을 완료했음을 나타냅니다.|  
|**TransferJobsTaskStartTransferringObjects**|태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 전송을 시작했음을 나타냅니다.|  
  
####  <a name="TransferLogins"></a> 로그인 전송 태스크  
 다음 표에서는 로그인 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**TransferLoginsTaskFinishedTransferringObjects**|태스크에서 로그인 전송을 완료했음을 나타냅니다.|  
|**TransferLoginsTaskStartTransferringObjects**|태스크에서 로그인 전송을 시작했음을 나타냅니다.|  
  
####  <a name="TransferMasterStoredProcedures"></a> Master 저장 프로시저 전송 태스크  
 다음 표에서는 Master 저장 프로시저 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**TransferStoredProceduresTaskFinishedTransferringObjects**|태스크에서 **master** 데이터베이스에 저장된 사용자 정의 저장 프로시저 전송을 완료했음을 나타냅니다.|  
|**TransferStoredProceduresTaskStartTransferringObjects**|태스크에서 **master** 데이터베이스에 저장된 사용자 정의 저장 프로시저 전송을 시작했음을 나타냅니다.|  
  
####  <a name="TransferSQLServerObjects"></a> SQL Server 개체 전송 태스크  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**TransferSqlServerObjectsTaskFinishedTransferringObjects**|태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체 전송을 완료했음을 나타냅니다.|  
|**TransferSqlServerObjectsTaskStartTransferringObjects**|태스크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체 전송을 시작했음을 나타냅니다.|  
  
####  <a name="WebServices"></a> 웹 서비스 태스크  
 다음 표에서는 웹 서비스 태스크에 사용할 수 있는 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|태스크에서 웹 서비스 액세스를 시작했습니다.|  
|**WSTaskEnd**|태스크에서 웹 서비스 메서드를 완료했습니다.|  
|**WSTaskInfo**|태스크에 대한 설명 정보입니다.|  
  
####  <a name="WMIDataReader"></a> WMI 데이터 판독기 태스크  
 다음 표에서는 WMI 데이터 판독기 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|태스크에서 WMI 데이터 읽기를 시작했음을 나타냅니다.|  
|**WMIDataReaderOperation**|태스크에서 실행한 WQL 쿼리를 보고합니다.|  
  
####  <a name="WMIEventWatcher"></a> WMI 이벤트 감시자 태스크  
 다음 표에서는 WMI 이벤트 감시자 태스크에 대한 사용자 지정 로그 항목을 나열합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|태스크에서 모니터링하고 있는 이벤트가 발생했음을 나타냅니다.|  
|**WMIEventWatcherTimedout**|태스크 시간이 초과되었음을 나타냅니다.|  
|**WMIEventWatcherWatchingForWMIEvents**|태스크에서 WQL 쿼리 실행을 시작했음을 나타냅니다. 이 항목은 해당 쿼리를 포함합니다.|  
  
####  <a name="XML"></a> XML 태스크  
 다음 표에서는 XML 태스크에 대한 사용자 지정 로그 항목을 설명합니다.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**XMLOperation**|태스크에서 수행한 작업에 대한 정보를 제공합니다.|  

## <a name="related-tasks"></a>관련 작업  
 다음 목록에는 로깅 기능과 관련된 태스크를 수행하는 방법을 보여 주는 항목에 대한 링크가 나와 있습니다.  
  
-   [Integration Services 패키지에서 기록하는 이벤트](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
## <a name="related-content"></a>관련 내용  
 [전체 및 세부 정보 로깅을 위한 DTLoggedExec 도구(CodePlex 프로젝트)](http://go.microsoft.com/fwlink/?LinkId=150579)  
