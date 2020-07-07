---
title: SMO에서 연결 된 서버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06f81e9474a17e8f721d05fa1ba4df3468d3abb0
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008940"
---
# <a name="using-linked-servers-in-smo"></a>SMO에서 연결된 서버 사용
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  연결된 서버는 원격 서버의 OLE DB 데이터 원본을 나타냅니다. 원격 OLE DB 데이터 원본은 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 공급자를 사용 하 여 현재 인스턴스에 원격 데이터베이스 서버를 연결할 수 있습니다. SMO에서 연결된 서버는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> 속성은 <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 개체 모음을 참조합니다. 이들은 연결된 서버와 연결을 설정하는 데 필요한 로그온 자격 증명을 저장합니다.  
  
## <a name="ole-db-providers"></a>OLE-DB 공급자  
 SMO에서 설치된 OLE-DB 공급자는 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 개체 모음으로 표시됩니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Visual C#에서 OLE-DB 공급자 서버에 대한 링크 만들기  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 다른 유형의 데이터 원본에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB에 대한 링크를 만드는 방법을 보여 줍니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 제품 이름으로 지정하면 공식 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 용 OLE DB 공급자인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 공급자를 사용하여 연결된 서버에서 데이터에 액세스할 수 있습니다.  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>PowerShell에서 OLE-DB 공급자 서버에 대한 링크 만들기  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 다른 유형의 데이터 원본에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB에 대한 링크를 만드는 방법을 보여 줍니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 제품 이름으로 지정하면 공식 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 용 OLE DB 공급자인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 공급자를 사용하여 연결된 서버에서 데이터에 액세스할 수 있습니다.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
