---
title: Azure에서 SSIS 패키지 배포 및 실행 | Microsoft Docs
description: SSIS(SQL Server Integration Services) 프로젝트를 Azure SQL Database에서 SSIS 카탈로그에 배포하고 패키지를 실행하는 방법을 알아봅니다
ms.date: 05/22/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 42250d8edbd646f9bd89f3663f2591b3404fe05f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68007944"
---
# <a name="tutorial-deploy-and-run-a-sql-server-integration-services-ssis-package-in-azure"></a>자습서: Azure에 SSIS(SQL Server Integration Services) 패키지 배포 및 실행

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 자습서에서는 SSIS(SQL Server Integration Services) 프로젝트를 Azure SQL Database의 SSIS 카탈로그에 배포하고, Azure-SSIS Integration Runtime에서 패키지를 실행하고, 실행 중인 패키지를 모니터링하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하기 전에 SQL Server Management Studio 버전 17.2 이상이 설치되어 있는지 확인합니다. SSMS의 최신 버전을 다운로드하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.

또한 Azure에서 SSISDB 데이터베이스를 설정하고 Azure-SSIS Integration Runtime을 프로비전했는지 확인합니다. Azure에서 SSIS를 프로비전하는 방법에 대한 자세한 내용은 [Azure에 SQL Server Integration Services 패키지 배포](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)를 참조하세요.

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database에서 연결 정보 가져오기

Azure SQL Database에서 패키지를 실행하려면 SSISDB(SSIS 카탈로그 데이터베이스)에 연결해야 하는 연결 정보를 가져옵니다. 다음 절차에는 정규화된 서버 이름과 로그인 정보가 필요합니다.

1. [Azure Portal](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **SQL Databases**를 선택한 다음, **SQL 데이터베이스** 페이지에서 SSISDB 데이터베이스를 선택합니다. 
3. 데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다. **복사하려면 클릭** 옵션을 표시하려면 마우스로 서버 이름 위를 가리킵니다. 
4. Azure SQL Database 서버 로그인 정보를 잊은 경우, SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다. 필요한 경우 암호를 다시 설정할 수 있습니다.

## <a name="connect-to-the-ssisdb-database"></a>SSISDB 데이터베이스에 연결

SQL Server Management Studio를 사용하여 Azure SQL Database 서버의 SSIS 카탈로그에 연결합니다. 자세한 내용과 스크린샷은 [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)을 참조하세요.

기억해야 할 중요한 두 가지 항목은 다음과 같습니다. 이러한 단계는 다음 절차에서 설명합니다.
-   Azure SQL Database 서버의 정규화된 이름을 **mysqldbserver.database.windows.net** 형식으로 입력합니다.
-   연결할 데이터베이스로 `SSISDB`을 선택합니다.

> [!IMPORTANT]
> Azure SQL Database 서버는 포트 1433에서 수신 대기합니다. 회사 방화벽 내에서 Azure SQL Database 서버에 성공적으로 연결하려면 이 포트가 회사 방화벽에서 열려 있어야 합니다.

1. SQL Server Management Studio를 엽니다.

2. **서버에 연결합니다**. **서버에 연결** 대화 상자에 다음 정보를 입력합니다.

   | 설정       | 제안 값 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **서버 유형** | 데이터베이스 엔진 | 이 값은 필수입니다. |
   | **서버 이름** | 정규화된 서버 이름 | **mysqldbserver.database.windows.net** 형식이어야 합니다. 서버 이름이 필요한 경우 [Azure에서 SSISDB 카탈로그 데이터베이스에 연결](ssis-azure-connect-to-catalog-database.md)을 참조하세요. |
   | **인증** | SQL Server 인증 | Windows 인증을 사용하여 Azure SQL Database에 연결할 수 없습니다. |
   | **로그인** | 서버 관리자 계정 | 서버를 만들 때 지정한 계정입니다. |
   | **암호** | 서버 관리자 계정의 암호 | 서버를 만들 때 지정한 암호입니다. |

3. **SSISDB 데이터베이스에 연결합니다**. **옵션**을 선택하여 **서버에 연결** 대화 상자를 펼칩니다. 펼쳐진 **서버에 연결** 대화 상자에서 **연결 속성** 탭을 선택합니다. **데이터베이스에 연결** 필드에서 `SSISDB`를 선택하거나 입력합니다.

4. 그런 다음 **연결**을 선택합니다. SSMS에서 개체 탐색기 창이 열립니다. 

5. 개체 탐색기에서 **Integration Services 카탈로그**, **SSISDB**를 차례로 펼쳐 SSIS 카탈로그 데이터베이스의 개체를 봅니다.

## <a name="deploy-a-project-with-the-deployment-wizard"></a>배포 마법사를 사용하여 프로젝트 배포

패키지 배포 및 배포 마법사에 대한 자세한 내용은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../packages/deploy-integration-services-ssis-projects-and-packages.md) 및 [Integration Services 배포 마법사](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)를 참조하세요.

> [!NOTE]
> 프로젝트 배포 모델만 Azure에 배포할 수 있습니다.

### <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사 시작
1. **Integration Services 카탈로그** 노드와 **SSISDB** 노드가 펼쳐진 SSMS의 [개체 탐색기]에서 프로젝트 폴더를 펼칩니다.

2.  **프로젝트** 노드를 선택합니다.

3.  **프로젝트** 노드를 마우스 오른쪽 단추로 클릭하고 **프로젝트 배포**를 선택합니다. Integration Services 배포 마법사가 열립니다. SSIS 카탈로그 데이터베이스 또는 파일 시스템에서 프로젝트를 배포할 수 있습니다.

    ![SSMS에서 프로젝트 배포](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![SSIS 배포 마법사 대화 상자가 열립니다.](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>배포 마법사를 사용하여 프로젝트 배포
1. [배포 마법사]의 **소개** 페이지에서 소개를 검토합니다. **다음**을 선택하여 **원본 선택** 페이지를 엽니다.

2. **원본 선택** 페이지에서 배포할 기존 SSIS 프로젝트를 선택합니다.
    -   만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 다음 카탈로그에 있는 프로젝트의 서버 이름과 경로를 입력합니다.
    -   **다음**을 선택하여 **대상 선택** 페이지를 표시합니다.
  
3.  **대상 선택** 페이지에서 프로젝트의 대상을 선택합니다.
    -   `<server_name>.database.windows.net` 형식으로 정규화된 서버 이름을 입력합니다.
    -   인증 정보를 입력한 다음, **연결**을 선택합니다.
    -   그런 다음 **찾아보기**를 선택하여 SSISDB에서 대상 폴더를 선택합니다.
    -   그런 다음, **다음**을 선택하여 **검토** 페이지를 엽니다. (**연결**을 선택하면 **다음** 단추가 활성화됩니다.)
  
4.  **검토** 페이지에서 선택한 설정을 검토합니다.
    -   **이전**을 선택하거나 왼쪽 창에서 단계 중 하나를 선택하여 선택 항목을 변경할 수 있습니다.
    -   **배포**를 선택하여 배포 프로세스를 시작합니다.

    > [!NOTE]
    > **활성 작업자 에이전트가 없습니다.(.NET SqlClient Data Provider)** 오류 메시지가 나타나면 Azure-SSIS Integration Runtime이 실행 중인지 확인합니다. Azure-SSIS IR이 중지된 상태에서 배포하려고 시도하면 이 오류가 발생합니다.

5.  배포 프로세스가 완료되면 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업이 실패하면 **결과** 열에서 **실패**를 선택하여 해당 오류에 대한 설명을 표시합니다.
    -   필요에 따라 **보고서 저장...** 을 선택하여 결과를 XML 파일에 저장합니다.
    -   **닫기**를 선택하여 마법사를 종료합니다.

## <a name="deploy-a-project-with-powershell"></a>PowerShell을 사용하여 프로젝트 배포

PowerShell을 사용하여 Azure SQL Database의 SSISDB에 프로젝트를 배포하려면 다음 스크립트를 요구 사항에 맞게 조정합니다. 이 스크립트는 `$ProjectFilePath` 아래의 자식 폴더와 각 자식 폴더의 프로젝트를 열거한 후 SSISDB에 동일한 폴더를 만들고 이러한 폴더에 프로젝트를 배포합니다.

이 스크립트를 실행하려면 스크립트를 실행하는 컴퓨터에 SQL Server Data Tools 버전 17.x 또는 SQL Server Management Studio가 설치되어 있어야 합니다.

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>패키지 실행

1. SSMS의 [개체 탐색기]에서 실행하려는 패키지를 선택합니다.

2. 마우스 오른쪽 단추로 클릭하고 **실행**을 선택하여 **패키지 실행** 대화 상자를 엽니다.

3.  **패키지 실행**대화 상자에서 **매개 변수**, **연결 관리자** 및 **고급** 탭의 설정을 사용하여 패키지 실행을 구성합니다.

4.  **확인**을 선택하여 패키지를 실행합니다.

## <a name="monitor-the-running-package-in-ssms"></a>SSMS에서 실행 중인 패키지 모니터링

Integration Services 서버에서 현재 실행 중인 Integration Services 작업의 상태(예: 배포, 유효성 검사 및 패키지 실행)를 보려면 SSMS의 **활성 작업** 대화 상자를 사용합니다. **활성 작업** 대화 상자를 열려면 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **활성 작업**을 선택합니다.

또한 [개체 탐색기]에서 패키지를 선택하여 마우스 오른쪽 단추로 클릭하고, **보고서**, **표준 보고서**, **모든 실행**을 차례로 선택할 수도 있습니다.

SSMS에서 실행 중인 패키지를 모니터링하는 방법에 대한 자세한 내용은 [실행 중인 패키지 및 기타 작업 모니터링](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations)을 참조하세요.

## <a name="monitor-the-execute-ssis-package-activity"></a>SSIS 패키지 작업 실행 모니터링

SSIS 패키지 작업 실행을 사용하여 Azure Data Factory 파이프라인의 일부로 패키지를 실행 중인 경우 Data Factory UI에서 파이프라인 실행을 모니터링할 수 있습니다. 그런 다음, 작업 실행의 출력에서 SSISDB 실행 ID를 가져오고 해당 ID를 사용하여 SSMS에서 보다 포괄적인 실행 로그 및 오류 메시지를 확인할 수 있습니다.

![Data Factory에 패키지 실행 ID 가져오기](media/ssis-azure-deploy-run-monitor-tutorial/get-execution-id.png)

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime 모니터링

패키지가 실행 중인 Azure-SSIS Integration Runtime에 대한 상태 정보를 가져오려면 다음 PowerShell 명령을 사용합니다. 각 명령에서 Data Factory, Azure SSIS IR 및 리소스 그룹의 이름을 제공합니다.

자세한 내용은 [Azure-SSIS Integration Runtime 모니터](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime)를 참조하세요.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime에 대한 메타데이터 가져오기

```powershell
Get-AzDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime에 대한 상태 가져오기

```powershell
Get-AzDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>다음 단계
- 패키지 실행을 예약하는 방법을 알아봅니다. 자세한 내용은 [Azure에서 SSIS 패키지 실행 예약](ssis-azure-schedule-packages.md)을 참조하세요.
