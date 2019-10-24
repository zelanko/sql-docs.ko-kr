---
title: 동의어 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a96f6ee89b920ec668af21ce625694fc31ce13bd
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781865"
---
# <a name="using-synonyms"></a>동의어 사용
  동의어는 스키마 범위 개체의 다른 이름입니다. SMO에서 동의어는 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체의 자식입니다. 이는 동의어가 정의된 데이터베이스 범위 내에서만 유효함을 의미합니다. 그러나 동의어가 다른 데이터베이스 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 원격 인스턴스의 개체를 참조할 수 있습니다.  
  
 대체 이름이 주어지는 개체를 기준 개체라고 합니다. <xref:Microsoft.SqlServer.Management.Smo.Synonym> 개체의 이름 속성이 기준 개체에 부여되는 대체 이름입니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 visual [studio .net에서 VISUAL BASIC SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 및 visual [Studio .Net에서 Visual C&#35; smo 프로젝트 만들기](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-synonym-in-visual-basic"></a>Visual Basic에서 동의어 만들기  
 코드 예제는 스키마 범위 개체에 대한 동의어 또는 대체 이름을 만드는 방법을 보여 줍니다. 클라이언트 애플리케이션에서 기준 개체를 참조하기 위해 여러 부분으로 된 이름을 사용하는 대신 동의어를 통해 기준 개체의 단일 참조를 사용할 수 있습니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSynonyms1](SMO How to#SMO_VBSynonyms1)]  -->  
  
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
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym -ArgumentList $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE SYNONYM&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
