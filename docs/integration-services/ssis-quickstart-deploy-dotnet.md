---
description: .NET 앱에 C# 코드가 있는 SSIS 프로젝트 배포
title: .NET 코드를 사용하여 SSIS 프로젝트 배포(C#) | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70bca79279d8db0bad18e1ee7ce9e4648dfb3c36
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129991"
---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>.NET 앱에 C# 코드가 있는 SSIS 프로젝트 배포

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


이 빠른 시작에서는 C# 코드를 작성하여 데이터베이스 서버에 연결하고 SSIS 프로젝트를 배포하는 방법을 보여줍니다.

C# 앱을 만들려면 Visual Studio, Visual Studio Code 또는 원하는 다른 도구를 사용할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하기 전에 Visual Studio 또는 Visual Studio Code가 설치되어 있는지 확인합니다. [Visual Studio 다운로드](https://www.visualstudio.com/downloads/)에서 Visual Studio Community Edition 버전 평가판 또는 Visual Studio Code 평가판을 다운로드합니다.

Azure SQL Database 서버는 포트 1433에서 수신 대기합니다. 회사 방화벽 내에서 Azure SQL Database 서버에 성공적으로 연결하려면 이 포트가 회사 방화벽에서 열려 있어야 합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에 SSIS 프로젝트를 배포할 수 있습니다.

-   Windows의 SQL Server

-   Azure SQL Database. Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 SQL Server on Linux에 SSIS 패키지를 배포할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database에서 연결 정보 가져오기

Azure SQL Database에 프로젝트를 배포하려면 SSISDB(SSIS 카탈로그 데이터베이스)에 연결해야 하는 연결 정보를 가져옵니다. 다음 절차에는 정규화된 서버 이름과 로그인 정보가 필요합니다.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **SQL Databases** 를 선택한 다음, **SQL 데이터베이스** 페이지에서 SSISDB 데이터베이스를 선택합니다. 
3. 데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다. **복사하려면 클릭** 옵션을 표시하려면 마우스로 서버 이름 위를 가리킵니다. 
4. Azure SQL Database 서버 로그인 정보를 잊은 경우, SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다. 필요한 경우 암호를 다시 설정할 수 있습니다.
5. **데이터베이스 연결 문자열 표시** 를 클릭합니다.
6. **ADO.NET** 연결 문자열 전체를 검토합니다. 필요에 따라 코드에서는 `SqlConnectionStringBuilder`를 사용하여 사용자가 제공한 개별 매개 변수 값으로 이 연결 문자열을 다시 작성할 수 있습니다.

## <a name="supported-authentication-method"></a>지원되는 인증 방법

[배포를 위한 인증 방법](ssis-quickstart-deploy-ssms.md#authentication-methods-for-deployment)을 참조하세요.

## <a name="create-a-new-visual-studio-project"></a>새 Visual Studio 프로젝트 만들기

1. Visual Studio에서 **파일**, **새로 만들기**, **프로젝트** 를 차례로 선택합니다. 
2. **새 프로젝트** 대화 상자에서 **Visual C#** 을 펼칩니다.
3. **콘솔 앱** 을 선택하고 프로젝트 이름으로 *deploy_ssis_project* 를 입력합니다.
4. **확인** 을 클릭하여 Visual Studio에서 새 프로젝트를 만들고 엽니다.

## <a name="add-references"></a>참조 추가
1. [솔루션 탐색기]에서 **참조** 폴더를 마우스 오른쪽 단추로 클릭하고 **참조 추가** 를 선택합니다. **참조 관리자** 대화 상자가 열립니다.
2. **참조 관리자** 대화 상자에서 **어셈블리** 를 펼치고 **확장** 을 선택합니다.
3. 다음 두 개의 참조를 선택하여 추가합니다.
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. **찾아보기** 단추를 클릭하여 **Microsoft.SqlServer.Management.IntegrationServices** 에 대한 참조를 추가합니다. (이 어셈블리는 GAC(전역 어셈블리 캐시)에만 설치됩니다.) **참조할 파일 선택** 대화 상자가 열립니다.
5. **참조할 파일 선택** 대화 상자에서 어셈블리를 포함한 GAC 폴더로 이동합니다. 일반적으로 이 폴더는 `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`입니다.
6. 폴더에서 어셈블리(즉 .dll 파일)를 선택하고 **추가** 를 클릭합니다.
7. **확인** 을 클릭하여 **참조 관리자** 대화 상자를 닫고 세 개의 참조를 추가합니다. 참조가 있는지 확인하려면 [솔루션 탐색기]에서 **참조** 목록을 확인합니다.

## <a name="add-the-c-code"></a>C# 코드 추가 
1. **Program.cs** 를 엽니다.

2. **Program.cs** 의 내용을 다음 코드로 바꿉니다. 서버, 데이터베이스, 사용자 및 암호에 적절한 값을 추가합니다.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용합니다. SQL Server 인증을 사용하려면 `Integrated Security=SSPI;` 인수를 `User ID=<user name>;Password=<password>;`로 바꿉니다. Azure SQL Database 서버에 연결하는 경우 Windows 인증을 사용할 수 없습니다.

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>코드 실행

1. 응용 프로그램을 실행하려면 **F5** 키를 누릅니다.
2. SSMS에서 프로젝트가 배포되었는지 확인합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL(VS 코드)을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
- 배포된 패키지를 실행합니다. 패키지를 실행하려면 여러 도구와 언어 중에서 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
