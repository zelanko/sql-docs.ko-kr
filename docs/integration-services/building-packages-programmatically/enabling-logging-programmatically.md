---
title: "프로그래밍 방식으로 로깅 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: dd512f022832b57aa3fdcb85260926dd8354298c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="enabling-logging-programmatically"></a>프로그래밍 방식으로 로깅 설정
  런타임 엔진에서는 패키지의 유효성 검사 및 실행 중에 이벤트 관련 정보를 캡처하는 데 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 개체의 컬렉션을 제공합니다. <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 개체는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>, <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> 개체를 비롯하여 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 개체에서 사용할 수 있습니다. 개별 컨테이너나 패키지 전체에 대해 로깅 기능을 사용하도록 설정할 수 있습니다.  
  
 컨테이너에서 사용할 수 있는 로그 공급자에는 여러 유형이 있습니다. 따라서 여러 형식으로 로그 정보를 만들고 저장할 수 있는 유연성이 있습니다. 컨테이너 개체를 로깅에 참여시키는 과정은 먼저 로깅을 활성화한 후 로그 공급자를 선택하는 두 단계로 이루어집니다. 컨테이너의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성은 로깅되는 이벤트를 지정하고 로그 공급자를 선택하는 데 사용됩니다.  
  
## <a name="enabling-logging"></a>로깅 설정  
 로깅을 수행할 수 있는 각 컨테이너에 있는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성은 컨테이너의 이벤트 정보를 이벤트 로그에 기록할지 여부를 결정합니다. 이 속성은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 구조의 값을 할당받으며 기본적으로 컨테이너의 부모에서 상속됩니다. 컨테이너는 패키지, 부모가 없는 경우 속성 사용의 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>, 데이터베이스가 기본 인 **비활성화**합니다.  
  
### <a name="selecting-a-log-provider"></a>로그 공급자 선택  
 후의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 속성 **Enabled**, 로그 공급자에 추가 됩니다는 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 프로세스를 완료 하려면 컨테이너의 컬렉션입니다. <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 컬렉션은 <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> 개체에서 사용할 수 있으며 컨테이너에 대해 선택된 로그 공급자를 포함합니다. <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> 메서드는 공급자를 만들어 컬렉션에 추가하기 위해 호출됩니다. 그런 다음 이 메서드는 컬렉션에 추가된 로그 공급자를 반환합니다. 각 공급자에는 해당 공급자에 고유한 구성 설정이 있으며 이러한 속성은 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 속성을 사용하여 설정됩니다.  
  
 다음 표에는 사용할 수 있는 로그 공급자, 해당 설명 및 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 정보가 나열되어 있습니다.  
  
|공급자|Description|ConfigString 속성|  
|--------------|-----------------|---------------------------|  
|SQL Server 프로파일러|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로파일러에서 캡처하고 볼 수 있는 SQL 추적을 생성합니다. 이 공급자의 기본 파일 이름 확장명은 .trc입니다.|구성이 필요하지 않습니다.|  
|SQL Server|이벤트 로그 항목을 기록는 **sysssislog** 테이블에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자를 사용하려면 데이터베이스에 대한 연결과 대상 데이터베이스 이름이 지정되어 있어야 합니다.|  
|텍스트 파일|이벤트 로그 항목을 CSV(쉼표로 구분된 값) 형식으로 ASCII 텍스트 파일에 기록합니다. 이 공급자의 기본 파일 이름 확장명은 .log입니다.|파일 연결 관리자의 이름입니다.|  
|Windows 이벤트 로그|로컬 컴퓨터의 응용 프로그램 로그에 있는 표준 Windows 이벤트 로그에 로깅합니다.|구성이 필요하지 않습니다.|  
|XML 파일|이벤트 로그 항목을 XML 형식의 파일에 씁니다. 이 공급자의 기본 파일 이름 확장명은 .xml입니다.|파일 연결 관리자의 이름입니다.|  
  
 이벤트 로그에 포함 하거나 설정 하 여 이벤트 로그에서 제외 된 **EventFilterKind** 및 **EventFilter** 컨테이너의 속성입니다. **EventFilterKind** 두 값을 포함 하는 구조 **ExclusionFilter** 및 **InclusionFilter**, 이벤트는 지를 나타내는에 추가 **EventFilter** 이벤트 로그에 포함 됩니다. **EventFilter** 속성은 필터링의 주체인 이벤트의 이름을 포함 하는 문자열 배열을 할당 됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
