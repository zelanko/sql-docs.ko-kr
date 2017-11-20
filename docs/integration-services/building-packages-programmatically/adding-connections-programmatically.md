---
title: "연결을 프로그래밍 방식으로 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b768ad80f2b28cc3fb73a2210188bab26c902441
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="adding-connections-programmatically"></a>프로그래밍 방식으로 연결 추가
  <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 외부 데이터 원본에 대한 실제 연결을 나타냅니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 연결의 구현 세부 사항을 런타임에서 격리합니다. 이 클래스를 사용하면 런타임에서는 일관되고 예측 가능한 방식으로 각 연결 관리자와 상호 작용할 수 있습니다. 연결 관리자에는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ID%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Description%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A>과 같이 모든 연결에 공통된 스톡 속성 집합이 포함되어 있습니다. 그러나 연결 관리자를 구성하는 데는 일반적으로 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.ConnectionString%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Name%2A> 속성만 필요합니다. 다른 프로그래밍 패러다임과, 여기서 연결 클래스 메서드를 노출와 같은 달리 **열려** 또는 **연결** 실제 데이터 원본에 연결을 설정, 런타임 엔진에서 관리를 패키지에 대 한 모든 연결 실행 되는 동안 합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 클래스는 해당 패키지에 추가되었으며 런타임에 사용할 수 있는 연결 관리자의 컬렉션입니다. 컬렉션의 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 메서드를 사용하고 연결 관리자 유형을 나타내는 문자열을 지정하여 컬렉션에 연결 관리자를 추가할 수도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Add%2A> 메서드는 패키지에 추가된 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 인스턴스를 반환합니다.  
  
## <a name="intrinsic-properties"></a>기본 속성  
 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 클래스는 모든 연결에 공통된 속성 집합을 제공합니다. 그러나 특정 연결 유형에 고유한 속성에 액세스해야 하는 경우도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.Properties%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 컬렉션을 사용하면 이러한 속성에 액세스할 수 있습니다. 인덱서 나 속성 이름을 사용 하 여 컬렉션에서 속성을 검색할 수 있습니다 및 **GetValue** 메서드와 값 사용 하 여 설정 되는 **SetValue** 메서드. 기본 연결 개체의 속성은 개체의 실제 인스턴스를 가져오고 해당 속성을 직접 설정하는 방법으로 설정할 수 있습니다. 기본 연결을 가져오려면 연결 관리자의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.InnerObject%2A> 속성을 사용합니다. 다음 코드 줄에서는 기본 클래스 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.ConnectionManagerAdoNetClass>가 있는 ADO.NET 연결 관리자를 만드는 C# 줄을 보여 줍니다.  
  
 `ConnectionManagerAdoNetClass cmado = cm.InnerObject as ConnectionManagerAdoNet;`  
  
 이 코드 줄은 관리되는 연결 관리자 개체를 기본 연결 개체로 캐스팅합니다. C + +를 사용 하는 경우는 **QueryInterface** 의 메서드는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체를 호출 하 고 기본 연결 개체의 인터페이스를 요청 합니다.  
  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 연결 관리자와 `package.Connections.Add("xxx")` 문에 사용되는 문자열을 보여 줍니다. 모든 연결 관리자의 목록에 대 한 참조 [Integration services&#40; Ssis&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)합니다.  
  
|문자열|ODBC 대상 편집기|  
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
|"SQLMOBILE"|연결 관리자에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결용입니다.|  
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
  
 `Connection description: OLE DB connection to the AdventureWorks database.`  
  
 `Number of connections in package: 2`  
  
## <a name="external-resources"></a>외부 리소스  
 기술 문서- [연결 문자열](http://go.microsoft.com/fwlink/?LinkId=220743), carlprothman.net의 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자 만들기](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  

