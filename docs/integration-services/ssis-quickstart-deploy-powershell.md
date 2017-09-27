---
title: "PowerShell과 함께 SSIS 프로젝트 배포 | Microsoft Docs"
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
ms.openlocfilehash: 37fe358eb7e11cb878ebd9b0c8356ac2295ca7e9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-powershell"></a>PowerShell과 함께 SSIS 프로젝트 배포
이 빠른 시작 자습서에는 데이터베이스 서버에 연결 하 여 SSIS 카탈로그에 SSIS 프로젝트를 배포 하는 PowerShell 스크립트를 사용 하는 방법을 보여 줍니다.

## <a name="powershell-script"></a>PowerShell 스크립트
다음 스크립트 맨 위에 있는 변수에 대 한 적절 한 값을 제공 하 고 SSIS 프로젝트를 배포 하는 스크립트를 실행 하십시오.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용 합니다. SQL Server 인증을 사용 하려면 대체는 `Integrated Security=SSPI;` 인수를 `User ID=<user name>;Password=<password>;`합니다.

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
- 패키지를 배포 하는 다른 방법을 고려 합니다.
    - [SSMS로 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [TRANSACT-SQL (VS Code)를 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 배포](./ssis-quickstart-deploy-cmdline.md)
    - [C#과 함께 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포 된 패키지를 실행 합니다. 패키지를 실행 하려면 여러 가지 도구와 언어를 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조 합니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

