---
title: 생성, 변경 및 트리거를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b063009c7cc10226a7bed26b84219084c330c7a7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067904"
---
# <a name="creating-altering-and-removing-triggers"></a>트리거 생성, 변경 및 제거
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  SMO에서 트리거는 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체를 사용하여 표시됩니다. 합니다 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 발생 하는 트리거에 의해 설정 된 경우 실행 되는 코드는 <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> 트리거 개체의 속성입니다. <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체의 다른 속성(예: <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A> 속성)을 사용하여 트리거 유형을 설정할 수 있습니다. Update 속성은 부모 테이블의 레코드 **UPDATE** 에 의해 트리거 실행 여부를 지정하는 부울 값입니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체는 전통적인 DML(데이터 조작 언어) 트리거를 나타냅니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서 DDL(데이터 정의 언어) 트리거도 지원됩니다. DDL 트리거는 <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> 개체로 표시됩니다.  
  
## <a name="example"></a>예제  
제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Visual Basic에서 트리거 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales`라는 기존 테이블에 업데이트 트리거를 만들고 삽입하는 방법을 보여 줍니다. 이 트리거는 테이블이 업데이트되거나 새 레코드가 삽입될 때 미리 알림 메시지를 보냅니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Visual C#에서 트리거 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales`라는 기존 테이블에 업데이트 트리거를 만들고 삽입하는 방법을 보여 줍니다. 이 트리거는 테이블이 업데이트되거나 새 레코드가 삽입될 때 미리 알림 메시지를 보냅니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>PowerShell에서 트리거 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales`라는 기존 테이블에 업데이트 트리거를 만들고 삽입하는 방법을 보여 줍니다. 이 트리거는 테이블이 업데이트되거나 새 레코드가 삽입될 때 미리 알림 메시지를 보냅니다.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
