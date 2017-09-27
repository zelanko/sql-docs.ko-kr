---
title: ".NET 코드 (C#)와 함께 SSIS 프로젝트 배포 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: c83ad5be88951b92c59a7517ed2676ff30692d02
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>.NET 응용 프로그램에서 C# 코드가 사용 된 SSIS 프로젝트 배포
이 빠른 시작 자습서에는 데이터베이스 서버에 연결 하 고 SSIS 프로젝트를 배포 하는 C# 코드를 작성 하는 방법을 보여 줍니다.

C# 앱을 만들려면 Visual Studio, Visual Studio Code 또는 원하는 다른 도구를 사용할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 Visual studio 또는 Visual Studio Code 설치 되어 있는지 확인 합니다. 무료 Community 버전의 Visual Studio 또는 무료 Visual Studio Code에서 다운로드 [Visual Studio 다운로드](https://www.visualstudio.com/downloads/)합니다.

> [!NOTE]
> Azure SQL 데이터베이스 서버는 포트 1433에서 수신합니다. 회사 방화벽 내에서 Azure SQL 데이터베이스 서버에 연결 하려는 경우에이 포트에 성공적으로 연결 하면 회사 방화벽에서 열려 있어야 합니다.

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>SQL 데이터베이스에 배포 된 경우 연결 정보를 얻기 

Azure SQL 데이터베이스에 패키지를 배포 하면 SSIS 카탈로그 데이터베이스 (SSISDB)에 연결 하는 데 필요한 연결 정보를 가져옵니다. 다음에 나오는 절차의 정규화 된 서버 이름 및 로그인 정보를 해야 합니다.

1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. 선택 **SQL 데이터베이스** 왼쪽 메뉴를 클릭 하 여 SSISDB 데이터베이스에 **SQL 데이터베이스** 페이지. 
3. 에 **개요** 데이터베이스 페이지에서 정규화 된 서버 이름을 검토 합니다. (를) 실행 하는 **에 복사 하려면 클릭** 옵션을 서버 이름을 가리키도록 합니다. 
4. Azure SQL 데이터베이스 서버 로그인 정보를 잊은 경우 서버 관리자 이름을 확인 하려면 SQL 데이터베이스 서버 페이지로 이동 합니다. 필요한 경우 암호를 재설정할 수 있습니다.
5. 클릭 **데이터베이스 연결 문자열 표시**합니다.
6. 전체 검토 **ADO.NET** 연결 문자열입니다. 샘플 코드를 사용 하 여는 `SqlConnectionStringBuilder` 를 제공 하는 개별 매개 변수 값으로이 연결 문자열을 다시 만듭니다.

## <a name="create-a-new-visual-studio-project"></a>새 Visual Studio 프로젝트 만들기

1. Visual Studio에서 선택 **파일**, **새로**, **프로젝트**합니다. 
2. 에 **새 프로젝트** 대화 상자에서 확장 **Visual C#**합니다.
3. 선택 **콘솔 응용 프로그램** 입력 *deploy_ssis_project* 프로젝트 이름에 대 한 합니다.
4. 클릭 **확인** 을 만들고 Visual Studio에서 새 프로젝트를 엽니다.

## <a name="add-references"></a>참조 추가
1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 **참조** 폴더와 선택 **참조 추가**합니다. **참조 관리자** 대화 상자가 열립니다.
2. 에 **참조 관리자** 대화 상자에서 **어셈블리** 선택 **확장**합니다.
3. 다음 두 개의 참조를 추가 하려면 선택 합니다.
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. 클릭는 **찾아보기** 단추에 대 한 참조를 추가 하려면 **Microsoft.SqlServer.Management.IntegrationServices**합니다. (이 어셈블리는 전역 어셈블리 캐시 (GAC)에 설치 됨). **참조할 파일 선택** 대화 상자가 열립니다.
5. 에 **참조할 파일 선택** 대화 상자에서 어셈블리를 포함 하는 GAC 폴더로 이동 합니다. 일반적으로이 폴더는 `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`합니다.
6. 폴더와 클릭에서 어셈블리 (.dll 파일)를 선택 **추가**합니다.
7. 클릭 **확인** 를 닫으려면는 **참조 관리자** 대화 상자를 세 개의 참조를 추가 합니다. 참조가 사항이 하려면 체크는 **참조** 솔루션 탐색기의 목록입니다.

## <a name="add-the-c-code"></a>C# 코드를 추가 합니다. 
1. 열기 **Program.cs**합니다.

2. 내용을 대체 **Program.cs** 다음 코드를 사용 합니다. 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 합니다.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용 합니다. SQL Server 인증을 사용 하려면 대체는 `Integrated Security=SSPI;` 인수를 `User ID=<user name>;Password=<password>;`합니다.

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

1. 키를 눌러 응용 프로그램을 실행 하려면 **F5**합니다.
2. SSMS에서 프로젝트를 배포한 적이 있는지 확인 합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 하는 다른 방법을 고려 합니다.
    - [SSMS로 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [TRANSACT-SQL (VS Code)를 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [PowerShell과 함께 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
- 배포 된 패키지를 실행 합니다. 패키지를 실행 하려면 여러 가지 도구와 언어를 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조 합니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

