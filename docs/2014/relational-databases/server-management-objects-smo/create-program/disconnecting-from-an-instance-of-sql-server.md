---
title: SQL server 인스턴스에서 연결 끊기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1f2ce4ae7ce42df42be9b6bc68c3d13acf949dba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181023"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>SQL Server 인스턴스에서 연결 끊기
  수동으로 닫고 연결을 끊을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) 개체 필요 하지 않습니다. 필요에 따라 연결이 열리고 닫힙니다.  
  
## <a name="connection-pooling"></a>연결 풀링  
 경우는 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 메서드를 호출 하면 연결이 자동으로 해제 되지 않습니다. <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 메서드를 명시적으로 호출하여 연결 풀에 대한 연결을 해제해야 합니다. 풀링되지 않은 연결을 요청할 수도 있습니다. 이 작업은 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 개체를 참조하는 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 속성의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 속성을 설정하여 수행됩니다.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>RMO에 대해 SQL Server 인스턴스에서 연결 끊기  
 RMO를 사용하여 프로그래밍할 때 서버 연결을 닫는 방법은 SMO와는 약간 다릅니다.  
  
 RMO 개체에 대 한 서버 연결 하 여 유지 관리 되므로 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를이 개체는 인스턴스에서 연결을 끊는 경우에 사용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] RMO를 사용 하 여 프로그래밍할 때. 사용 하 여 연결을 끊어야는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 호출 하는 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> RMO 개체의 메서드. 연결이 닫힌 후에는 RMO 개체를 사용할 수 없습니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Visual Basic에서 SMO 개체 닫기 및 연결 끊기  
 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 주는 코드 예제는 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 의 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성입니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Visual C#에서 SMO 개체 닫기 및 연결 끊기  
 설정 하 여 풀링되지 않은 연결을 요청 하는 방법을 보여 주는 코드 예제는 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 의 속성은 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 개체 속성입니다.  
  
```  
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
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  