---
title: ADOMD.NET에서 보안 연결 설정 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b92b5b1bfdec6e311b93743d22cc990623315a9a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connections-in-adomdnet---establishing-secure-connections"></a>Connections in ADOMD.NET-보안 연결 설정
  연결에 사용 되는 보안 메서드는 값에 따라 ADOMD.NET에서 연결을 사용 하는 경우는 **ProtectionLevel** 호출할 때 사용 하는 연결 문자열의 속성은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 메서드는 의<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 **ProtectionLevel** 속성은 네 가지 보안 수준을: 인증 되지 않은, 인증, 서명 및 암호화 합니다. 다음 표에서는 이러한 여러 보안 수준에 대해 설명합니다.  
  
> [!NOTE]  
>  데이터베이스 연결 풀링을 사용하기로 선택한 경우에는 데이터베이스에서 보안을 관리할 수 없습니다. 이는 데이터베이스 연결 풀링을 사용하려면 연결 문자열이 풀 연결과 같아야 하기 때문입니다. 따라서 다른 곳에서 보안을 관리해야 합니다.  
  
|보안 수준|ProtectionLevel 값|  
|--------------------|---------------------------|  
|*인증 되지 않은 연결*<br /> 인증되지 않은 연결에는 인증 형식이 없습니다. 이 연결 유형은 가장 널리 지원되지만 보안 수준이 가장 낮은 연결 형식을 나타냅니다.|**없음**|  
|*인증 된 연결*<br /> 인증된 연결은 연결을 설정한 사용자를 인증합니다. 그러나 추가 보안 통신을 지원하지는 않습니다. 이 연결 유형은 분석 데이터 원본에 연결하고 있는 사용자 또는 응용 프로그램의 ID를 설정할 수 있을 때 유용합니다.|**Connect**|  
|*서명된 연결*<br /> 서명된 연결은 연결을 요청하는 사용자를 인증한 후 전송이 수정되지 않았는지 확인합니다. 이 연결 유형은 전송된 데이터의 신뢰성을 확인해야 하는 경우에 유용합니다. 서명된 연결에서는 데이터 패킷의 내용을 수정할 수 없지만 전송 중인 내용을 볼 수는 있습니다.<br /><br /><br /><br /> 서명 된 연결은 for Analysis 공급자에서 제공 하는 xml만 지원 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.|**Pkt 무결성** 또는 **PktIntegrity**|  
|*암호화 된 연결*<br /> 암호화된 연결은 ADOMD.NET에서 사용되는 기본 연결 유형입니다. 이 연결 유형은 연결을 요청하는 사용자를 인증한 후 전송되는 데이터를 암호화합니다. 암호화된 연결은 ADOMD.NET에서 만들 수 있는 연결 중 보안 수준이 가장 높은 연결입니다. 데이터 패킷의 내용을 보거나 수정할 수 없기 때문에 전송 중인 데이터를 안전하게 보호할 수 있습니다.<br /><br /><br /><br /> XML for Analysis 공급자에서 제공한 암호화 된 연결 에서만 지원 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.|**개인 정보 보호 Pkt** 또는 **PktPrivacy**|  
  
 모든 연결 유형에 모든 보안 수준을 사용할 수 있는 것은 아닙니다.  
  
-   TCP 연결은 네 가지 보안 수준 중 한 수준만 사용할 수 있습니다. 실제로 TCP 연결을 Windows 통합 보안과 함께 사용하게 되면 가장 높은 보안 수준으로 분석 데이터 원본에 연결할 수 있습니다.  
  
-   HTTP 연결은 인증된 연결만 가능합니다. 따라서는 **ProtectionLevel** 속성으로 설정 되어 있어야 **연결**합니다.  
  
-   HTTPS 연결은 암호화된 연결만 가능합니다. 따라서는 **ProtectionLevel** 속성으로 설정 되어 있어야 **Pkt 개인 정보 보호** 또는 **PktPrivacy**합니다.  
  
## <a name="securing-tcp-connections"></a>TCP 연결 보안 설정  
 TCP 연결에 대 한는 **ProtectionLevel** 속성 다음 표에 나열 된 네 가지 보안 수준을 모두 지원 합니다.  
  
|ProtectionLevel 값|TCP 연결 사용 여부|결과|  
|---------------------------|------------------------------|-------------|  
|**없음**|예|인증되지 않은 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청하지만 해당 스트림을 요청하는 사용자에 대해 수행되는 인증 형식이 없습니다.|  
|**Connect**|예|인증된 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청 하는 사용자의 보안 컨텍스트가 서버에 대해 인증 됩니다 및: 없는 다른 작업을 수행 하는 인증에 성공 하는 경우. 인증이 실패하면 다차원 데이터 원본으로부터 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 연결이 끊어지고 예외가 throw됩니다.<br /><br /> 인증이 성공 또는 실패한 후 연결을 인증하는 데 사용된 보안 컨텍스트는 삭제됩니다.|  
|**Pkt 무결성** 또는 **PktIntegrity**|예|서명된 연결을 지정합니다.<br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청하는 사용자의 보안 컨텍스트가 서버에 대해 인증됩니다.<br /><br /> <br /><br /> 인증이 성공하면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체가 기존 TCP 스트림을 닫은 후 서명된 TCP 스트림을 열어서 모든 요청을 처리합니다. 데이터 또는 메타데이터에 대한 각 요청은 연결을 여는 데 사용된 보안 컨텍스트를 사용하여 인증됩니다. 또한 각 패킷은 TCP 패킷의 페이로드가 변경되지 않았음을 보장하기 위해 디지털 서명됩니다.<br /><br /> <br /><br /> 인증이 실패하면 다차원 데이터 원본으로부터 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 연결이 끊어지고 예외가 throw됩니다.|  
|**개인 정보 보호 Pkt** 또는 **PktPrivacy**|예|암호화된 연결을 지정합니다.<br /><br /> <br /><br /> 설정 하지 않으면 암호화 된 연결을도 지정할 수는 **ProtectionLevel** 연결 문자열의 속성입니다.<br /><br /> <br /><br /> 공급자에서 TCP 스트림을 요청한 후 해당 스트림을 요청하는 사용자의 보안 컨텍스트가 서버에 대해 인증됩니다.<br /><br /> <br /><br /> 인증이 성공하면 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체가 기존 TCP 스트림을 닫은 후 암호화된 TCP 스트림을 열어서 모든 요청을 처리합니다. 데이터 또는 메타데이터에 대한 각 요청은 연결을 여는 데 사용된 보안 컨텍스트를 사용하여 인증됩니다. 또한 각 TCP 패킷의 페이로드는 공급자와 다차원 데이터 원본에서 지원되는 최고 수준의 암호화 방법을 사용하여 암호화됩니다.<br /><br /> <br /><br /> 인증이 실패하면 다차원 데이터 원본으로부터 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 연결이 끊어지고 예외가 throw됩니다.|  
  
### <a name="using-windows-integrated-security-for-the-connection"></a>연결에 Windows 통합 보안 사용  
 Windows 통합 보안은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 연결을 가장 높은 보안 수준으로 설정할 수 있는 방법입니다. Windows 통합 보안은 인증 프로세스 동안 사용자 이름 또는 암호 같은 보안 자격 증명을 노출하지 않고 대신 현재 실행 중인 프로세스의 보안 식별자를 사용하여 ID를 설정합니다. 대부분의 클라이언트 응용 프로그램에서 이 보안 식별자는 현재 로그온한 사용자의 ID를 나타냅니다.  
  
 Windows 통합 보안을 사용하려면 연결 문자열을 다음과 같이 설정해야 합니다.  
  
-   에 대 한는 **통합 보안** 속성을이 속성을 설정 하거나이 속성을 설정 하지 마십시오 어느 **SSPI**합니다.  
  
    > [!NOTE]  
    >  HTTP 연결을 사용 해야 하므로 Windows 통합 보안은 TCP 연결에 사용할 수만 **기본** 에 대 한 설정에서 **통합 보안** 속성입니다.  
  
-   에 대 한는 **ProtectionLevel** 이 속성을 설정 하는 속성을 **연결**, **Pkt 무결성**, 또는 **Pkt 개인 정보 보호**합니다.  
  
## <a name="securing-http-connections"></a>HTTP 연결 보안 설정  
 HTTPS 및 SSL(Secure Sockets Layer)은 분석 데이터 원본과의 HTTP 통신을 외부에서 보안 설정하는 데 사용할 수 있습니다.  
  
 XMLA 공급자가 보안 HTTP만을 사용하므로 ADOMD.NET의 HTTP 연결은 다음 표와 같이 서명된 연결이어야 합니다.  
  
|ProtectionLevel 값|HTTP 또는 HTTPS 사용|  
|---------------------------|----------------------------|  
|**없음**|아니요|  
|**Connect**|HTTP|  
|**Pkt 무결성** 또는 **PktIntegrity**|아니요|  
|**개인 정보 보호 Pkt** 또는 **PktPrivacy**|HTTPS|  
  
### <a name="opening-a-secure-http-connection"></a>보안 HTTP 연결 열기  
 다음 예제에서는 ADOMD.NET을 사용 하 여 열에 대 한 HTTP 연결 하는 **AdventureWorksAS** 샘플 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스:  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [ADOMD.NET에서 연결 설정](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
  
