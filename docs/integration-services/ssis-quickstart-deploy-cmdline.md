---
title: 명령 프롬프트에서 SSIS 프로젝트 배포 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f1179443d8b86e23a51fdf2250f007914e27cf0b
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335867"
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>ISDeploymentWizard.exe를 사용하여 명령 프롬프트에서 SSIS 프로젝트 배포
이 빠른 시작에서는 Integration Services 배포 마법사인 `ISDeploymentWizard.exe`를 실행하여 명령 프롬프트에서 SSIS 프로젝트를 배포하는 방법을 보여줍니다.

Integration Services 배포 마법사에 대한 자세한 내용은 [ Integration Services 배포 마법사](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

Azure SQL Database에 대한 배포를 위해 이 아티클에서 설명한 유효성 검사에는 SSDT(SQL Server Data Tools) 버전 17.4 이상이 필요합니다. SSDT의 최신 버전을 얻으려면 [SQL Server Data Tools(SSDT) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

Azure SQL Database 서버는 1433 포트에서 수신 대기합니다. 회사 방화벽 내에서 Azure SQL Database 서버에 성공적으로 연결하려면 이 포트가 회사 방화벽에서 열려 있어야 합니다.

## <a name="supported-platforms"></a>지원 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에 SSIS 프로젝트를 배포할 수 있습니다.

-   Windows의 SQL Server

-   Azure SQL Database Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 SQL Server on Linux에 SSIS 패키지를 배포할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database에서 연결 정보 가져오기

Azure SQL Database에 프로젝트를 배포하려면 SSISDB(SSIS 카탈로그 데이터베이스)에 연결해야 하는 연결 정보를 가져옵니다. 다음 절차에는 정규화된 서버 이름과 로그인 정보가 필요합니다.

1. [Azure 포털](https://portal.azure.com/)에 로그인합니다.
2. 왼쪽 메뉴에서 **SQL Databases**를 선택한 다음, **SQL 데이터베이스** 페이지에서 SSISDB 데이터베이스를 선택합니다. 
3. 데이터베이스의 **개요** 페이지에서 정규화된 서버 이름을 검토합니다. **복사하려면 클릭** 옵션을 표시하려면 마우스로 서버 이름 위를 가리킵니다. 
4. Azure SQL Database 서버 로그인 정보를 잊은 경우, SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다. 필요한 경우 암호를 다시 설정할 수 있습니다.

## <a name="authentication-methods-in-the-deployment-wizard"></a>배포 마법사의 인증 방법

배포 마법사를 사용하여 SQL Server에 배포하는 경우 Windows 인증을 사용해야 합니다. SQL Server 인증을 사용할 수 없습니다.

Azure SQL Database 서버에 배포하는 경우 SQL Server 인증 또는 Azure Active Directory 인증을 사용해야 합니다. Windows 인증을 사용할 수 없습니다.

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사 시작
1. 명령 프롬프트 창을 엽니다.

2. `ISDeploymentWizard.exe`을 실행합니다. Integration Services 배포 마법사가 열립니다.

    `ISDeploymentWizard.exe`를 포함하고 있는 폴더가 `path` 환경 변수 내에 없으면 `cd` 명령을 사용하여 해당 디렉터리로 변경해야 합니다. SQL Server 2017의 경우 이 폴더는 일반적으로 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`입니다.

## <a name="deploy-a-project-with-the-wizard"></a>마법사를 사용하여 프로젝트 배포
1. 마법사의 **소개** 페이지에서 소개를 검토합니다. **다음**을 클릭하여 **원본 선택** 페이지를 엽니다.

2. **원본 선택** 페이지에서 배포할 기존 SSIS 프로젝트를 선택합니다.
    -   개발 환경에서 프로젝트를 빌드하여 만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일**을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그 데이터베이스에 배포된 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 다음, 카탈로그에 있는 프로젝트의 서버 이름과 경로를 입력합니다.
    **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.
  
3.  **대상 선택** 페이지에서 프로젝트의 대상을 선택합니다.
    -   정규화된 서버 이름을 입력합니다. 대상 서버가 Azure SQL Database 서버인 경우 이름은 `<server_name>.database.windows.net` 형식입니다.
    -   인증 정보를 입력한 다음, **연결**을 선택합니다. 이 아티클에서 [배포 마법사의 인증 방법](#wizard_auth)을 참조하세요.
    -   그런 다음 **찾아보기**를 선택하여 SSISDB에서 대상 폴더를 선택합니다.
    -   그런 다음, **다음**을 선택하여 **검토** 페이지를 엽니다. (**연결**을 선택하면 **다음** 단추가 활성화됩니다.)

4.  **검토** 페이지에서 선택한 설정을 검토합니다.
    -   **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.
    -   **배포** 를 클릭해 배포 프로세스를 시작합니다.

5.  Azure SQL Database 서버에 배포하는 경우 **유효성 검사** 페이지가 열리고 프로젝트의 패키지를 검사하여 Azure SSIS Integration Runtime에서 패키지가 예상대로 실행되지 않을 수 있는 알려진 문제점을 찾습니다. 자세한 내용은 [Azure에 배포된 SSIS 패키지 유효성 검사](lift-shift/ssis-azure-validate-packages.md)를 참조하세요.

6.  배포 프로세스가 완료되면 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업이 실패하면 **결과** 열에서 **실패**를 클릭하여 해당 오류에 대한 설명을 표시합니다.
    -   필요에 따라 **보고서 저장...** 을 클릭하여 결과를 XML 파일에 저장합니다.
    -   **닫기**를 클릭하여 마법사를 종료합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL(VS 코드)을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [PowerShell을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
    - [C#을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포된 패키지를 실행합니다. 패키지를 실행하려면 여러 도구와 언어 중에서 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
