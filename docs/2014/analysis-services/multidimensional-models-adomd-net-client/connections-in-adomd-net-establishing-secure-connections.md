---
title: ADOMD.NET에서 보안 연결 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- connections [ADOMD.NET]
- security [ADOMD.NET]
ms.assetid: b084d447-1456-45a4-8e0e-746c07d7d6fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b77fefaad8ac573e526412f1c81be3969743a3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178213"
---
# <a name="establishing-secure-connections-in-adomdnet"></a>ADOMD.NET에서 보안 연결 설정
  ADOMD.NET에서 연결을 사용하는 경우 연결에 사용되는 보안 메서드는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A>의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 메서드를 호출할 때 사용되는 연결 문자열의 `ProtectionLevel` 속성 값에 따라 결정됩니다.  
  
 `ProtectionLevel` 속성 네 가지 보안 수준을 제공 합니다: 인증 되지 않은, 인증, 서명 및 암호화 합니다. 다음 표에서는 이러한 여러 보안 수준에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터베이스 연결 풀링을 사용하기로 선택한 경우에는 데이터베이스에서 보안을 관리할 수 없습니다. 이는 데이터베이스 연결 풀링을 사용하려면 연결 문자열이 풀 연결과 같아야 하기 때문입니다. 따라서 다른 곳에서 보안을 관리해야 합니다.  
  
|보안 수준|ProtectionLevel 값|  
|--------------------|---------------------------|  
|*인증 되지 않은 연결*<br /> 인증되지 않은 연결에는 인증 형식이 없습니다. 이 연결 유형은 가장 널리 지원되지만 보안 수준이 가장 낮은 연결 형식을 나타냅니다.|`None`|  
|*인증 된 연결*<br /> 인증된 연결은 연결을 설정한 사용자를 인증합니다. 그러나 추가 보안 통신을 지원하지는 않습니다. 이 연결 유형은 분석 데이터 원본에 연결하고 있는 사용자 또는 응용 프로그램의 ID를 설정할 수 있을 때 유용합니다.|`Connect`|  
|*서명 된 연결*<br /> 서명된 연결은 연결을 요청하는 사용자를 인증한 후 전송이 수정되지 않았는지 확인합니다. 이 연결 유형은 전송된 데이터의 신뢰성을 확인해야 하는 경우에 유용합니다. 서명된 연결에서는 데이터 패킷의 내용을 수정할 수 없지만 전송 중인 내용을 볼 수는 있습니다. **참고:** XML for Analysis 공급자에서 제공 하는 서명 된 연결 에서만 지원 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.|`Pkt Integrity` 또는 `PktIntegrity`|  
|*암호화 된 연결*<br /> 암호화된 연결은 ADOMD.NET에서 사용되는 기본 연결 유형입니다. 이 연결 유형은 연결을 요청하는 사용자를 인증한 후 전송되는 데이터를 암호화합니다. 암호화된 연결은 ADOMD.NET에서 만들 수 있는 연결 중 보안 수준이 가장 높은 연결입니다. 데이터 패킷의 내용을 보거나 수정할 수 없기 때문에 전송 중인 데이터를 안전하게 보호할 수 있습니다. **참고:** XML for Analysis 공급자에서 제공 하는 암호화 된 연결 에서만 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.|`Pkt Privacy` 또는 `PktPrivacy`|  
  
 모든 연결 유형에 모든 보안 수준을 사용할 수 있는 것은 아닙니다.  
  
-   TCP 연결은 네 가지 보안 수준 중 한 수준만 사용할 수 있습니다. 실제로 TCP 연결을 Windows 통합 보안과 함께 사용하게 되면 가장 높은 보안 수준으로 분석 데이터 원본에 연결할 수 있습니다.  
  
-   HTTP 연결은 인증된 연결만 가능합니다. 따라서 `ProtectionLevel` 속성을 `Connect`로 설정해야 합니다.  
  
-   HTTPS 연결은 암호화된 연결만 가능합니다. 따라서 `ProtectionLevel` 속성을 `Pkt Privacy` 또는 `PktPrivacy`로 설정해야 합니다.  
  
## <a name="securing-tcp-connections"></a>TCP 연결 보안 설정  
 TCP 연결의 경우 `ProtectionLevel` 속성은 다음 표에 나열된 네 가지 보안 수준을 모두 지원합니다.  
  
|ProtectionLevel 값|TCP 연결 사용 여부|결과|  
|---------------------------|------------------------------|-------------|  
|`None`|사용자 계정 컨트롤|인증되지 않은 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청하지만 해당 스트림을 요청하는 사용자에 대해 수행되는 인증 형식이 없습니다.|  
|`Connect`|사용자 계정 컨트롤|인증된 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청하는 사용자의 보안 컨텍스트가 서버에 대해 인증됩니다.<br /><br /> -인증에 성공 하는 경우 아무런 다른 동작이 발생 합니다.<br />-인증에 실패 하는 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체 다차원 데이터 원본에서 연결이 끊어지고 예외가 throw 됩니다.<br /><br /> 인증이 성공 또는 실패한 후 연결을 인증하는 데 사용된 보안 컨텍스트는 삭제됩니다.|  
|`Pkt Integrity` 또는 `PktIntegrity`|사용자 계정 컨트롤|서명된 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청하는 사용자의 보안 컨텍스트가 서버에 대해 인증됩니다.<br /><br /> -인증에 성공 하는 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체가 기존 TCP 스트림을 닫은 서명 된 TCP 스트림을 열어서 모든 요청을 처리 합니다. 데이터 또는 메타데이터에 대한 각 요청은 연결을 여는 데 사용된 보안 컨텍스트를 사용하여 인증됩니다. 또한 각 패킷은 TCP 패킷의 페이로드가 변경되지 않았음을 보장하기 위해 디지털 서명됩니다.<br />-인증에 실패 하는 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체 다차원 데이터 원본에서 연결이 끊어지고 예외가 throw 됩니다.|  
|`Pkt Privacy` 또는 `PktPrivacy`|사용자 계정 컨트롤|암호화된 연결을 지정합니다. **참고:** 설정 하지 않으면 암호화 된 연결을 지정할 수도 있습니다는 `ProtectionLevel` 연결 문자열에는 속성입니다. <br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청하는 사용자의 보안 컨텍스트가 서버에 대해 인증됩니다.<br /><br /> -인증에 성공 하는 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체가 기존 TCP 스트림을 닫은 후 열어서 암호화 된 TCP 스트림을 모든 요청을 처리 합니다. 데이터 또는 메타데이터에 대한 각 요청은 연결을 여는 데 사용된 보안 컨텍스트를 사용하여 인증됩니다. 또한 각 TCP 패킷의 페이로드는 공급자와 다차원 데이터 원본에서 지원되는 최고 수준의 암호화 방법을 사용하여 암호화됩니다.<br />-인증에 실패 하는 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체 다차원 데이터 원본에서 연결이 끊어지고 예외가 throw 됩니다.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>연결에 Windows 통합 보안 사용  
 Windows 통합 보안은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 가장 높은 보안 수준으로 설정할 수 있는 방법입니다. Windows 통합 보안은 인증 프로세스 동안 사용자 이름 또는 암호 같은 보안 자격 증명을 노출하지 않고 대신 현재 실행 중인 프로세스의 보안 식별자를 사용하여 ID를 설정합니다. 대부분의 클라이언트 응용 프로그램에서 이 보안 식별자는 현재 로그온한 사용자의 ID를 나타냅니다.  
  
 Windows 통합 보안을 사용하려면 연결 문자열을 다음과 같이 설정해야 합니다.  
  
-   `Integrated Security` 속성의 경우 이 속성을 설정하지 않거나 `SSPI`로 설정합니다.  
  
    > [!NOTE]  
    >  HTTP 연결에서 `Basic` 속성에 대해 `Integrated Security` 설정을 사용해야 하므로 Windows 통합 보안은 TCP 연결에만 사용할 수 있습니다.  
  
-   `ProtectionLevel` 속성의 경우 이 속성을 `Connect`, `Pkt Integrity` 또는 `Pkt Privacy`로 설정합니다.  
  
## <a name="securing-http-connections"></a>HTTP 연결 보안 설정  
 HTTPS 및 SSL(Secure Sockets Layer)은 분석 데이터 원본과의 HTTP 통신을 외부에서 보안 설정하는 데 사용할 수 있습니다.  
  
 XMLA 공급자가 보안 HTTP만을 사용하므로 ADOMD.NET의 HTTP 연결은 다음 표와 같이 서명된 연결이어야 합니다.  
  
|ProtectionLevel 값|HTTP 또는 HTTPS 사용|  
|---------------------------|----------------------------|  
|`None`|아니요|  
|`Connect`|HTTP|  
|`Pkt Integrity` 또는 `PktIntegrity`|아니요|  
|`Pkt Privacy` 또는 `PktPrivacy`|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>보안 HTTP 연결 열기  
 다음 예제에서는 ADOMD.NET을 사용하여 `AdventureWorksAS` 예제 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 HTTP 연결을 여는 방법을 보여 줍니다.  
  
```vb  
Public Function GetAWEncryptedConnection( _  
    Optional ByVal serverName As String = "https:\\localhost\isapy\msmdpump.dll") _  
    As AdomdConnection  
  
    Dim strConnectionString As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' To establish an encrypted connection, set the   
        ' ProtectionLevel setting to PktPrivacy.  
        strConnectionString = "DataSource=" & serverName & ";" & _  
            "Catalog=AdventureWorksAS;" & _  
            "ProtectionLevel=PktPrivacy;"  
  
        ' Note that username and password are not supplied here.  
        ' The current security context is used for authentication  
        ' purposes.  
  
        objConnection.ConnectionString = strConnectionString  
        objConnection.Open()  
    Catch ex As Exception  
        objConnection = Nothing  
        Throw ex  
    Finally  
        ' Return the encrypted connection.  
        GetAWEncryptedConnection = objConnection  
    End Try  
End Function  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET에서 연결 설정](connections-in-adomd-net.md)  
  
  
