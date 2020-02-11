---
title: 사용자 정의 함수 생성, 변경 및 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edde17b3339a6a78f81ddf92da95afb2f8ba851c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782344"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>사용자 정의 함수 생성, 변경 및 제거
  개체 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 는 사용자가에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]사용자 정의 함수를 프로그래밍 방식으로 관리할 수 있도록 하는 기능을 제공 합니다. 사용자 정의 함수는 입력 및 출력 매개 변수를 지원하며 테이블 열에 대한 직접 참조도 지원합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 저장 프로시저, 사용자 정의 함수, 트리거 및 사용자 정의 데이터 형식에서 어셈블리를 사용할 수 있으려면 먼저 데이터베이스에 어셈블리를 등록해야 합니다. SMO는 <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> 개체에서 이 기능을 지원합니다.  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 개체는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> 및 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> 속성으로 .NET 어셈블리를 참조합니다.  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 개체가 .NET 어셈블리를 참조하는 경우 <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> 개체를 만들고 이를 <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> 개체에 속하는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체에 추가하여 어셈블리를 등록해야 합니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 visual [studio .net에서 VISUAL BASIC SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [visual Studio .Net에서 VISUAL C&#35; smo 프로젝트 만들기](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Visual Basic에서 스칼라 사용자 정의 함수 만들기  
 이 코드 예제는 <xref:System.DateTime>에서 입력 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 개체 매개 변수와 정수 반환 형식을 사용하는 스칼라 사용자 정의 함수를 만들고 제거하는 방법을 보여 줍니다. 사용자 정의 함수는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 만들어집니다. 이 예에서는 날짜 인수를 사용하여 ISO 주 번호를 계산하는 ISOweek라는 사용자 정의 함수를 만듭니다. 이 함수가 계산을 제대로 수행하기 위해서는 함수를 호출하기 전에 데이터베이스 DATEFIRST 옵션을 1로 설정해야 합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Visual C#에서 스칼라 사용자 정의 함수 만들기  
 이 코드 예제는 <xref:System.DateTime>에서 입력 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 개체 매개 변수와 정수 반환 형식을 사용하는 스칼라 사용자 정의 함수를 만들고 제거하는 방법을 보여 줍니다. 사용자 정의 함수는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 만들어집니다. 이 예에서는 사용자 정의 함수를 만듭니다. `ISOweek`. 이 함수는 날짜 인수를 사용하여 ISO 주 번호를 계산합니다. 이 함수가 계산을 제대로 수행하기 위해서는 함수를 호출하기 전에 데이터베이스 `DATEFIRST` 옵션을 `1` 로 설정해야 합니다.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>PowerShell에서 스칼라 사용자 정의 함수 만들기  
 이 코드 예제는 <xref:System.DateTime>에서 입력 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 개체 매개 변수와 정수 반환 형식을 사용하는 스칼라 사용자 정의 함수를 만들고 제거하는 방법을 보여 줍니다. 사용자 정의 함수는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 데이터베이스에 만들어집니다. 이 예에서는 사용자 정의 함수를 만듭니다. `ISOweek`. 이 함수는 날짜 인수를 사용하여 ISO 주 번호를 계산합니다. 이 함수가 계산을 제대로 수행하기 위해서는 함수를 호출하기 전에 데이터베이스 `DATEFIRST` 옵션을 `1` 로 설정해야 합니다.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction -argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter -argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.
$udf.Create()  
  
# Remove the user-defined function.
$udf.Drop()  
```  
  
## <a name="see-also"></a>참고 항목  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
