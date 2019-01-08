---
title: 생성, 변경 및 저장된 프로시저를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [SMO]
ms.assetid: 2a072f9c-8f11-4364-ab71-3990735a8d66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc38e4f11b32c368626b0f84a352d3f9c00fa0f7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805415"
---
# <a name="creating-altering-and-removing-stored-procedures"></a>저장 프로시저 생성, 변경 및 제거
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects(SMO)에서 저장 프로시저는 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 개체로 표시됩니다.  
  
 SMO에서 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 개체를 만들려면 저장 프로시저를 정의하는 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.TextBody%2A> 속성을 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트로 설정해야 합니다. 매개 변수가 필요 합니다 \@ 접두사를 사용 하 여 개별적으로 만들어야 합니다 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> 개체를 추가 하는 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> 컬렉션은 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> 개체.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-basic"></a>Visual Basic에서 저장 프로시저 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 대한 저장 프로시저를 만드는 방법을 보여 줍니다. 이 예에서는 직원 ID 번호를 제공하면 직원의 성을 반환합니다. 저장 프로시저에는 직원 ID 번호를 지정하는 입력 매개 변수 하나와 직원의 성을 반환하는 출력 매개 변수 하나가 필요합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStoredProcs1](SMO How to#SMO_VBStoredProcs1)]  -->  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-c"></a>Visual C#에서 저장 프로시저 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 대한 저장 프로시저를 만드는 방법을 보여 줍니다. 이 예에서는 직원 ID 번호(`BusinessEntityID`)를 제공하면 직원의 성을 반환합니다. 저장 프로시저에는 직원 ID 번호를 지정하는 입력 매개 변수 하나와 직원의 성을 반환하는 출력 매개 변수 하나가 필요합니다.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
            StoredProcedure sp;  
            sp = new StoredProcedure(db, "GetLastNameByBusinessEntityID");  
            //Set the TextMode property to false and then set the other object properties.   
            sp.TextMode = false;  
            sp.AnsiNullsStatus = false;  
            sp.QuotedIdentifierStatus = false;  
            //Add two parameters.   
            StoredProcedureParameter param;  
            param = new StoredProcedureParameter(sp, "@empval", DataType.Int);  
            sp.Parameters.Add(param);  
            StoredProcedureParameter param2;  
            param2 = new StoredProcedureParameter(sp, "@retval", DataType.NVarChar(50));  
            param2.IsOutputParameter = true;  
            sp.Parameters.Add(param2);  
            //Set the TextBody property to define the stored procedure.   
            string stmt;  
            stmt = " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )";  
            sp.TextBody = stmt;  
            //Create the stored procedure on the instance of SQL Server.   
            sp.Create();  
            //Modify a property and run the Alter method to make the change on the instance of SQL Server.   
            sp.QuotedIdentifierStatus = true;  
            sp.Alter();  
            //Remove the stored procedure.   
            sp.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-powershell"></a>PowerShell에서 저장 프로시저 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 대한 저장 프로시저를 만드는 방법을 보여 줍니다. 이 예에서는 직원 ID 번호(`BusinessEntityID`)를 제공하면 직원의 성을 반환합니다. 저장 프로시저에는 직원 ID 번호를 지정하는 입력 매개 변수 하나와 직원의 성을 반환하는 출력 매개 변수 하나가 필요합니다.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
$sp  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedure `  
-argumentlist $db, "GetLastNameByBusinessEntityID"  
  
#Set the TextMode property to false and then set the other object properties.   
$sp.TextMode = $false  
$sp.AnsiNullsStatus = $false  
$sp.QuotedIdentifierStatus = $false  
  
# Add two parameters  
$type = [Microsoft.SqlServer.Management.SMO.Datatype]::Int  
$param  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@empval",$type  
$sp.Parameters.Add($param)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::NVarChar(50)  
$param2  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@retval",$type  
$param2.IsOutputParameter = $true  
$sp.Parameters.Add($param2)  
  
#Set the TextBody property to define the stored procedure.   
$sp.TextBody =  " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )"  
  
# Create the stored procedure on the instance of SQL Server.   
$sp.Create()  
  
# Modify a property and run the Alter method to make the change on the instance of SQL Server.   
$sp.QuotedIdentifierStatus = $true  
$sp.Alter()  
  
#Remove the stored procedure.   
$sp.Drop()  
```  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>  
  
  
