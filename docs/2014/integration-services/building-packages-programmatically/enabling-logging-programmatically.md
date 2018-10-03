---
title: 프로그래밍 방식으로 로깅 설정 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9fa879258a588c944c9d4c35954845cde767e626
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103663"
---
# <a name="enabling-logging-programmatically"></a>프로그래밍 방식으로 로깅 설정
  런타임 엔진에서는 패키지의 유효성 검사 및 실행 중에 이벤트 관련 정보를 캡처하는 데 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 개체의 컬렉션을 제공합니다. <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 개체는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>, <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> 개체를 비롯하여 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 개체에서 사용할 수 있습니다. 개별 컨테이너나 패키지 전체에 대해 로깅 기능을 사용하도록 설정할 수 있습니다.  
  
 컨테이너에서 사용할 수 있는 로그 공급자에는 여러 유형이 있습니다. 따라서 여러 형식으로 로그 정보를 만들고 저장할 수 있는 유연성이 있습니다. 컨테이너 개체를 로깅에 참여시키는 과정은 먼저 로깅을 활성화한 후 로그 공급자를 선택하는 두 단계로 이루어집니다. 컨테이너의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성은 로깅되는 이벤트를 지정하고 로그 공급자를 선택하는 데 사용됩니다.  
  
## <a name="enabling-logging"></a>로깅 설정  
 로깅을 수행할 수 있는 각 컨테이너에 있는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성은 컨테이너의 이벤트 정보를 이벤트 로그에 기록할지 여부를 결정합니다. 이 속성은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 구조의 값을 할당받으며 기본적으로 컨테이너의 부모에서 상속됩니다. 컨테이너가 패키지라서 부모가 없는 경우 이 속성은 기본값이 `Disabled`인 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>을 사용합니다.  
  
### <a name="selecting-a-log-provider"></a>로그 공급자 선택  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성이 `Enabled`로 설정되면 컨테이너의 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 컬렉션에 로그 공급자가 추가되면서 프로세스가 완료됩니다. <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 컬렉션은 <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> 개체에서 사용할 수 있으며 컨테이너에 대해 선택된 로그 공급자를 포함합니다. <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> 메서드는 공급자를 만들어 컬렉션에 추가하기 위해 호출됩니다. 그런 다음 이 메서드는 컬렉션에 추가된 로그 공급자를 반환합니다. 각 공급자에는 해당 공급자에 고유한 구성 설정이 있으며 이러한 속성은 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 속성을 사용하여 설정됩니다.  
  
 다음 표에는 사용할 수 있는 로그 공급자, 해당 설명 및 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 정보가 나열되어 있습니다.  
  
|공급자|Description|ConfigString 속성|  
|--------------|-----------------|---------------------------|  
|SQL Server 프로파일러|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로파일러에서 캡처하고 볼 수 있는 SQL 추적을 생성합니다. 이 공급자의 기본 파일 이름 확장명은 .trc입니다.|구성이 필요하지 않습니다.|  
|SQL Server|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 **sysssislog** 테이블에 이벤트 로그 항목을 기록합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자를 사용하려면 데이터베이스에 대한 연결과 대상 데이터베이스 이름이 지정되어 있어야 합니다.|  
|텍스트 파일|이벤트 로그 항목을 CSV(쉼표로 구분된 값) 형식으로 ASCII 텍스트 파일에 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .log입니다.|파일 연결 관리자의 이름입니다.|  
|Windows 이벤트 로그|로컬 컴퓨터의 응용 프로그램 로그에 있는 표준 Windows 이벤트 로그에 로깅합니다.|구성이 필요하지 않습니다.|  
|XML 파일|이벤트 로그 항목을 XML 형식의 파일에 씁니다. 이 공급자의 기본 파일 이름 확장명은 .xml입니다.|파일 연결 관리자의 이름입니다.|  
  
 컨테이너의 `EventFilterKind` 및 `EventFilter` 속성을 설정하여 이벤트를 이벤트 로그에 포함하거나 이벤트 로그에서 제외할 수 있습니다. `EventFilterKind` 구조에는 `ExclusionFilter`에 추가된 이벤트가 이벤트 로그에 포함되는지 여부를 나타내는 `InclusionFilter` 및 `EventFilter` 값이 들어 있습니다. `EventFilter` 속성에는 필터링 제목에 해당하는 이벤트 이름이 들어 있는 문자열 배열이 할당됩니다.  
  
 다음 코드에서는 패키지에 로깅 기능을 사용하도록 설정하고, <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 컬렉션에 텍스트 파일에 대한 로그 공급자를 추가하고, 로깅 출력에 포함할 이벤트 목록을 지정합니다.  
  
## <a name="sample"></a>예제  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정** <br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md)  
  
  
