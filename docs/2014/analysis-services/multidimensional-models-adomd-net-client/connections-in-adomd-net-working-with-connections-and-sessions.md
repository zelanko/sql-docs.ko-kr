---
title: ADOMD.NET에서 연결 및 세션 작업 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [ADOMD.NET]
- connections [ADOMD.NET]
ms.assetid: 72b43c06-f3e4-42c3-a696-4a3419c3b884
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 07c17333b58d34a99e8d393a1dbc8ec00d75f60e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172770"
---
# <a name="working-with-connections-and-sessions-in-adomdnet"></a>ADOMD.NET에서 연결 및 세션 작업
  XMLA(XML for Analysis)에서 세션은 분석 데이터 액세스 동안 상태 저장 작업에 필요한 지원을 제공합니다. 세션은 분석 데이터 원본에 대한 명령 및 트랜잭션의 범위와 컨텍스트를 지정합니다. 세션 관리에 사용되는 XMLA 요소로는 [BeginSession](../xmla/xml-elements-headers/beginsession-element-xmla.md), [Session](../xmla/xml-elements-headers/session-element-xmla.md)및 [EndSession](../xmla/xml-elements-headers/endsession-element-xmla.md)이 있습니다.  
  
 ADOMD.NET에서는 이러한 세 XMLA 세션 요소를 사용하여 세션을 시작하고, 세션 도중 쿼리를 수행하거나 데이터를 검색하고, 세션을 닫을 수 있습니다.  
  
## <a name="starting-a-session"></a>세션 시작  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 개체의 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 속성에는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체에 연결된 활성 세션의 식별자가 있습니다. 이 속성을 올바르게 사용하면 응용 프로그램에서 클라이언트 및 서버 상태 저장을 모두 효과적으로 제어할 수 있습니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 메서드를 호출할 때 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 속성이 유효한 세션 ID로 설정되어 있지 않은 경우 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체는 공급자에게 새 세션 ID를 요청합니다. ADOMD.NET에서는 XMLA `BeginSession` 헤더를 공급자에게 보내어 세션을 시작합니다. 세션이 성공적으로 시작되면 ADOMD.NET에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 속성의 값을 새로 만들어진 세션의 세션 ID로 설정합니다.  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 메서드를 호출할 때 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Open%2A> 속성이 유효한 세션 ID로 설정되어 있는 경우 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체는 지정된 세션에 연결하려고 시도합니다.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체가 지정된 세션에 연결할 수 없거나 공급자가 세션을 지원하지 않으면 예외가 throw됩니다.  
  
> [!NOTE]  
>  ADOMD.NET에서 세션을 만든 후에는 여러 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 하나의 해당 활성 세션에 연결하거나 단일 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체와 해당 세션의 연결을 끊고 해당 개체를 다른 세션에 다시 연결할 수 있습니다.  
  
## <a name="working-in-a-session"></a>세션 작업  
 ADOMD.NET에서는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 유효한 세션에 연결한 후 응용 프로그램에서 만들어진 데이터 또는 메타데이터에 대한 모든 요청이 포함된 XMLA `Session` 헤더를 공급자에게 보냅니다. 모든 요청에는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 속성의 값으로 설정된 세션 ID가 있습니다.  
  
 세션 ID는 세션이 계속 유효한 상태로 유지됨을 보장하지 않습니다. 세션이 만료된 경우(예를 들어, 세션의 시간이 초과되거나 연결이 끊어진 경우) 공급자는 해당 세션의 동작을 종료하고 롤백할 수 있습니다. 이 경우 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체의 후속 메서드를 호출하면 항상 예외가 throw됩니다. 세션이 만료될 때가 아니라 다음 요청이 공급자에게 전송될 때만 예외가 throw되므로 응용 프로그램에서 공급자의 데이터 또는 메타데이터를 검색할 때 이러한 예외를 처리할 수 있어야 합니다.  
  
## <a name="closing-a-session"></a>세션 닫기  
 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 메서드는 값을 지정 하지 않고는 *endSession* 매개 변수 또는 경우에는 *endSession* 매개 변수가 세션은 세션에 대 한 연결과 모두 True로 설정 된 와 연결 된는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체 닫힙니다. 세션을 닫기 위해 ADOMD.NET에서는 세션 ID가 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.SessionID%2A> 속성의 값으로 설정된 XMLA `EndSession` 헤더를 공급자에게 보냅니다.  
  
 경우는 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 메서드는 *endSession* 매개 변수가 False로 설정 되어 연관 된 세션에서 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 개체를 활성 상태로 유지 되지만 세션에 대 한 연결이 닫힙니다.  
  
## <a name="example-of-managing-a-session"></a>세션 관리 예  
 다음 예제에서는 ADOMD.NET에서 연결을 열고, 세션을 만들고, 세션을 열린 상태로 유지하면서 연결을 닫는 방법을 보여 줍니다.  
  
```vb  
Public Function CreateSession(ByVal connectionString As String) As String  
    Dim strSessionID As String = ""  
    Dim objConnection As New AdomdConnection  
  
    Try  
        ' First, try to connect to the specified data source.  
        ' If the connection string is not valid, or if the specified  
        ' provider does not support sessions, an exception is thrown.  
        objConnection.ConnectionString = connectionString  
        objConnection.Open()  
  
        ' Now that the connection is open, retrieve the new  
        ' active session ID.  
        strSessionID = objConnection.SessionID  
        ' Close the connection, but leave the session open.  
        objConnection.Close(False)  
        Return strSessionID  
  
    Finally  
        objConnection = Nothing  
    End Try  
End Function  
```  
  
```csharp  
static string CreateSession(string connectionString)  
{  
    string strSessionID = "";  
    AdomdConnection objConnection = new AdomdConnection();  
    try  
    {  
        /*First, try to connect to the specified data source.  
          If the connection string is not valid, or if the specified  
          provider does not support sessions, an exception is thrown. */  
        objConnection.ConnectionString = connectionString;  
        objConnection.Open();  
  
        // Now that the connection is open, retrieve the new  
        // active session ID.  
        strSessionID = objConnection.SessionID;  
        // Close the connection, but leave the session open.  
        objConnection.Close(false);  
        return strSessionID;  
    }  
    finally  
    {  
        objConnection = null;  
    }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [ADOMD.NET에서 연결 설정](connections-in-adomd-net.md)  
  
  