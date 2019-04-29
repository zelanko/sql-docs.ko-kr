---
title: 사용자 지정 연결 관리자의 사용자 인터페이스 개발 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], developing user interface
- custom user interface [Integration Services], custom connection manager
ms.assetid: 908bf2ac-fc84-4af8-a869-1cb43573d2df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 54ec4cc92383d0b8e423aabd19c0aeee9226d71f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896045"
---
# <a name="developing-a-user-interface-for-a-custom-connection-manager"></a>사용자 지정 연결 관리자의 사용자 인터페이스 개발
  기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공한 후 연결 관리자의 사용자 지정 사용자 인터페이스를 만들 수 있습니다. 사용자 지정 사용자 인터페이스를 만들지 않은 경우 사용자는 속성 창에서만 연결 관리자를 구성할 수 있습니다.  
  
 사용자 지정 사용자 인터페이스 프로젝트 또는 어셈블리에는 일반적으로 두 개의 클래스가 포함됩니다. 하나는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>를 구현하는 클래스이고 다른 하나는 이 클래스에서 사용자로부터 정보를 수집하기 위해 표시하는 Windows Form입니다.  
  
> [!IMPORTANT]  
>  [사용자 지정 연결 관리자 코딩](../building-deploying-and-debugging-custom-objects.md)에 설명된 대로 사용자 지정 사용자 인터페이스를 서명 및 빌드하고 전역 어셈블리 캐시에 설치한 후에는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> 속성에서 이 클래스의 정규화된 이름을 지정해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 기본 제공된 대부분의 태스크, 원본 및 대상은 특정 유형의 기본 제공 연결 관리자와만 사용할 수 있습니다. 따라서 이러한 예제를 기본 제공 태스크 및 구성 요소와 함께 테스트할 수 없습니다.  
  
## <a name="coding-the-user-interface-class"></a>사용자 인터페이스 클래스 코딩  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> 인터페이스에는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Delete%2A> 등의 메서드 네 개가 있습니다. 다음 섹션에서는 이 네 개의 메서드에 대해 설명합니다.  
  
> [!NOTE]  
>  사용자가 연결 관리자의 인스턴스를 삭제할 때 정리 작업을 수행할 필요가 없으면 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Delete%2A> 메서드에 대한 코드를 작성하지 않아도 됩니다.  
  
### <a name="initializing-the-user-interface"></a>사용자 인터페이스 초기화  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A> 메서드에서 디자이너는 사용자 인터페이스 클래스에서 연결 관리자의 속성을 수정할 수 있도록 구성할 연결 관리자에 대한 참조를 제공합니다. 다음 코드에서 보여 주는 것과 같이 코드에서는 나중에 사용할 수 있도록 연결 관리자에 대한 참조를 캐시해야 합니다.  
  
```vb  
Public Sub Initialize(ByVal connectionManager As Microsoft.SqlServer.Dts.Runtime.ConnectionManager, ByVal serviceProvider As System.IServiceProvider) Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize  
  
    _connectionManager = connectionManager  
    _serviceProvider = serviceProvider  
  
  End Sub  
```  
  
```csharp  
public void Initialize(Microsoft.SqlServer.Dts.Runtime.ConnectionManager connectionManager, System.IServiceProvider serviceProvider)  
{  
  
  _connectionManager = connectionManager;  
  _serviceProvider = serviceProvider;  
  
}  
```  
  
### <a name="creating-a-new-instance-of-the-user-interface"></a>사용자 인터페이스의 새 인스턴스 만들기  
 생성자가 아닌 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A> 메서드는 사용자가 연결 관리자의 새 인스턴스를 만들 때 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Initialize%2A> 메서드 다음에 호출됩니다. 사용자가 기존 연결 관리자를 복사하여 붙여 넣지 않은 경우 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A> 메서드에서는 일반적으로 편집용 폼을 표시할 수 있습니다. 다음 코드에서는 이 메서드의 구현을 보여 줍니다.  
  
```vb  
Public Function [New](ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, ByVal connectionUIArgs As Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs) As Boolean Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New  
  
  Dim clipboardService As IDtsClipboardService  
  
  clipboardService = _  
    DirectCast(_serviceProvider.GetService(GetType(IDtsClipboardService)), IDtsClipboardService)  
  If Not clipboardService Is Nothing Then  
    ' If the connection manager has been copied and pasted, take no action.  
    If clipboardService.IsPasteActive Then  
      Return True  
    End If  
  End If  
  
  Return EditSqlConnection(parentWindow)  
  
End Function  
```  
  
```csharp  
public bool New(System.Windows.Forms.IWin32Window parentWindow, Microsoft.SqlServer.Dts.Runtime.Connections connections, Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs connectionUIArgs)  
  {  
    IDtsClipboardService clipboardService;  
  
    clipboardService = (IDtsClipboardService)_serviceProvider.GetService(typeof(IDtsClipboardService));  
    if (clipboardService != null)  
    // If connection manager has been copied and pasted, take no action.  
    {  
      if (clipboardService.IsPasteActive)  
      {  
        return true;  
      }  
    }  
  
    return EditSqlConnection(parentWindow);  
  }  
```  
  
### <a name="editing-the-connection-manager"></a>연결 관리자 편집  
 편집용 폼은 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.New%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A> 메서드 모두에서 호출되므로 도우미 함수를 사용하여 폼을 표시하는 코드를 캡슐화하는 것이 편리합니다. 다음 코드에서는 이 도우미 함수의 구현을 보여 줍니다.  
  
```vb  
Private Function EditSqlConnection(ByVal parentWindow As IWin32Window) As Boolean  
  
  Dim sqlCMUIForm As New SqlConnMgrUIFormVB  
  
  sqlCMUIForm.Initialize(_connectionManager, _serviceProvider)  
  If sqlCMUIForm.ShowDialog(parentWindow) = DialogResult.OK Then  
    Return True  
  Else  
    Return False  
  End If  
  
End Function  
```  
  
```csharp  
private bool EditSqlConnection(IWin32Window parentWindow)  
 {  
  
   SqlConnMgrUIFormCS sqlCMUIForm = new SqlConnMgrUIFormCS();  
  
   sqlCMUIForm.Initialize(_connectionManager, _serviceProvider);  
   if (sqlCMUIForm.ShowDialog(parentWindow) == DialogResult.OK)  
   {  
     return true;  
   }  
   else  
   {  
     return false;  
   }  
  
 }  
```  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A> 메서드에서는 편집용 폼을 표시하기만 하면 됩니다. 다음 코드에서는 도우미 함수를 사용하여 폼의 코드를 캡슐화하는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit%2A> 메서드의 구현을 보여 줍니다.  
  
```vb  
Public Function Edit(ByVal parentWindow As System.Windows.Forms.IWin32Window, ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, ByVal connectionUIArg As Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs) As Boolean Implements Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI.Edit  
  
  Return EditSqlConnection(parentWindow)  
  
End Function  
```  
  
```csharp  
public bool Edit(System.Windows.Forms.IWin32Window parentWindow, Microsoft.SqlServer.Dts.Runtime.Connections connections, Microsoft.SqlServer.Dts.Runtime.Design.ConnectionManagerUIArgs connectionUIArg)  
{  
  
  return EditSqlConnection(parentWindow);  
  
}  
```  
  
## <a name="coding-the-user-interface-form"></a>사용자 인터페이스 폼 코딩  
 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> 인터페이스의 메서드를 구현하는 사용자 인터페이스 클래스를 만든 후에는 사용자가 연결 관리자의 속성을 구성할 수 있는 Windows Form을 만들어야 합니다.  
  
### <a name="initializing-the-user-interface-form"></a>사용자 인터페이스 폼 초기화  
 편집용 사용자 지정 폼을 표시하면 편집할 연결 관리자에 대한 참조를 전달할 수 있습니다. 폼 클래스의 사용자 지정 생성자를 사용하거나 여기에 표시된 대로 `Initialize` 메서드를 만들어 이 참조를 전달할 수 있습니다.  
  
```vb  
Public Sub Initialize(ByVal connectionManager As ConnectionManager, ByVal serviceProvider As IServiceProvider)  
  
  _connectionManager = connectionManager  
  _serviceProvider = serviceProvider  
  ConfigureControlsFromConnectionManager()  
  EnableControls()  
  
End Sub  
```  
  
```csharp  
public void Initialize(ConnectionManager connectionManager, IServiceProvider serviceProvider)  
 {  
  
   _connectionManager = connectionManager;  
   _serviceProvider = serviceProvider;  
   ConfigureControlsFromConnectionManager();  
   EnableControls();  
  
 }  
```  
  
### <a name="setting-properties-on-the-user-interface-form"></a>사용자 인터페이스 폼의 속성 설정  
 마지막으로 폼 클래스에는 해당 폼이 처음 로드될 때 폼의 컨트롤을 연결 관리자의 기존 또는 기본 속성 값으로 채우는 도우미 함수가 필요합니다. 또한 폼 클래스에는 사용자가 "확인"을 클릭하고 폼을 닫을 때 속성 값을 사용자가 입력한 값으로 설정하는 유사한 함수가 필요합니다.  
  
```vb  
Private Const CONNECTIONNAME_BASE As String = "SqlConnectionManager"  
  
Private Sub ConfigureControlsFromConnectionManager()  
  
  Dim tempName As String  
  Dim tempServerName As String  
  Dim tempDatabaseName As String  
  
  With _connectionManager  
  
    tempName = .Properties("Name").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempName) Then  
      _connectionName = tempName  
    Else  
      _connectionName = CONNECTIONNAME_BASE  
    End If  
  
    tempServerName = .Properties("ServerName").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempServerName) Then  
      _serverName = tempServerName  
      txtServerName.Text = _serverName  
    End If  
  
    tempDatabaseName = .Properties("DatabaseName").GetValue(_connectionManager).ToString  
    If Not String.IsNullOrEmpty(tempDatabaseName) Then  
      _databaseName = tempDatabaseName  
      txtDatabaseName.Text = _databaseName  
    End If  
  
  End With  
  
End Sub  
  
Private Sub ConfigureConnectionManagerFromControls()  
  
  With _connectionManager  
    .Properties("Name").SetValue(_connectionManager, _connectionName)  
    .Properties("ServerName").SetValue(_connectionManager, _serverName)  
    .Properties("DatabaseName").SetValue(_connectionManager, _databaseName)  
  End With  
  
End Sub  
```  
  
```csharp  
private const string CONNECTIONNAME_BASE = "SqlConnectionManager";  
  
private void ConfigureControlsFromConnectionManager()  
 {  
  
   string tempName;  
   string tempServerName;  
   string tempDatabaseName;  
  
   {  
     tempName = _connectionManager.Properties["Name"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempName))  
     {  
       _connectionName = tempName;  
     }  
     else  
     {  
       _connectionName = CONNECTIONNAME_BASE;  
     }  
  
     tempServerName = _connectionManager.Properties["ServerName"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempServerName))  
     {  
       _serverName = tempServerName;  
       txtServerName.Text = _serverName;  
     }  
  
     tempDatabaseName = _connectionManager.Properties["DatabaseName"].GetValue(_connectionManager).ToString();  
     if (!String.IsNullOrEmpty(tempDatabaseName))  
     {  
       _databaseName = tempDatabaseName;  
       txtDatabaseName.Text = _databaseName;  
     }  
  
   }  
  
 }  
  
 private void ConfigureConnectionManagerFromControls()  
 {  
  
   {  
     _connectionManager.Properties["Name"].SetValue(_connectionManager, _connectionName);  
     _connectionManager.Properties["ServerName"].SetValue(_connectionManager, _serverName);  
     _connectionManager.Properties["DatabaseName"].SetValue(_connectionManager, _databaseName);  
   }  
  
 }  
```  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 연결 관리자 만들기](creating-a-custom-connection-manager.md)   
 [사용자 지정 연결 관리자 코딩](coding-a-custom-connection-manager.md)  
  
  
