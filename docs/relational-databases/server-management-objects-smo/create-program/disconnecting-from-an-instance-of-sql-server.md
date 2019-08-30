---
title: SQL Server의 인스턴스에서 연결을 끊는 중 Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: de53acd4ef3d9feb6ed1a5026d8890f83e88d557
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148732"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 연결 끊기
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  수동으로 SMO( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) 개체를 닫고 연결을 끊을 필요는 없습니다. 필요에 따라 연결이 열리고 닫힙니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 [Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) 메서드를 호출 하면 연결이 자동으로 해제 되지 않습니다. 연결 풀에 대 한 연결을 해제 하려면 [Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) 메서드를 명시적으로 호출 해야 합니다. 풀링되지 않은 연결을 요청할 수도 있습니다. [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체를 참조 하는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 속성의 [nonpooledconnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 속성을 설정 하 여이 작업을 수행 합니다.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>RMO에 대해 SQL Server 인스턴스에서 연결 끊기  
 RMO를 사용하여 프로그래밍할 때 서버 연결을 닫는 방법은 SMO와는 약간 다릅니다.  
  
 Rmo 개체에 대 한 서버 연결이 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체에 의해 유지 관리 되기 때문에 rmo를 사용 하 여 프로그래밍할 때 인스턴스에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 연결을 끊을 때도이 개체가 사용 됩니다. [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체를 사용 하 여 연결을 닫으려면 rmo 개체의 [Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) 메서드를 호출 합니다. 연결이 닫힌 후에는 RMO 개체를 사용할 수 없습니다.  
  
## <a name="example"></a>예제  
제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Visual Basic에서 SMO 개체 닫기 및 연결 끊기  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성의 [nonpooledconnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 속성을 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 줍니다.  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Visual C#에서 SMO 개체 닫기 및 연결 끊기  
 이 코드 예제에서는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성의 [nonpooledconnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 속성을 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 줍니다.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
