---
title: SQL server 인스턴스에서 연결 끊기 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7a724db457da651cf74c259069bea149a8e6da76
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 연결 끊기
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  수동으로 SMO( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) 개체를 닫고 연결을 끊을 필요는 없습니다. 필요에 따라 연결이 열리고 닫힙니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 경우는 [연결](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) 메서드를 호출 하면 연결이 자동으로 해제 되지 않습니다. [연결 끊기](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) 연결 풀에 대 한 연결을 해제 하기 위해 메서드를 명시적으로 호출 해야 합니다. 풀링되지 않은 연결을 요청할 수도 있습니다. 설정 하 여이 작업을 수행는 [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 참조 하는 속성의 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체입니다.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>RMO에 대해 SQL Server 인스턴스에서 연결 끊기  
 RMO를 사용하여 프로그래밍할 때 서버 연결을 닫는 방법은 SMO와는 약간 다릅니다.  
  
 RMO 개체에 대 한 서버 연결 하 여 유지 관리 되므로 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체를이 개체는 인스턴스에서 연결을 끊는 경우에 사용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] RMO를 사용 하 여 프로그래밍할 때. 사용 하 여 연결을 끊어야는 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) 개체를 호출 하는 [연결 끊기](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) RMO 개체의 메서드. 연결이 닫힌 후에는 RMO 개체를 사용할 수 없습니다.  
  
## <a name="example"></a>예제  
제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [Visual C를 만들&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Visual Basic에서 SMO 개체 닫기 및 연결 끊기  
 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 주는 코드 예제는 [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 의 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성입니다.  
  
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
 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 주는 코드 예제는 [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) 의 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
