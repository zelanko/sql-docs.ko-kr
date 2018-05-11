---
title: 프로그래밍 방식으로 원격 패키지 로드 및 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: run-manage-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 60d811ccb738d3b9cabbb85118c99fc50fe01cb0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>프로그래밍 방식으로 원격 패키지 로드 및 실행
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 설치되어 있지 않은 로컬 컴퓨터에서 원격 패키지를 실행하려면 패키지를 시작할 때 해당 패키지가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 설치된 원격 컴퓨터에서 실행되도록 합니다. 이렇게 하려면 로컬 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, 웹 서비스 또는 원격 구성 요소를 사용하여 원격 컴퓨터에서 패키지를 시작하도록 합니다. 로컬 컴퓨터에서 직접 원격 패키지를 시작하면 패키지가 로컬 컴퓨터로 로드되어 로컬 컴퓨터에서 실행됩니다. 로컬 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 설치되어 있지 않으면 패키지가 실행되지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]가 설치되지 않은 클라이언트 컴퓨터의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 외부에서는 패키지를 실행할 수 없으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용권 계약에 따라 추가 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하지 못할 수도 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 서버 구성 요소이며 클라이언트 컴퓨터에 재배포할 수 없습니다.  
  
 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]가 설치된 로컬 컴퓨터에서 원격 패키지를 실행할 수 있습니다. 자세한 내용은 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)을 참조하세요.  
  
##  <a name="top"></a> 원격 컴퓨터에서 원격 패키지 실행  
 위에서 언급한 대로 원격 서버에서 원격 패키지를 실행하는 방법에는 여러 가지가 있습니다.  
  
-   [SQL Server 에이전트를 사용하여 프로그래밍 방식으로 원격 패키지 실행](#agent)  
  
-   [웹 서비스 또는 원격 구성 요소를 사용하여 프로그래밍 방식으로 원격 패키지 실행](#service)  
  
 이 항목에서 패키지를 로드하고 저장하는 데 사용되는 거의 모든 메서드에는 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. **System.Data**에 대한 참조만 필요한 **sp_start_job** 저장 프로시저를 실행하기 위해 이 항목에서 설명하는 ADO.NET 방법은 예외입니다. 새 프로젝트의 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조를 추가한 후 **using** 또는 **Imports** 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져옵니다.  
  
###  <a name="agent"></a> SQL Server 에이전트를 사용하여 서버에서 프로그래밍 방식으로 원격 패키지 실행  
 다음 코드 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 프로그래밍 방식으로 사용하여 서버에서 원격 패키지를 실행하는 방법을 보여 줍니다. 이 코드 샘플에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 시작하는 **sp_start_job** 시스템 저장 프로시저를 호출합니다. 이 프로시저가 시작하는 작업의 이름은 `RunSSISPackage`이며 이 작업은 원격 컴퓨터에 있습니다. 그런 다음 `RunSSISPackage` 작업은 원격 컴퓨터에서 패키지를 실행합니다.  
  
> [!NOTE]  
>  **sp_start_job** 저장 프로시저의 반환 값은 저장 프로시저에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 성공적으로 시작할 수 있었는지 여부를 나타내며, 패키지가 성공했는지 실패했는지를 나타내지는 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업에서 실행되는 패키지 문제를 해결하는 방법에 대한 자세한 내용은 [SSIS 패키지는 SQL Server 에이전트 작업 단계에서 호출 될 때 실행되지 않습니다.](http://support.microsoft.com/kb/918760) Microsoft 문서를 참조하세요.  
  
### <a name="sample-code"></a>예제 코드  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
###  <a name="service"></a> 웹 서비스 또는 원격 구성 요소를 사용하여 프로그래밍 방식으로 원격 패키지 실행  
 서버에서 프로그래밍 방식으로 패키지를 실행하기 위한 이전 솔루션의 경우 서버에서 사용자 지정 코드가 필요하지 않습니다. 그러나 SQL Server 에이전트를 사용하지 않고 패키지를 실행할 수 있는 솔루션이 필요한 경우가 있습니다. 다음 예에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 로컬로 시작하기 위해 서버에 만들 수 있는 웹 서비스와 클라이언트 컴퓨터에서 웹 서비스를 호출하는 데 사용할 수 있는 테스트 응용 프로그램을 보여 줍니다. 웹 서비스 대신 원격 구성 요소를 만들려면 원격 구성 요소를 거의 변경하지 않는 동일한 코드 논리를 사용할 수 있습니다. 그러나 원격 구성 요소를 만들 경우에는 웹 서비스를 만들 때보다 더욱 광범위한 구성이 필요할 수 있습니다.  
  
> [!IMPORTANT]  
>  인증 및 권한 부여에 기본 설정을 사용할 경우 웹 서비스에는 일반적으로 SQL Server 또는 파일 시스템에 액세스하여 패키지를 로드하고 실행할 수 있는 충분한 권한이 없습니다. **web.config** 파일에서 인증 및 권한 부여 설정을 구성하고 데이터베이스 및 파일 시스템 권한을 적절하게 할당하여 웹 서비스에 적절한 권한을 할당해야 할 수 있습니다. 웹, 데이터베이스 및 파일 시스템 사용 권한에 대한 자세한 설명은 이 항목에서 다루지 않습니다.  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
### <a name="sample-code"></a>예제 코드  
 다음 코드 예제에서는 웹 서비스를 만들고 테스트하는 방법을 보여 줍니다.  
  
#### <a name="creating-the-web-service"></a>웹 서비스 만들기  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 파일 또는 SQL Server에서 직접 로드하거나 SQL Server와 특수한 파일 시스템 폴더 모두의 패키지 저장소를 관리하는 SSIS 패키지 저장소에서 로드할 수 있습니다. 이 샘플에서는 **Select Case** 또는 **switch** 구문을 사용하여 패키지를 시작하기 위한 적절한 구문을 선택하고 입력 인수를 적절하게 연결함으로써 사용 가능한 모든 옵션을 지원합니다. LaunchPackage 웹 서비스 메서드는 클라이언트 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리에 대한 참조가 필요하지 않도록 패키지 실행 결과를 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 값 대신 정수로 반환합니다.  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>웹 서비스를 만들어 서버에서 프로그래밍 방식으로 패키지를 실행하려면  
  
1.  Visual Studio를 열고 원하는 프로그래밍 언어로 웹 서비스 프로젝트를 만듭니다. 예제 코드에서는 프로젝트 이름으로 LaunchSSISPackageService를 사용합니다.  
  
2.  **Microsoft.SqlServer.ManagedDTS**에 대한 참조를 추가하고, **Microsoft.SqlServer.Dts.Runtime** 네임스페이스에 대한 코드 파일에 **Imports** 또는 **using** 문을 추가합니다.  
  
3.  LaunchPackage 웹 서비스 메서드의 예제 코드를 클래스에 붙여 넣습니다. 이 예제에서는 코드 창의 전체 내용을 보여 줍니다.  
  
4.  LaunchPackage 메서드의 입력 인수 중 기존 패키지를 가리키는 인수에 올바른 값을 지정하여 웹 서비스를 빌드하고 테스트합니다. 예를 들어 package1.dtsx가 서버의 C:\My Packages에 저장되어 있는 경우 sourceType 값으로 "file"을 전달하고, sourceLocation 값으로 "C:\My Packages"를 전달하고, packageName 값으로 "package1"(확장명 없음)을 전달합니다.  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="http://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "http://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>웹 서비스 테스트  
 다음 예제 콘솔 응용 프로그램에서는 웹 서비스를 사용하여 패키지를 실행합니다. 웹 서비스의 LaunchPackage 메서드는 클라이언트 컴퓨터에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 어셈블리에 대한 참조가 필요하지 않도록 패키지 실행 결과를 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 값 대신 정수로 반환합니다. 이 예제에서는 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 값을 미러링하는 값을 포함하는 전용 열거형을 만들어 실행 결과를 보고합니다.  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>콘솔 응용 프로그램을 만들어 웹 서비스를 테스트하려면  
  
1.  Visual Studio에서 원하는 프로그래밍 언어를 사용하여 웹 서비스 프로젝트가 들어 있는 솔루션에 새 콘솔 응용 프로그램을 추가합니다. 예제 코드에서는 프로젝트 이름으로 LaunchSSISPackageTest를 사용합니다.  
  
2.  새 콘솔 응용 프로그램을 솔루션의 시작 프로젝트로 설정합니다.  
  
3.  웹 서비스 프로젝트에 대한 웹 참조를 추가합니다. 필요할 경우 예제 코드에서 웹 서비스 프록시 개체에 지정한 이름에 대한 변수 선언을 조정합니다.  
  
4.  기본 루틴 및 전용 열거형에 대한 예제 코드를 코드에 붙여 넣습니다. 이 예제에서는 코드 창의 전체 내용을 보여 줍니다.  
  
5.  LaunchPackage 메서드를 호출하는 코드 줄을 편집하여 기존 패키지를 가리키는 입력 인수에 올바른 값을 지정합니다. 예를 들어 package1.dtsx가 서버의 C:\My Packages에 저장되어 있는 경우 `sourceType` 값으로 "file"을 전달하고, `sourceLocation` 값으로 "C:\My Packages"를 전달하고, `packageName` 값으로 "package1"(확장명 없음)을 전달합니다.  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  
## <a name="external-resources"></a>외부 리소스  
  
-   technet.microsoft.com의 비디오 - [방법: SQL Server 에이전트를 사용하여 SSIS 패키지 실행 자동화(SQL Server 비디오)](http://technet.microsoft.com/sqlserver/ff686764.aspx)  
  
## <a name="see-also"></a>참고 항목  
 [로컬 실행과 원격 실행의 차이점 이해](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
