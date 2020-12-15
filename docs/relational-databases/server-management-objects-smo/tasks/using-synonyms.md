---
description: 동의어 사용
title: 동의어 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 47deb46f1ff11a207aebcb1b5a77fb67b6f2c2b8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467184"
---
# <a name="using-synonyms"></a>동의어 사용
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  동의어는 스키마 범위 개체의 다른 이름입니다. SMO에서 동의어는 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체의 자식입니다. 이는 동의어가 정의된 데이터베이스 범위 내에서만 유효함을 의미합니다. 그러나 동의어가 다른 데이터베이스 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 원격 인스턴스의 개체를 참조할 수 있습니다.  
  
 대체 이름이 주어지는 개체를 기준 개체라고 합니다. <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체의 이름 속성이 기준 개체에 부여되는 대체 이름입니다.  
  
## <a name="example"></a>예  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-synonym-in-visual-c"></a>Visual C#에서 동의어 만들기  
 코드 예제는 스키마 범위 개체에 대한 동의어 또는 대체 이름을 만드는 방법을 보여 줍니다. 클라이언트 애플리케이션에서 기준 개체를 참조하기 위해 여러 부분으로 된 이름을 사용하는 대신 동의어를 통해 기준 개체의 단일 참조를 사용할 수 있습니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>PowerShell에서 동의어 만들기  
 코드 예제는 스키마 범위 개체에 대한 동의어 또는 대체 이름을 만드는 방법을 보여 줍니다. 클라이언트 애플리케이션에서 기준 개체를 참조하기 위해 여러 부분으로 된 이름을 사용하는 대신 동의어를 통해 기준 개체의 단일 참조를 사용할 수 있습니다.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  
