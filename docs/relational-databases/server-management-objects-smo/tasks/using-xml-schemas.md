---
description: XML 스키마 사용
title: XML 스키마 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- XML [SMO]
ms.assetid: 9d04de01-efeb-4b2d-8c28-3234bc7ff2f3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fee01522731e38eeb830e08dd162901cf08efbb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448042"
---
# <a name="using-xml-schemas"></a>XML 스키마 사용

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO에서 XML 프로그래밍은 XML 데이터 형식, XML 네임스페이스 및 XML 데이터 형식 열의 단순 인덱스를 제공하는 것으로 제한됩니다.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 XML 문서 인스턴스에 대 한 기본 저장소를 제공 합니다. XML 스키마를 사용하여 데이터 무결성 보장을 위해 XML 문서의 유효성 검사에 사용할 수 있는 복잡한 XML 데이터 형식을 정의할 수 있습니다. XML 스키마는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 개체에 정의됩니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-an-xml-schema-in-visual-basic"></a>Visual Basic에서 XML 스키마 만들기  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 개체를 사용하여 XML 스키마를 만드는 방법을 보여 줍니다. XML 스키마 컬렉션을 정의하는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 속성은 여러 개의 큰따옴표를 포함하고 이들은 `chr(34)` 문자열로 바뀝니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define an XmlSchemaCollection object by supplying the parent database and name arguments in the constructor.
Dim xsc As XmlSchemaCollection
xsc = New XmlSchemaCollection(db, "MySampleCollection")
xsc.Text = "\<schema xmlns=" + Chr(34) + "http://www.w3.org/2001/XMLSchema" + Chr(34) + "  xmlns:ns=" + Chr(34) + "http://ns" + Chr(34) + ">\<element name=" + Chr(34) + "e" + Chr(34) + " type=" + Chr(34) + "dateTime" + Chr(34) + "/></schema>"
'Create the XML schema collection on the instance of SQL Server.
xsc.Create()
```
  
## <a name="creating-an-xml-schema-in-visual-c"></a>Visual C#에서 XML 스키마 만들기  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 개체를 사용하여 XML 스키마를 만드는 방법을 보여 줍니다. XML 스키마 컬렉션을 정의하는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 속성은 여러 개의 큰따옴표를 포함하고 이들은 `chr(34)` 문자열로 바뀝니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = default(Server);  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define an XmlSchemaCollection object by supplying the parent  
            // database and name arguments in the constructor.   
            XmlSchemaCollection xsc = default(XmlSchemaCollection);  
            xsc = new XmlSchemaCollection(db, "MySampleCollection");  
            xsc.Text = "\<schema xmlns=" + Strings.Chr(34) + "http://www.w3.org/2001/XMLSchema" + Strings.Chr(34) + " xmlns:ns=" + Strings.Chr(34) + "http://ns" + Strings.Chr(34) + ">\<element name=" + Strings.Chr(34) + "e" + Strings.Chr(34) + " type=" + Strings.Chr(34) + "dateTime" + Strings.Chr(34) + "/></schema>";  
            //Create the XML schema collection on the instance of SQL Server.   
            xsc.Create();  
        }  
```  
  
## <a name="creating-an-xml-schema-in-powershell"></a>PowerShell에서 XML 스키마 만들기  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection> 개체를 사용하여 XML 스키마를 만드는 방법을 보여 줍니다. XML 스키마 컬렉션을 정의하는 <xref:Microsoft.SqlServer.Management.Smo.XmlSchemaCollection.Text%2A> 속성은 여러 개의 큰따옴표를 포함하고 이들은 `chr(34)` 문자열로 바뀝니다.  
  
```powershell   
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalHost  
$srv = get-item default  
  
#Reference the AdventureWorks database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a new schema collection  
$xsc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.XmlSchemaCollection `  
-argumentlist $db,"MySampleCollection"  
  
#Add the xml  
$dq = '"' # the double quote character  
$xsc.Text = "<schema xmlns=" + $dq + "http://www.w3.org/2001/XMLSchema" + $dq + `  
"  xmlns:ns=" + $dq + "http://ns" + $dq + "><element name=" + $dq + "e" + $dq +`  
 " type=" + $dq + "dateTime" + $dq + "/></schema>"  
  
#Create the XML schema collection on the instance of SQL Server.  
$xsc.Create()  
```  
  
  
