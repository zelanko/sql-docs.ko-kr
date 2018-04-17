---
title: SMO에서 연결 된 서버를 사용 하 여 | Microsoft Docs
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
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e14e7516cbf5998c89165efe6b55775d8da9ecb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-linked-servers-in-smo"></a>SMO에서 연결된 서버 사용
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  연결된 서버는 원격 서버의 OLE DB 데이터 원본을 나타냅니다. 원격 OLE DB 데이터 원본 인스턴스에 연결 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용 하 여는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체입니다.  
  
 현재 인스턴스에 원격 데이터베이스 서버를 연결할 수 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 공급자를 사용 하 여 합니다. SMO에서 연결 된 서버 표시 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> 속성 참조의 컬렉션 <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 개체입니다. 이들은 연결된 서버와 연결을 설정하는 데 필요한 로그온 자격 증명을 저장합니다.  
  
## <a name="ole-db-providers"></a>OLE-DB 공급자  
 SMO에서 설치된 OLE-DB 공급자는 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 개체 모음으로 표시됩니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [Visual C를 만들&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Visual C#에서 OLE-DB 공급자 서버에 대한 링크 만들기  
 링크를 만드는 방법을 보여 주는 코드 예제는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB를 사용 하 여 유형이 다른 데이터 소스는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체입니다. 지정 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 제품 이름으로 데이터에서 액세스 하는 연결된 된 서버를 사용 하 여는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자를 공식적인 OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
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
 링크를 만드는 방법을 보여 주는 코드 예제는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB를 사용 하 여 유형이 다른 데이터 소스는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체입니다. 지정 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 제품 이름으로 데이터에서 액세스 하는 연결된 된 서버를 사용 하 여는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자를 공식적인 OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
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
  
  
