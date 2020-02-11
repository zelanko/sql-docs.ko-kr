---
title: SQL Server의 인스턴스에 연결 하는 중 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d22ec44b7be6562c7186272b403a76cd562be62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192084"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>SQL Server 인스턴스에 연결
  SMO ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) 응용 프로그램의 첫 번째 프로그래밍 단계는 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체의 인스턴스를 만들고 인스턴스에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]대 한 연결을 설정 하는 것입니다.  
  
 다음과 같은 세 가지 방법으로 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체의 인스턴스를 만들고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 설정할 수 있습니다. 첫 번째는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체 변수를 사용하여 연결 정보를 제공하는 것입니다. 두 번째는 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 속성을 명시적으로 설정하여 연결 정보를 제공하는 것입니다. 세 번째는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 개체 생성자에 <xref:Microsoft.SqlServer.Management.Smo.Server> 인스턴스의 이름을 전달하는 것입니다.  
  
 **ServerConnection 개체 사용**  
  
 
  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체 변수를 사용할 경우 연결 정보를 다시 사용할 수 있다는 장점이 있습니다. 
  <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 변수를 선언합니다. 그런 다음 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 선언하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름 및 인증 모드와 같은 연결 정보를 사용하여 속성을 설정합니다. 그리고 나서 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체 변수를 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 생성자에 매개 변수로 전달합니다. 다른 서버 개체 간에는 연결을 동시에 공유하지 않는 것이 좋습니다. 
  <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> 메서드를 사용하여 기존 연결 문자열의 복사본을 가져옵니다.  
  
 **Server 개체 속성을 명시적으로 설정**  
  
 또는 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 변수를 선언하고 기본 생성자를 호출할 수 있습니다. 이 경우 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체가 모든 기본 연결 설정을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 인스턴스에 연결합니다.  
  
 **Server 개체 생성자에 SQL Server 인스턴스 이름 제공**  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.Server> 개체 변수를 선언하고 생성자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름을 문자열 매개 변수로 전달합니다. 
  <xref:Microsoft.SqlServer.Management.Smo.Server> 개체가 기본 연결 설정을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스와의 연결을 설정합니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 일반적으로 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 개체의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 메서드는 호출할 필요가 없습니다. SMO는 필요한 경우 자동으로 연결을 설정하고 작업을 완료한 후에는 연결을 연결 풀로 해제합니다. 
  <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 메서드를 호출하면 연결이 풀로 해제되지 않습니다. 이 경우 연결을 풀로 해제하려면 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 메서드를 명시적으로 호출해야 합니다. 또는 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 개체의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 속성을 설정하여 풀링되지 않은 연결을 요청할 수 있습니다.  
  
## <a name="multithreaded-applications"></a>다중 스레드 애플리케이션  
 다중 스레드 애플리케이션의 경우 각 스레드에서 별도의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용해야 합니다.  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>RMO의 SQL Server 인스턴스 연결  
 RMO(복제 관리 개체)는 SMO와는 약간 다른 방법으로 복제 서버에 연결합니다.  
  
 RMO 프로그래밍 개체의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네임스페이스에서 구현한 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용하여 `Microsoft.SqlServer.Management.Common` 인스턴스에 연결해야 합니다. 이 서버 연결은 RMO 프로그래밍 개체와는 독립적으로 이루어집니다. 그런 다음에는 인스턴스 생성 중에 또는 개체의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 할당하여 연결이 RMO 개체로 전달됩니다. 이런 식으로 RMO 프로그래밍 개체와 연결 개체 인스턴스를 별도로 만들고 관리할 수 있으며 여러 RMO 프로그래밍 개체에서 단일 연결 개체를 다시 사용할 수 있습니다. 복제 서버에 대한 연결에는 다음 규칙이 적용됩니다.  
  
-   지정된 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체에 대해 모든 연결 속성이 정의됩니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 각 연결에 고유의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체가 있어야 합니다.  
  
-   서버에 연결하고 성공적으로 로그인하기 위해 모든 인증 정보를 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체에 제공합니다.  
  
-   연결 설정 시 기본적으로 Microsoft Windows 인증이 사용됩니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하려면 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A>를 False로 설정하고 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A>를 올바른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그온 및 암호로 설정해야 합니다. 보안 자격 증명은 항상 안전하게 저장 및 처리되어야 하고 가능하면 런타임에 제공되어야 합니다.  
  
-   연결을 RMO 프로그래밍 개체에 전달하기 전에 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 메서드를 호출해야 합니다.  
  
## <a name="examples"></a>예  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Visual Basic에서 Windows 인증을 사용하여 SQL Server 로컬 인스턴스에 연결  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로컬 인스턴스에 연결하는 데는 많은 코드가 필요하지 않습니다. 대신 인증 방법 및 서버에 대한 기본 설정이 사용됩니다. 데이터 검색이 필요한 첫 번째 작업에서 연결이 만들어집니다.  
  
 이 예제는 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] Windows 인증을 사용 하 여의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로컬 인스턴스에 연결 하는 .net 코드입니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB1](SMO How to#SMO_VB1)]  -->  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C#에서 Windows 인증을 사용하여 SQL Server 로컬 인스턴스에 연결  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로컬 인스턴스에 연결하는 데는 많은 코드가 필요하지 않습니다. 대신 인증 방법 및 서버에 대한 기본 설정이 사용됩니다. 데이터 검색이 필요한 첫 번째 작업에서 연결이 만들어집니다.  
  
 다음 예는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로컬 인스턴스에 연결하는 Visual C# .NET 코드입니다.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//The connection is established when a property is requested.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Visual Basic .NET에서 Windows 인증을 사용하여 SQL Server 원격 인스턴스에 연결  
 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결할 경우에는 인증 유형을 지정할 필요가 없습니다. Windows 인증이 기본값입니다.  
  
 이 예제는 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] Windows 인증을 사용 하 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 여 원격 인스턴스에 연결 하는 .net 코드입니다. *Strserver* 문자열 변수에는 원격 인스턴스의 이름이 포함 됩니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB2](SMO How to#SMO_VB2)]  -->  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Visual C#에서 Windows 인증을 사용하여 SQL Server 원격 인스턴스에 연결  
 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결할 경우에는 인증 유형을 지정할 필요가 없습니다. Windows 인증이 기본값입니다.  
  
 다음 예는 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 원격 인스턴스에 연결하는 Visual C# .NET 코드입니다. *Strserver* 문자열 변수에는 원격 인스턴스의 이름이 포함 됩니다.  
  
```  
{   
//Connect to a remote instance of SQL Server.   
Server srv;   
//The strServer string variable contains the name of a remote instance of SQL Server.   
srv = new Server(strServer);   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-basic"></a>Visual Basic에서 SQL Server 인증을 사용하여 SQL Server 인스턴스에 연결  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결할 경우에는 인증 유형을 지정해야 합니다. 다음 예에서는 연결 정보를 다시 사용할 수 있도록 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체 변수를 선언하는 다른 방법을 보여 줍니다.  
  
 예는 원격 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 및 *vpassword* 에 연결 하는 방법을 보여 주는 .net 코드는 로그온 및 암호를 포함 합니다.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim sqlServerLogin As [String] = "user_id"  
      Dim password As [String] = "pwd"  
      Dim instanceName As [String] = "instance_name"  
      Dim remoteSvrName As [String] = "remote_server_name"  
  
      ' Connecting to an instance of SQL Server using SQL Server Authentication  
      Dim srv1 As New Server()   ' connects to default instance  
      srv1.ConnectionContext.LoginSecure = False   ' set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin  
      srv1.ConnectionContext.Password = password  
      Console.WriteLine(srv1.Information.Version)   ' connection is established  
  
      ' Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      Dim srvConn As New ServerConnection()  
      srvConn.ServerInstance = ".\" & instanceName   ' connects to named instance  
      srvConn.LoginSecure = False   ' set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin  
      srvConn.Password = password  
      Dim srv2 As New Server(srvConn)  
      Console.WriteLine(srv2.Information.Version)   ' connection is established  
  
      ' For remote connection, remote server name / ServerInstance needs to be specified  
      Dim srvConn2 As New ServerConnection(remoteSvrName)  
      srvConn2.LoginSecure = False  
      srvConn2.Login = sqlServerLogin  
      srvConn2.Password = password  
      Dim srv3 As New Server(srvConn2)  
      Console.WriteLine(srv3.Information.Version)   ' connection is established  
   End Sub  
End Class  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-c"></a>Visual C#에서 SQL Server 인증을 사용하여 SQL Server 인스턴스에 연결  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결할 경우에는 인증 유형을 지정해야 합니다. 다음 예에서는 연결 정보를 다시 사용할 수 있도록 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체 변수를 선언하는 다른 방법을 보여 줍니다.  
  
 예제는 원격 및 *Vpassword* 에 연결 하는 방법을 보여 주는 Visual c # .net 코드는 로그온 및 암호를 포함 합니다.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {   
      String sqlServerLogin = "user_id";  
      String password = "pwd";  
      String instanceName = "instance_name";  
      String remoteSvrName = "remote_server_name";  
  
      // Connecting to an instance of SQL Server using SQL Server Authentication  
      Server srv1 = new Server();   // connects to default instance  
      srv1.ConnectionContext.LoginSecure = false;   // set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin;  
      srv1.ConnectionContext.Password = password;  
      Console.WriteLine(srv1.Information.Version);   // connection is established  
  
      // Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      ServerConnection srvConn = new ServerConnection();  
      srvConn.ServerInstance = @".\" + instanceName;   // connects to named instance  
      srvConn.LoginSecure = false;   // set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin;  
      srvConn.Password = password;  
      Server srv2 = new Server(srvConn);  
      Console.WriteLine(srv2.Information.Version);   // connection is established  
  
      // For remote connection, remote server name / ServerInstance needs to be specified  
      ServerConnection srvConn2 = new ServerConnection(remoteSvrName);  
      srvConn2.LoginSecure = false;  
      srvConn2.Login = sqlServerLogin;  
      srvConn2.Password = password;  
      Server srv3 = new Server(srvConn2);  
      Console.WriteLine(srv3.Information.Version);   // connection is established  
   }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
