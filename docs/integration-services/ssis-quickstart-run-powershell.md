---
title: "PowerShell에서 SSIS 패키지 실행 | Microsoft Docs"
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
ms.openlocfilehash: d392ac49442ef0f04961908fff7acf553fa1aa57
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-powershell"></a>PowerShell에서 SSIS 패키지 실행
이 빠른 시작 자습서에는 데이터베이스 서버에 연결 하 고 SSIS 패키지를 실행 하는 PowerShell 스크립트를 사용 하는 방법을 보여 줍니다.

## <a name="powershell-script"></a>PowerShell 스크립트
다음 스크립트 맨 위에 있는 변수에 대 한 적절 한 값을 제공 하 고 SSIS 패키지를 실행 하는 스크립트를 실행 하십시오.

> [!NOTE]
> 다음 예제에서는 Windows 인증을 사용 합니다. SQL Server 인증을 사용 하려면 대체는 `Integrated Security=SSPI;` 인수를 `User ID=<user name>;Password=<password>;`합니다.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

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

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>다음 단계
- 다른 방법으로 패키지를 실행 하는 것이 좋습니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

