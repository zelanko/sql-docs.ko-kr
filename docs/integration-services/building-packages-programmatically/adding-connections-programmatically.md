---
title: 프로그래밍 방식으로 연결 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- connection managers [Integration Services], packages
- Integration Services packages, connections
- connections [Integration Services], packages
- SSIS packages, connections
- packages [Integration Services], connections
- intrinsic properties [Integration Services]
- SQL Server Integration Services packages, connections
- ConnectionManager class
- SSIS connection managers
- adding package connections
ms.assetid: d90716d1-4c65-466c-b82c-4aabbee1e3e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eeddd2924722cbcf152c4c55c33c126a19a0679a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65729398"
---
# <a name="adding-connections-programmatically"></a>프로그래밍 방식으로 연결 추가

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 외부 데이터 원본에 대한 실제 연결을 나타냅니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 연결의 구현 세부 사항을 런타임에서 격리합니다. 이 클래스를 사용하면 런타임에서는 일관되고 예측 가능한 방식으로 각 연결 관리자와 상호 작용할 수 있습니다. 연결 관리자에는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ID%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>과 같이 모든 연결에 공통된 스톡 속성 집합이 포함되어 있습니다. 그러나 연결 관리자를 구성하는 데는 일반적으로 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> 속성만 필요합니다. 연결 클래스에서 **Open** 또는 **Connect**와 같은 메서드를 제공하여 데이터 원본에 대한 실제 연결을 설정하는 다른 프로그래밍 패러다임과 달리 런타임 엔진에서는 패키지 실행 중 패키지의 모든 연결을 관리합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 클래스는 해당 패키지에 추가되었으며 런타임에 사용할 수 있는 연결 관리자의 컬렉션입니다. 컬렉션의 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 메서드를 사용하고 연결 관리자 유형을 나타내는 문자열을 지정하여 컬렉션에 연결 관리자를 추가할 수도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 메서드는 패키지에 추가된 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 인스턴스를 반환합니다.  
  
## <a name="intrinsic-properties"></a>기본 속성  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 모든 연결에 공통된 속성 집합을 제공합니다. 그러나 특정 연결 유형에 고유한 속성에 액세스해야 하는 경우도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Properties%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 컬렉션을 사용하면 이러한 속성에 액세스할 수 있습니다. 이러한 속성을 검색하는 데는 인덱서나 속성 이름 및 **GetValue** 메서드를 사용할 수 있으며, 해당 값을 설정하는 데는 **SetValue** 메서드를 사용할 수 있습니다. 기본 연결 개체의 속성은 개체의 실제 인스턴스를 가져오고 해당 속성을 직접 설정하는 방법으로 설정할 수 있습니다. 기본 연결을 가져오려면 연결 관리자의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.InnerObject%2A> 속성을 사용합니다. 다음 코드 줄에서는 기본 클래스 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.ConnectionManagerAdoNetClass>가 있는 ADO.NET 연결 관리자를 만드는 C# 줄을 보여 줍니다.  
  
 `ConnectionManagerAdoNetClass cmado = cm.InnerObject as ConnectionManagerAdoNet;`  
  
 이 코드 줄은 관리되는 연결 관리자 개체를 기본 연결 개체로 캐스팅합니다. C++를 사용하는 경우에는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체의 **QueryInterface** 메서드를 호출하며 기본 연결 개체의 인터페이스가 필요합니다.  
  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 연결 관리자와 `package.Connections.Add("xxx")` 문에 사용되는 문자열을 보여 줍니다. 모든 연결 관리자의 목록은 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)를 참조하세요.  
  
|String|ODBC 대상 편집기|  
|------------|------------------------|  
|"OLEDB"|OLE DB 연결용 연결 관리자|  
|"ODBC"|ODBC 연결용 연결 관리자|  
|"ADO"|ADO 연결용 연결 관리자|  
|"ADO.NET:SQL"|ADO.NET(SQL 데이터 공급자) 연결용 연결 관리자|  
|"ADO.NET:OLEDB"|ADO.NET(OLE DB 데이터 공급자) 연결용 연결 관리자|  
|"FLATFILE"|플랫 파일 연결용 연결 관리자|  
|"FILE"|파일 연결용 연결 관리자|  
|"MULTIFLATFILE"|다중 플랫 파일 연결용 연결 관리자|  
|"MULTIFILE"|다중 파일 연결용 연결 관리자|  
|"SQLMOBILE"|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결용 연결 관리자|  
|"MSOLAP100"|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 연결용 연결 관리자|  
|"FTP"|FTP 연결용 연결 관리자|  
|"HTTP"|HTTP 연결용 연결 관리자|  
|"MSMQ"|메시지 큐(MSMQ) 연결용 연결 관리자|  
|"SMTP"|SMTP 연결용 연결 관리자|  
|"WMI"|Microsoft WMI(Windows Management Instrumentation) 연결용 연결 관리자|  
  
 다음 코드 예에서는 <xref:Microsoft.SqlServer.Dts.Runtime.Package.Connections%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.Package> 컬렉션에 OLE DB 및 FILE 연결을 추가하는 방법을 보여 줍니다. 그런 다음 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> 속성을 설정합니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package, and retrieve its connections.  
      Package pkg = new Package();  
      Connections pkgConns = pkg.Connections;  
  
      // Add an OLE DB connection to the package, using the   
      // method defined in the AddConnection class.  
      CreateConnection myOLEDBConn = new CreateConnection();  
      myOLEDBConn.CreateOLEDBConnection(pkg);  
  
      // View the new connection in the package.  
      Console.WriteLine("Connection description: {0}",  
         pkg.Connections["SSIS Connection Manager for OLE DB"].Description);  
  
      // Add a second connection to the package.  
      CreateConnection myFileConn = new CreateConnection();  
      myFileConn.CreateFileConnection(pkg);  
  
      // View the second connection in the package.  
      Console.WriteLine("Connection description: {0}",  
        pkg.Connections["SSIS Connection Manager for Files"].Description);  
  
      Console.WriteLine();  
      Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count);  
  
      Console.Read();  
    }  
  }  
  // <summary>  
  // This class contains the definitions for multiple  
  // connection managers.  
  // </summary>  
  public class CreateConnection  
  {  
    // Private data.  
    private ConnectionManager ConMgr;  
  
    // Class definition for OLE DB Provider.  
    public void CreateOLEDBConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("OLEDB");  
      ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" +  
        "Data Source=(local);";  
      ConMgr.Name = "SSIS Connection Manager for OLE DB";  
      ConMgr.Description = "OLE DB connection to the AdventureWorks database.";  
    }  
    public void CreateFileConnection(Package p)  
    {  
      ConMgr = p.Connections.Add("File");  
      ConMgr.ConnectionString = @"\\<yourserver>\<yourfolder>\books.xml";  
      ConMgr.Name = "SSIS Connection Manager for Files";  
      ConMgr.Description = "Flat File connection";  
    }  
  }  
  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package, and retrieve its connections.  
    Dim pkg As New Package()  
    Dim pkgConns As Connections = pkg.Connections  
  
    ' Add an OLE DB connection to the package, using the   
    ' method defined in the AddConnection class.  
    Dim myOLEDBConn As New CreateConnection()  
    myOLEDBConn.CreateOLEDBConnection(pkg)  
  
    ' View the new connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for OLE DB").Description)  
  
    ' Add a second connection to the package.  
    Dim myFileConn As New CreateConnection()  
    myFileConn.CreateFileConnection(pkg)  
  
    ' View the second connection in the package.  
    Console.WriteLine("Connection description: {0}", _  
      pkg.Connections("SSIS Connection Manager for Files").Description)  
  
    Console.WriteLine()  
    Console.WriteLine("Number of connections in package: {0}", pkg.Connections.Count)  
  
    Console.Read()  
  
  End Sub  
  
End Module  
  
' This class contains the definitions for multiple  
' connection managers.  
  
Public Class CreateConnection  
  ' Private data.  
  Private ConMgr As ConnectionManager  
  
  ' Class definition for OLE DB provider.  
  Public Sub CreateOLEDBConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("OLEDB")  
    ConMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;Initial Catalog=AdventureWorks;" & _  
      "Data Source=(local);"  
    ConMgr.Name = "SSIS Connection Manager for OLE DB"  
    ConMgr.Description = "OLE DB connection to the AdventureWorks database."  
  End Sub  
  
  Public Sub CreateFileConnection(ByVal p As Package)  
    ConMgr = p.Connections.Add("File")  
    ConMgr.ConnectionString = "\\<yourserver>\<yourfolder>\books.xml"  
    ConMgr.Name = "SSIS Connection Manager for Files"  
    ConMgr.Description = "Flat File connection"  
  End Sub  
  
End Class  
```  
  
 **샘플 출력:**  
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Connection description: Flat File connection.`  
  
 `Number of connections in package: 2`  
  
## <a name="external-resources"></a>외부 리소스  
 carlprothman.net의 기술 문서 - [Connection Strings](https://go.microsoft.com/fwlink/?LinkId=220743)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자 만들기](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
