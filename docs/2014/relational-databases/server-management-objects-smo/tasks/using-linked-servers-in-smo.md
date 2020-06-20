---
title: SMO에서 연결 된 서버 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67bb9f002356e94f2546527aacae13b56768930d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003530"
---
# <a name="using-linked-servers-in-smo"></a>SMO에서 연결된 서버 사용
  연결된 서버는 원격 서버의 OLE DB 데이터 원본을 나타냅니다. 원격 OLE DB 데이터 원본은 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 공급자를 사용 하 여 현재 인스턴스에 원격 데이터베이스 서버를 연결할 수 있습니다. SMO에서 연결된 서버는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> 속성은 <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 개체 모음을 참조합니다. 이들은 연결된 서버와 연결을 설정하는 데 필요한 로그온 자격 증명을 저장합니다.  
  
## <a name="ole-db-providers"></a>OLE-DB 공급자  
 SMO에서 설치된 OLE-DB 공급자는 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 개체 모음으로 표시됩니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 visual studio [.net에서 VISUAL BASIC SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 및 visual [Studio .Net에서 VISUAL C&#35; smo 프로젝트 만들기](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>Visual Basic에서 OLE-DB 공급자 서버에 대한 링크 만들기  
 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 개체를 사용하여 다른 유형의 데이터 원본에 대해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB에 대한 링크를 만드는 방법을 보여 줍니다. 를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 제품 이름으로 지정 하면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 공식 OLE DB 공급자 인 클라이언트 OLE DB 공급자를 사용 하 여 연결 된 서버에서 데이터에 액세스할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 있습니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
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
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -ArgumentList $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.
$lsvr.ProductName = "SQL Server"
  
#Create the Database Object  
$lsvr.Create()
```  
