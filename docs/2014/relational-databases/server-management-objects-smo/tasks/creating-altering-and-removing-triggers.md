---
title: 생성, 변경 및 제거 하는 트리거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f8a29df21e0f633a95291e7e636e6028468fd696
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093716"
---
# <a name="creating-altering-and-removing-triggers"></a>트리거 생성, 변경 및 제거
  SMO에서 트리거는 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체를 사용하여 표시됩니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 트리거는 발생 하 설정 된 경우 실행 하는 코드는 <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> 트리거 개체의 속성입니다. <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체의 다른 속성(예: <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A> 속성)을 사용하여 트리거 유형을 설정할 수 있습니다. Update 속성은 부모 테이블의 레코드 `UPDATE`에 의해 트리거 실행 여부를 지정하는 부울 값입니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 개체는 전통적인 DML(데이터 조작 언어) 트리거를 나타냅니다. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 버전에서 DDL(데이터 정의 언어) 트리거도 지원됩니다. DDL 트리거는 <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> 개체로 표시됩니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Visual Basic에서 트리거 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales`라는 기존 테이블에 업데이트 트리거를 만들고 삽입하는 방법을 보여 줍니다. 이 트리거는 테이블이 업데이트되거나 새 레코드가 삽입될 때 미리 알림 메시지를 보냅니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBTriggers1](SMO How to#SMO_VBTriggers1)]  -->  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Visual C#에서 트리거 생성, 변경 및 제거  
 이 코드 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `Sales`라는 기존 테이블에 업데이트 트리거를 만들고 삽입하는 방법을 보여 줍니다. 이 트리거는 테이블이 업데이트되거나 새 레코드가 삽입될 때 미리 알림 메시지를 보냅니다.  
  
```  
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
  
```  
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
  
  