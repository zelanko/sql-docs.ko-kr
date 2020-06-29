---
title: 사용자 지정 로그 공급자 코딩 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom log providers [Integration Services], coding
ms.assetid: 979a29ca-956e-4fdd-ab47-f06e84cead7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3eaa589014bb866a7993b82c4f7b90ce7d0b42bd
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427490"
---
# <a name="coding-a-custom-log-provider"></a>사용자 지정 로그 공급자 코딩
  <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 기본 클래스에서 상속된 클래스를 만들고 이 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 특성을 적용한 후에는 기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공해야 합니다.  
  
 실제로 작동 중인 사용자 지정 로그 공급자의 예제를 보려면 [사용자 지정 로그 공급자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-log-provider.md)을 참조하세요.  
  
## <a name="configuring-the-log-provider"></a>로그 공급자 구성  
  
### <a name="initializing-the-log-provider"></a>로그 공급자 초기화  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.InitializeLogProvider%2A> 메서드를 재정의하여 연결 컬렉션 및 이벤트 인터페이스에 대한 참조를 캐시할 수 있습니다. 이렇게 캐시된 참조는 나중에 로그 공급자의 다른 메서드에서 사용할 수 있습니다.  
  
### <a name="using-the-configstring-property"></a>ConfigString 속성 사용  
 디자인 타임에 로그 공급자는 **구성** 열에서 구성 정보를 받습니다. 구성 정보는 로그 공급자의 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 속성에 해당합니다. 기본적으로 이 열에는 문자열 정보를 검색할 수 있는 입력란이 들어 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 포함된 대부분의 로그 공급자는 이 속성을 사용하여 해당 공급자가 외부 데이터 원본에 연결하는 데 사용하는 연결 관리자의 이름을 저장합니다. 로그 공급자가 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 속성을 사용하는 경우에는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 메서드를 사용하여 이 속성의 유효성을 검사하고 속성이 올바르게 설정되어 있는지 확인합니다.  
  
### <a name="validating-the-log-provider"></a>로그 공급자 유효성 검사  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 메서드를 재정의하여 로그 공급자가 올바르게 구성되어 있고 실행 준비가 되어 있는지 확인할 수 있습니다. 일반적으로 최소 수준의 유효성 검사는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>이 올바르게 설정되어 있는지 확인하는 것입니다. 로그 공급자가 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> 메서드에서 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A>를 반환하기 전까지는 실행을 계속할 수 없습니다.  
  
 다음 코드 예에서는 연결 관리자 이름이 지정되어 있고, 연결 관리자가 패키지에 있으며, 연결 관리자가 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Validate%2A> 속성에서 파일 이름을 반환하는지 확인하는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>의 구현을 보여 줍니다.  
  
```csharp  
public override DTSExecResult Validate(IDTSInfoEvents infoEvents)  
{  
    if (this.ConfigString.Length == 0 || connections.Contains(ConfigString) == false)  
    {  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
        return DTSExecResult.Failure;  
    }  
    else  
    {  
        string fileName = connections[ConfigString].AcquireConnection(null) as string;  
  
        if (fileName == null || fileName.Length == 0)  
        {  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0);  
            return DTSExecResult.Failure;  
        }  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As IDTSInfoEvents) As DTSExecResult  
    If Me.ConfigString.Length = 0 Or connections.Contains(ConfigString) = False Then  
        infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
        Return DTSExecResult.Failure  
    Else   
        Dim fileName As String =  connections(ConfigString).AcquireConnectionCType(as string, Nothing)  
  
        If fileName = Nothing Or fileName.Length = 0 Then  
            infoEvents.FireError(0, "MyTextLogProvider", "The ConnectionManager " + ConfigString + " specified in the ConfigString property cannot be found in the collection.", "", 0)  
            Return DTSExecResult.Failure  
        End If  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
### <a name="persisting-the-log-provider"></a>로그 공급자 지속  
 일반적으로 연결 관리자의 사용자 지정 지속성은 구현할 필요가 없습니다. 사용자 지정 지속성은 개체의 속성이 복합 데이터 형식을 사용할 때만 필요합니다. 자세한 내용은[Integration Services 사용자 지정 개체 개발](../developing-custom-objects-for-integration-services.md)을 참조하세요.  
  
## <a name="logging-with-the-log-provider"></a>로그 공급자를 사용하여 로깅  
 모든 로그 공급자는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 등의 런타임 메서드 세 개를 재정의해야 합니다.  
  
> [!IMPORTANT]  
>  단일 패키지의 유효성 검사 및 실행 중 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 메서드는 두 번 이상 호출됩니다. 사용자 지정 코드로 인해 다음에 로그를 열고 닫을 때 이전의 로그 항목을 덮어쓰지 않도록 해야 합니다. 테스트 패키지에서 유효성 검사 이벤트를 로깅하도록 선택한 경우 표시되는 첫 번째 로깅 이벤트는 OnPreValidate입니다. 이 이벤트 대신 PackageStart가 표시되는 첫 번째 로깅 이벤트인 경우에는 초기 유효성 검사 이벤트가 덮어쓰여진 것입니다.  
  
### <a name="opening-the-log"></a>로그 열기  
 대부분의 로그 공급자는 파일 또는 데이터베이스와 같은 외부 데이터 원본에 연결하여 패키지가 실행되는 동안 수집된 이벤트 정보를 저장합니다. 런타임의 다른 개체와 마찬가지로 외부 데이터 원본에 연결하는 작업은 일반적으로 연결 관리자 개체를 사용하여 수행됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 메서드는 패키지 실행이 시작될 때 호출되며, 이 메서드를 재정의하여 외부 데이터 원본에 대한 연결을 설정할 수 있습니다.  
  
 다음 예제 코드에서는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 실행 중에 텍스트 파일을 쓰기용으로 여는 로그 공급자를 보여 줍니다. 이 로그 공급자는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 속성에 지정된 연결 관리자의 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 메서드를 호출하여 파일을 엽니다.  
  
```csharp  
public override void OpenLog()  
{  
    if(!this.connections.Contains(this.ConfigString))  
        throw new Exception("The ConnectionManager " + this.ConfigString + " does not exist in the Connections collection.");  
  
    this.connectionManager = connections[ConfigString];  
    string filePath = this.connectionManager.AcquireConnection(null) as string;  
  
    if(filePath == null || filePath.Length == 0)  
        throw new Exception("The ConnectionManager " + this.ConfigString + " is not a valid FILE ConnectionManager");  
  
    //  Create a StreamWriter to append to.  
    sw = new StreamWriter(filePath,true);  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString());  
}  
```  
  
```vb  
Public Overrides  Sub OpenLog()  
    If Not Me.connections.Contains(Me.ConfigString) Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " does not exist in the Connections collection.")  
    End If  
  
    Me.connectionManager = connections(ConfigString)  
    Dim filePath As String =  Me.connectionManager.AcquireConnectionCType(as string, Nothing)  
  
    If filePath = Nothing Or filePath.Length = 0 Then  
        Throw New Exception("The ConnectionManager " + Me.ConfigString + " is not a valid FILE ConnectionManager")  
    End If  
  
    '  Create a StreamWriter to append to.  
    sw = New StreamWriter(filePath,True)  
  
    sw.WriteLine("Open log" + System.DateTime.Now.ToShortTimeString())  
End Sub  
```  
  
### <a name="writing-log-entries"></a>로그 항목 기록  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>메서드는 패키지의 개체가 \<event> 이벤트 인터페이스 중 하나에서 Fire 메서드를 호출 하 여 이벤트를 발생 시킬 때마다 호출 됩니다. 각 이벤트가 발생할 때는 해당 컨텍스트에 대한 정보와 설명 메시지도 포함됩니다. 그러나 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 메서드를 호출할 때마다 모든 메서드 매개 변수에 대한 정보가 포함되는 것은 아닙니다. 예를 들어 이름이 설명 역할을 하는 표준 이벤트는 MessageText를 제공하지 않으며 DataCode와 DataBytes는 선택적인 추가 정보를 위한 것입니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 메서드를 구현하고 이전 섹션에서 연 스트림에 이벤트를 기록합니다.  
  
```csharp  
public override void Log(string logEntryName, string computerName, string operatorName, string sourceName, string sourceID, string executionID, string messageText, DateTime startTime, DateTime endTime, int dataCode, byte[] dataBytes)  
{  
    sw.Write(logEntryName + ",");  
    sw.Write(computerName + ",");  
    sw.Write(operatorName + ",");  
    sw.Write(sourceName + ",");  
    sw.Write(sourceID + ",");  
    sw.Write(messageText + ",");  
    sw.Write(dataBytes + ",");  
    sw.WriteLine("");  
}  
```  
  
```vb  
Public Overrides  Sub Log(ByVal logEnTryName As String, ByVal computerName As String, ByVal operatorName As String, ByVal sourceName As String, ByVal sourceID As String, ByVal executionID As String, ByVal messageText As String, ByVal startTime As DateTime, ByVal endTime As DateTime, ByVal dataCode As Integer, ByVal dataBytes() As Byte)  
    sw.Write(logEnTryName + ",")  
    sw.Write(computerName + ",")  
    sw.Write(operatorName + ",")  
    sw.Write(sourceName + ",")  
    sw.Write(sourceID + ",")  
    sw.Write(messageText + ",")  
    sw.Write(dataBytes + ",")  
    sw.WriteLine("")  
End Sub  
```  
  
### <a name="closing-the-log"></a>로그 닫기  
 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 메서드는 패키지 실행이 끝날 때, 즉 패키지에 있는 모든 개체의 실행이 완료된 후나 오류로 인해 패키지가 중지된 경우에 호출됩니다.  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 메서드 실행 중 연 파일 스트림을 닫는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A> 메서드의 구현을 보여 줍니다.  
  
```csharp  
public override void CloseLog()  
{  
    if (sw != null)  
    {  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString());  
        sw.Close();  
    }  
}  
```  
  
```vb  
Public Overrides  Sub CloseLog()  
    If Not sw Is Nothing Then  
        sw.WriteLine("Close log" + System.DateTime.Now.ToShortTimeString())  
        sw.Close()  
    End If  
End Sub  
```  
  
![Integration Services 아이콘 (작은 아이콘)](../../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 로그 공급자 만들기](creating-a-custom-log-provider.md)   
 [사용자 지정 로그 공급자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
