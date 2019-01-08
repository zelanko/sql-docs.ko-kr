---
title: 사용자 지정 연결 관리자 코딩 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], coding
ms.assetid: b12b6778-1f01-4a7d-984d-73f2f7630aa5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 05331b9141ac276ca902ea6004578ea515e81f00
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53349556"
---
# <a name="coding-a-custom-connection-manager"></a>사용자 지정 연결 관리자 코딩
  <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 기본 클래스에서 상속된 클래스를 만들고 이 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 특성을 적용한 후에는 기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공해야 합니다.  
  
 사용자 지정 연결 관리자의 예제는 [사용자 지정 연결 관리자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-connection-manager.md)을 참조하세요. 이 항목에 표시된 코드 예는 SQL Server 사용자 지정 연결 관리자 예제에서 가져온 것입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 기본 제공된 대부분의 태스크, 원본 및 대상은 특정 유형의 기본 제공 연결 관리자와만 사용할 수 있습니다. 따라서 이러한 예제를 기본 제공 태스크 및 구성 요소와 함께 테스트할 수 없습니다.  
  
## <a name="configuring-the-connection-manager"></a>연결 관리자 구성  
  
### <a name="setting-the-connectionstring-property"></a>ConnectionString 속성 설정  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 속성은 중요한 속성으로서, 사용자 지정 연결 관리자에 고유한 유일한 속성입니다. 연결 관리자는 이 속성 값을 사용하여 외부 데이터 원본에 연결합니다. 서버 이름 및 데이터베이스 이름 등의 다른 여러 속성을 조합하여 연결 문자열을 만들 경우 도우미 함수로 연결 문자열 템플릿의 일부 값을 사용자가 지정한 새 값으로 바꿔 문자열을 조합할 수 있습니다. 다음 코드 예에서는 도우미 함수를 사용하여 문자열을 조합하는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 속성의 구현을 보여 줍니다.  
  
```vb  
' Default values.  
Private _serverName As String = "(local)"  
Private _databaseName As String = "AdventureWorks"  
Private _connectionString As String = String.Empty  
  
Private Const CONNECTIONSTRING_TEMPLATE As String = _  
  "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI"  
  
Public Property ServerName() As String  
  Get  
    Return _serverName  
  End Get  
  Set(ByVal value As String)  
    _serverName = value  
  End Set  
End Property  
  
Public Property DatabaseName() As String  
  Get  
    Return _databaseName  
  End Get  
  Set(ByVal value As String)  
    _databaseName = value  
  End Set  
End Property  
  
Public Overrides Property ConnectionString() As String  
  Get  
    UpdateConnectionString()  
    Return _connectionString  
  End Get  
  Set(ByVal value As String)  
    _connectionString = value  
  End Set  
End Property  
  
Private Sub UpdateConnectionString()  
  
  Dim temporaryString As String = CONNECTIONSTRING_TEMPLATE  
  
  If Not String.IsNullOrEmpty(_serverName) Then  
    temporaryString = temporaryString.Replace("<servername>", _serverName)  
  End If  
  If Not String.IsNullOrEmpty(_databaseName) Then  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName)  
  End If  
  
  _connectionString = temporaryString  
  
End Sub  
```  
  
```csharp  
// Default values.  
private string _serverName = "(local)";  
private string _databaseName = "AdventureWorks";  
private string _connectionString = String.Empty;  
  
private const string CONNECTIONSTRING_TEMPLATE = "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=SSPI";  
  
public string ServerName  
{  
  get  
  {  
    return _serverName;  
  }  
  set  
  {  
    _serverName = value;  
  }  
}  
  
public string DatabaseName  
{  
  get  
  {  
    return _databaseName;  
  }  
  set  
  {  
    _databaseName = value;  
  }  
}  
  
public override string ConnectionString  
{  
  get  
  {  
    UpdateConnectionString();  
    return _connectionString;  
  }  
  set  
  {  
    _connectionString = value;  
  }  
}  
  
private void UpdateConnectionString()  
{  
  
  string temporaryString = CONNECTIONSTRING_TEMPLATE;  
  
  if (!String.IsNullOrEmpty(_serverName))  
  {  
    temporaryString = temporaryString.Replace("<servername>", _serverName);  
  }  
  
  if (!String.IsNullOrEmpty(_databaseName))  
  {  
    temporaryString = temporaryString.Replace("<databasename>", _databaseName);  
  }  
  
  _connectionString = temporaryString;  
  
}  
```  
  
### <a name="validating-the-connection-manager"></a>연결 관리자 유효성 검사  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A> 메서드를 재정의하여 연결 관리자가 올바르게 구성되어 있는지 확인할 수 있습니다. 최소한 연결 문자열 형식의 유효성을 검사하고 모든 인수에 값이 지정되었는지 확인해야 합니다. 연결 관리자가 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success> 메서드에서 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A>를 반환하기 전까지는 실행을 계속할 수 없습니다.  
  
 다음 코드 예에서는 사용자가 연결의 서버 이름을 지정했는지 확인하는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.Validate%2A>의 구현을 보여 줍니다.  
  
```vb  
Public Overrides Function Validate(ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  If String.IsNullOrEmpty(_serverName) Then  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0)  
    Return DTSExecResult.Failure  
  Else  
    Return DTSExecResult.Success  
  End If  
  
End Function  
```  
  
```csharp  
public override Microsoft.SqlServer.Dts.Runtime.DTSExecResult Validate(Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  if (String.IsNullOrEmpty(_serverName))  
  {  
    infoEvents.FireError(0, "SqlConnectionManager", "No server name specified", String.Empty, 0);  
    return DTSExecResult.Failure;  
  }  
  else  
  {  
    return DTSExecResult.Success;  
  }  
  
}  
```  
  
### <a name="persisting-the-connection-manager"></a>연결 관리자 지속  
 일반적으로 연결 관리자의 사용자 지정 지속성은 구현할 필요가 없습니다. 사용자 지정 지속성은 개체의 속성이 복합 데이터 형식을 사용할 때만 필요합니다. 자세한 내용은[Integration Services 사용자 지정 개체 개발](../developing-custom-objects-for-integration-services.md)을 참조하세요.  
  
## <a name="working-with-the-external-data-source"></a>외부 데이터 원본 작업  
 외부 데이터 원본에 대한 연결을 지원하는 메서드는 사용자 지정 연결 관리자의 중요한 메서드입니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 메서드는 디자인 타임과 런타임에 호출됩니다.  
  
### <a name="acquiring-the-connection"></a>연결 설정  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 메서드가 사용자 지정 연결 관리자에서 반환하는 데 적절한 개체 유형을 결정해야 합니다. 예를 들어 파일 연결 관리자는 경로 및 파일 이름이 들어 있는 문자열만 반환하는 반면에 ADO.NET 연결 관리자는 이미 열려 있는 관리되는 연결 개체를 반환합니다. 또한 OLE DB 연결 관리자는 관리 코드에서 사용할 수 없는 네이티브 OLE DB 연결 개체를 반환하고, 사용자 지정 SQL Server 연결 관리자는 열려 있는 `SqlConnection` 개체를 반환합니다. 이 항목의 코드 조각은 이 연결 관리자의 일부입니다.  
  
 연결 관리자의 사용자는 반환된 개체를 적절한 유형으로 캐스팅하고 해당 메서드 및 속성에 액세스할 수 있도록 예상되는 개체 유형을 미리 알고 있어야 합니다.  
  
```vb  
Public Overrides Function AcquireConnection(ByVal txn As Object) As Object  
  
  Dim sqlConnection As New SqlConnection  
  
  UpdateConnectionString()  
  
  With sqlConnection  
    .ConnectionString = _connectionString  
    .Open()  
  End With  
  
  Return sqlConnection  
  
End Function  
```  
  
```csharp  
public override object AcquireConnection(object txn)  
{  
  
  SqlConnection sqlConnection = new SqlConnection();  
  
  UpdateConnectionString();  
  
  {  
    sqlConnection.ConnectionString = _connectionString;  
    sqlConnection.Open();  
  }  
  
  return sqlConnection;  
  
}  
```  
  
### <a name="releasing-the-connection"></a>연결 해제  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 메서드에서 수행하는 동작은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 메서드에서 반환된 개체의 유형에 따라 달라집니다. 열려 있는 연결 개체가 있는 경우 해당 연결 개체를 닫고 이 개체에서 사용 중인 리소스를 해제해야 합니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>이 문자열 값만 반환한 경우에는 아무 동작도 수행할 필요가 없습니다.  
  
```vb  
Public Overrides Sub ReleaseConnection(ByVal connection As Object)  
  
  Dim sqlConnection As SqlConnection  
  
  sqlConnection = DirectCast(connection, SqlConnection)  
  
  If sqlConnection.State <> ConnectionState.Closed Then  
    sqlConnection.Close()  
  End If  
  
End Sub  
```  
  
```csharp  
public override void ReleaseConnection(object connection)  
{  
  SqlConnection sqlConnection;  
  sqlConnection = (SqlConnection)connection;  
  if (sqlConnection.State != ConnectionState.Closed)  
    sqlConnection.Close();  
}  
```  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 연결 관리자 만들기](creating-a-custom-connection-manager.md)   
 [사용자 지정 연결 관리자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
