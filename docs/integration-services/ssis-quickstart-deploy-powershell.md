---
title: PowerShell을 사용하여 SSIS 프로젝트 배포 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
ms.openlocfilehash: efcda9dd280a7341f1b1dc398c1e325c71a79a9a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100833"
---
# <a name="deploy-an-ssis-project-with-powershell"></a>PowerShell을 사용하여 SSIS 프로젝트 배포

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 빠른 시작에서는 PowerShell 스크립트를 사용하여 데이터베이스 서버에 연결하고 SSIS 프로젝트를 SSIS 카탈로그에 배포하는 방법을 보여줍니다.

## <a name="prerequisites"></a>사전 요구 사항

Azure SQL Database 서버는 1433 포트에서 수신 대기합니다. 회사 방화벽 내에서 Azure SQL Database 서버에 성공적으로 연결하려면 이 포트가 회사 방화벽에서 열려 있어야 합니다.

## <a name="supported-platforms"></a>지원 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에 SSIS 프로젝트를 배포할 수 있습니다.

-   Windows의 SQL Server

-   Azure SQL Database Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 SQL Server on Linux에 SSIS 패키지를 배포할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database에서 연결 정보 가져오기

Azure SQL Database에 프로젝트를 배포하려면 SSISDB(SSIS 카탈로그 데이터베이스)에 연결해야 하는 연결 정보를 가져옵니다. 다음 절차에는 정규화된 서버 이름과 로그인 정보가 필요합니다.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **SQL Databases**를 선택한 다음, **SQL 데이터베이스** 페이지에서 SSISDB 데이터베이스를 선택합니다. 
3. 데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다. **복사하려면 클릭** 옵션을 표시하려면 마우스로 서버 이름 위를 가리킵니다. 
4. Azure SQL Database 서버 로그인 정보를 잊은 경우, SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다. 필요한 경우 암호를 다시 설정할 수 있습니다.
5. **데이터베이스 연결 문자열 표시**를 클릭합니다.
6. **ADO.NET** 연결 문자열 전체를 검토합니다.

## <a name="ssis-powershell-provider"></a>SSIS PowerShell 공급자
다음 스크립트를 기반으로 변수에 적절한 값을 제공한 후 SSIS 프로젝트를 배포하는 스크립트를 실행하세요.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용하여 SQL Server 온-프레미스를 배포합니다. `New-PSDive` cmdlet을 통해 SQL Server 인증을 사용하여 연결을 설정합니다. Azure SQL Database 서버에 연결하는 경우 Windows 인증을 사용할 수 없습니다.

```powershell
# Variables
$TargetInstanceName = "localhost\default"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Get the Integration Services catalog
$catalog = Get-Item SQLSERVER:\SSIS\$TargetInstanceName\Catalogs\SSISDB\

# Create the target folder
New-Object "Microsoft.SqlServer.Management.IntegrationServices.CatalogFolder" ($catalog, 
$TargetFolderName,"Folder description") -OutVariable folder
$folder.Create()

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

# Verify packages were deployed.
dir "$($catalog.PSPath)\Folders\$TargetFolderName\Projects\$ProjectName\Packages" | 
SELECT Name, DisplayName, PackageId
```

## <a name="powershell-script"></a>PowerShell 스크립트
다음 스크립트를 기반으로 변수에 적절한 값을 제공한 후 SSIS 프로젝트를 배포하는 스크립트를 실행하세요.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용하여 SQL Server 온-프레미스를 배포합니다. SQL Server 인증을 사용하려면 `Integrated Security=SSPI;` 인수를 `User ID=<user name>;Password=<password>;`로 바꿉니다. Azure SQL Database 서버에 연결하는 경우 Windows 인증을 사용할 수 없습니다.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>다음 단계
- 패키지를 배포하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL(VS 코드)을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [C#을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포된 패키지를 실행합니다. 패키지를 실행하려면 여러 도구와 언어 중에서 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
